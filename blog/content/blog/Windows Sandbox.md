+++
author = "Matt Browne"
categories = [""]
date = ""
description = "Windows Sandbox"
featured = "pipes.jpeg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = ""
tags = [""]
type = "post"
draft = "true"
+++

## What is Windows Sandbox

## What do I need to run it

* You need Windows 10 Pro or Enterprise x64
* You need to be running Windows 10 build 18305 or higher
* On physical machines you need virtualisation turned on in the BIOS.
* On a virtual machine you need to enable 'Nested Virtualisation' 
* At least 4Gb RAM
* At least 2 Cores


## How do I get Windows Sandbox

On your Windows 10 machine go to *Settings -> Apps -> Apps & Features -> Programs and Features -> Turn Windows Features on or off.*  Scroll to the bottom of the list and you should see Windows Sandbox in the list, tick this and go to OK.

```PowerShell
# You will need the RSAT tools installed on your machine for this 
# https://www.microsoft.com/en-au/download/details.aspx?id=45520

Enable-WindowsOptionalFeature -Online -FeatureName "Containers-DisposableClientVM"
```


## So why do I need Windows Sandbox






