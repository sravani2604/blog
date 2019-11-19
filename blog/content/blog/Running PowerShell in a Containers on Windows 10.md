+++
author = "Matt Browne"
categories = [""]
date = ""
description = ""
featured = "pipes.jpeg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "Running PowerShell in a Containers on Windows 10"
tags = [""]
type = "post"
draft = "true"
+++

Ok, so this is a little niche I admit it but stick with me, there is some real value in this.  This came about because I needed to run a PowerShell script on a box with particular version on some modules and tools without messing with what was already on there.  This is where containers come in....

# Installing Docker on Windows 10

You will need to be running Windows 10 Pro or Enterprise, 1607 or later.
You will need the Hyper-V feature enabled.  Just run this in a elevated PowerShell window....

```PowerShell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

Download and Install Docker CE.  You will need to sign up for a Docker account and the [install instructions can be found here](https://docs.docker.com/docker-for-windows/install/#install-docker-desktop-for-windows-desktop-app "Install Docker Desktop for Windows desktop app")

Once we have docker installed, we need to switch it over to using Windows Containers (it will default to Linux containers).  This can be done by right clicking on the Docker icon on the taskbar and selecting "Switch to Windows Containers"

![Switching to Windows Containers](/img/2019/03/windowsContainers01.jpg "Swiching to Windows Containers")

# Creating the first Windows Container

Now that we have the Docker installed and running we need to get a container to run ......

```
docker pull mcr.microsoft.com/powershell
```
This will pull the latest version of the Windows Nano Server from Microsoft.

![Downloading Windows Container](/img/2019/03/windowsContainers02.jpg "Downloading Windows Container")

When the pull finishes, we will have a working container downloaded with PowerShell installed in it.  You can see all the docker containers you have on the system using *'docker images'*...

![First Windows Container](/img/2019/03/windowsContainers03.jpg "Nano Server Container")

Now all we need to do is run up the container and get it to run PowerShell within it.  We do this using 'docker run' with the '-i' parameter to make it interactive, like this....

```PowerShell
docker run -i mcr.microsoft.com/powershell powershell.exe 
```

Then, just to prove the point, if we run "Get-ComputerInfo" then we see that this is a Server Core installation and the hostname is different from the machine you are running it on.  So now we have a PowerShell install that is separate from the host  machine, so we can install any module we like and it will remain in that container. 

To start, stop or view the running containers, use the following commands....

```
docker run 
```



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