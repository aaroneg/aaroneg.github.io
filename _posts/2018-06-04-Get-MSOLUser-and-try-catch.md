---
title: "Get-MSOLUser and try/catch in powershell"
categories: powershell
author: aaroneg
tags: rage powershell microsoft MSOnline
---
# Summary
If you're depending on try/catch to see if a Microsoft Online user exists, you have to use `-ErrorAction Stop` because some idiot thought that a cmdlet that cannot do it's one job shouldn't return a terminating error. If you don't do this, Get-MSOLUser will return a non-terminating error and the catch block will not fire.


