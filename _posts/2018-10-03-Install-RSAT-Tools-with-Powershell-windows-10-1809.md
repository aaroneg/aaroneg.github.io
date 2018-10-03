---
title: "Install RSAT tools with Powershell on Windows 10 1809 release"
categories: rsat
author: aaroneg
tags: rsat powershell
---
# Summary
How to install all RSAT features on Windows 10 release 1809 with powershell.

# Intro
With the release of Windows 10, 1809 yesterday I immediately needed all my RSAT tools back, and clicking on each feature to install it manually is a pain. 

```powershell
Get-WindowsCapability -Online | ? Name -like 'RSAT*'|Where {$_.State -eq 'NotPresent'} |foreach {Add-WindowsCapability -online -name $_.Name}
```
# Warning
Depending on your organization's settings, you may run into errors when your computer tries to download from a windows update server and can't. 

See this article for a workaround:
https://vniklas.djungeln.se/2017/12/20/install-ssh-client-as-a-optional-feature-on-windows-10-failed/
