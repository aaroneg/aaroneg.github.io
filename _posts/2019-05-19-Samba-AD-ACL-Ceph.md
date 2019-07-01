---
title: "Combining Samba, Active Directory, ACLs and Ceph"
categories: ceph
author: aaroneg
tags: 
---

# AD Integrated Samba server, with ACLs

I had a need to create a Samba server, exposing a cephfs filesystem that uses ACLs tied to Active Directory identities. Here is the lab setup. Be aware that this entire process is incredibly irritating and prone to failure, largely due to the need for SSSD. SSSD is hard to troubleshoot in any meaningful way - you can turn debugging up as high as it goes but actually identifying and fixing the problem can still be difficult or impossible in any reasonable amount of time.

## Lab Environment

| Machine Name | OS | Description |
|---------|:---:|-----------:|
|gateway|pfsense|firewall/router|
|adc|Windows 2019 Core|Domain Controller|
|samba |OpenSUSE Leap 15.0|SMB server|
|ubclient|Ubuntu 19.01 (disco dingo)|Linux client|
|wxclient|Windows 10, 1809|Windows Client to manage domain and test fileshares|

> I am only going into great detail on the samba server as far as AD membership goes. For all other machines and OSs, follow the correct documentation for your OS and version. For Linux, you will almost always want to look up how to use realmd to join AD. You do not need FreeIPA for any reason.

## Active Directory

You will need an AD controller up and working with a domain. You can create as many users as you like to test with, and place them in groups that you will use to test with. Creating a domain is outside the scope of this document, especially since if you're doing this for real, you already have a domain.

## Samba Server

### Lab Setup Decisions probably unsuitable for production:

* I did remove apparmor based on my experience with it so far. It's fine for a lab, but you'll probably want to re-examine this for production.
* The firewall is also disabled on the lab samba server. For production you will want to enable and configure the firewall.
* This server is a VM both for lab reasons and so I can revert to snapshots before doing things that might mess up the setup. SSSD is really fragile and if it breaks, you're kind of hosed.
* The machine also has IPv6 disabled. If you disable ipv6, that will take a reboot to take effect.

### Lab Setup Steps (OpenSUSE)

* Install and configure a base OpenSUSE server
  * Choose "Server" role, as opposed to a desktop install to avoid unrelated software like office suites and games. This will save on the amount of space required for the system, along with patching speed.
  * The default server software package includes samba, along with the YAST modules you'll need.
  * Set the hostname & ip you want for your machine during setup or immediately after. Be sure and make your domain controller the primary DNS server, or that the DNS server you set has a proper delegation for the AD domain. In this lab setup, the FQDN for the general network and AD match, and AD is the authoritative source for all DNS information on this network.
* Join the domain using the "User Logon Management" YaST module. I recommend that you don't try to be too fancy here. This is a samba server, so you don't need to mess with sudo rules, etc. On the global options, you can add the `default_domain_suffix` as your AD domain `IN.ALL.UPPERCASE` as that is the most reliable way I have found.
  * For service options, I recommend adding the extended option `debug_level` **for both authentication and name switch**, because this will help you if you are ever stuck troubleshooting SSSD and the complex interactions it has with the rest of the system and AD. 
  * When adding the domain, choose the option to override samba config to work with this domain, it will save time and setup later.
  * When you've finished enrolling in the domain, go back and add `debug_level` to the domain entry as well, and set to 9. This will save us time later, and we can always go back and turn the debug level down on all of these components.
  * See [3] for instructions.
  * For Ubuntu: [4]
  * Centos / RHEL [5]

### Samba Config

We'll start here by providing a normal basic disk-backed share config, and specialize into Ceph later in the document.

The good news is that if you were successful in joining the domain and setting the options to override the samba config file, there's not much to do here other than create some shares. There are however a few things to keep in mind on each share:

Create the folders you want to share in advance. Create the folders using the root user, or sudo equivalent. Owner and Group should be root.

Create the shares from these folders. it's pretty easy, here is an example from `smb.conf`

```
[documents]
        comment = company documents
        inherit acls = Yes
        path = /srv/samba/documents
        read only = No
        vfs objects = streams_xattr acl_xattr
```

Things to keep in mind:

* `inherit acls = Yes` should be specified on each share
* To enable windows to see and respect the ACLs, you'll also need `vfs objects = streams_xattr acl_xattr` on each share.

That's pretty much all you have to do on the Samba side of things for now.

### ACLs and Security

> A note about windows ACLs: You can see and sometimes change the ACLs from windows explorer. I suggest that you do not. They only seem to have an effect on windows clients, and Linux clients ignore them, even when accessing them through a samba share.

Apply the following commands to set default permissions to the root level shares, replacing `home` with your domain's shortname, and `./` with the full path to the folder you're sharing: 
```
sudo setfacl -m g:'domain users@home':rx ./documents
sudo setfacl -m g:'domain users@home':rx ./homes
sudo setfacl -Rm g:'domain admins@home':rwx ./homes
sudo setfacl -Rm g:'domain admins@home':rwx ./documents
```

This will allow domain admins full, inheriting permissions to these folders and subfolders, and rights to **view** the top level of the folders only. This permission does not inherit.

# References

## Identity management / AD integration

### SUSE

* [The SSSD, Active Directory, and growing SLES integration][1]
* [How to configure sssd on SLES 12 to authenticate against LDAP.][2]
* [Joining Active Directory Using User Logon Management][3]
  

[1]: https://www.suse.com/c/the-sssd-active-directory-and-sles-12-and-15/
[2]: https://www.suse.com/support/kb/doc/?id=7017932
[3]: https://www.suse.com/documentation/sles-12/book_security/data/sec_security_ad_config.html#sec_security_ad_sssd
[4]: https://help.ubuntu.com/lts/serverguide/sssd-ad.html.en
[5]: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/windows_integration_guide/ch-configuring_authentication