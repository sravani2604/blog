+++
author = "Matt Browne"
categories = [""]
date = ""
description = ""
featured = "pipes.jpeg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "Running PowerShell in a Windows Container on Windows 10"
tags = [""]
type = "post"
draft = "true"
+++

Ok, so this is a little niche I admit it but stick with me, there is some value in this.  This came about because I needed to run a PowerShell script on a box with particular version on some modules and tools without messing with what was already on there.  This is where containers come in....

# Installing Docker on Windows 10

You will need to be running Windows 10 Pro or Enterprise, 1607 or later.
You will need the Hyper-V feature enabled.  Just run this in a elevated PowerShell window....

```PowerShell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

Download and Install Docker CE.  You will need to sign up for a Docker account and the [install instructions can be found here](https://docs.docker.com/docker-for-windows/install/#install-docker-desktop-for-windows-desktop-app "Install Docker Desktop for Windows desktop app")

Once it's installed we have docker installed we need to switch it over to using Windows Containers (it will default to Linux containers).  This can be done by right clicking on the Docker icon on the taskbar and selecting "Switch to Windows Containers"

![Switching to Windows Containers](/img/2019/03/windowsContainers01.jpg "Swiching to Windows Containers")

# Creating the first Windows Container

Now that we have the Docker installed and running we need to get a container to run ......

```
docker pull mcr.microsoft.com/windows/nanoserver
```
This will pull the latest version of the Windows Nano Server from Microsoft.

![Downloading Windows Container](/img/2019/03/windowsContainers02.jpg "Downloading Windows Container")

Once this is finished you should get



# Section 1
## Sub-Section 1

[I'm an inline-style link with title - Markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet "Google's Homepage")

![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Image")


```PowerShell
#A PowerSHell code block
Get-Service
Get-AzureRMVM
```

# Link to the 