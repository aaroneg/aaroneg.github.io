---
title: "Tracking Down Enterprise CAs using powershell"
categories: pki enterprise certificate authority powershell
author: aaroneg
---
# Summary
How to find a list of certificate authorities in your domain

# Intro
I needed to find a way to get the list of CAs present in my domain to revamp my script that allows you to automatically get a code signing cert, if your CA allows it.

# Finding where AD lists known, trusted CAs
There was probably a better way to do this, but I figured it would be fairly obvious in ADSI edit. I was right. 

> **DO NOT USE ADSI TO EDIT ANYTHING, EVER - UNLESS A PAID SUPPORT PERSON HAS TOLD YOU TO DO SO**

>> Also, it's a good idea to not even open the program if you are a clumsy or otherwise un-careful person. You can fuck up your domain pretty hard with this tool. In this article, I use it in a read-only manner.

I started by right clicking the ADSI Edit node in the top-left corner of the window, choosing "Connect to...", and switching the "Configuration" well known naming context - leaving all other options at their defaults.

![An image showing the "Connect to" dialog from ADSI Edit with the mouse cursor over the "Configuration" well known naming context]({{ site.baseurl }}/assets/ADSI-Connect-Configuration.png "Connect to the Configuration Context")

Since an Enterprise CA sounds like a service to me, I expanded the "CN=Services" container, then the "CN=Public Key Services", then "CN=Certification Services". This is pretty obviously the thing i'm looking for, so now I know it's easy to find out what my domain offers. 

Now I know that it's possible to find the information I want, I have an idea of how to get this information in powershell. Because this script is meant to be generally available, I'll have powershell do some of the leg work of figuring out information about the environment, instead of using variables at the top of the file or prompting for information.

<aside class="notice">
You'll need the AD RSAT tools installed to use this script. 
</aside>

```powershell
# Read the current domain ( https://msdn.microsoft.com/en-us/library/system.directoryservices.activedirectory.domain(v=vs.110).aspx )
$CurrentDomainRootDN=[System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain().GetDirectoryEntry().distinguishedName
# Construct the EnrollmentDN from the domain root DN
$EnrollmentDN="CN=Enrollment Services,CN=Public Key Services,CN=Services,CN=Configuration,$CurrentDomainRootDN"
# Force powershell to treat the result as an array - weird things can happen during processing later if there is one result when you expected several.
[array]$EnrollmentServices=Get-ADObject -SearchBase $EnrollmentDN -LDAPFilter "(objectClass=pKIEnrollmentService)" -Properties dNSHostName
# Write the enrollment services to the console
$EnrollmentServices
```

This helps us automate portions of the script. Now we turn it into a function to use later. 

```powershell
function Get-DomainEnrollmentServices () {
    # Read the current domain ( https://msdn.microsoft.com/en-us/library/system.directoryservices.activedirectory.domain(v=vs.110).aspx )
    $CurrentDomainRootDN=[System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain().GetDirectoryEntry().distinguishedName
    # Construct the EnrollmentDN from the domain root DN
    $EnrollmentDN="CN=Enrollment Services,CN=Public Key Services,CN=Services,CN=Configuration,$CurrentDomainRootDN"
    # Force powershell to treat the result as an array - weird things can happen during processing later if there is one result when you expected several.
    [array]$EnrollmentServices=Get-ADObject -SearchBase $EnrollmentDN -LDAPFilter "(objectClass=pKIEnrollmentService)" -Properties dNSHostName
    $EnrollmentServices
}
``` 
