+++
author = "@MattBrowne"
categories = [""]
date = "2019-01-05"
description = "What is it, why do I care, and how do I get it?"
featured = "sandbox.jpg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "What is Windows Sandbox"
tags = [""]
type = "post"
draft = "true"
+++

*Note - If you just want to know how to get Sandbox, skip to the second half of the post.*

## What is Windows Sandbox

Windows Sandbox is a lot like running a virtual machine in Windows 10 in some ways but not in others.  When you spin it up, ie click on the icon, a window opens with a vanilla version of Win10 running.  It's using the Windows Container technology to run the OS, so it's using the files on the machine to run but it can't change them at all.  Therefore it's got all the features of your machine but it can't break anything outside of it's own little 'sandbox'.  It's not going to be as fast or as feature rich as a full VM, but as a temporary space to test/break/prove something, its perfect.  And it does all of this in about 100mb of disk space.

![Initial view](/img/2019/01/WindowsSandbox_02.jpg)

However, **nothing survives a restart**.  This is where it starts to feel different from running a VM.  It's designed as something you can use to blow things up and test, not as a tool to run things in the long term (or even medium term).  Therefore get yourself some good automation scripts for installing the software you need before testing, this will save you a whole load of time.

It's being mentioned as a tool for testing things like suspect files and viruses, which it is, but I think it goes further than that.  This is a space where you can test software, test scripts or even just test Windows 10 settings.  **It kills the 'works on my machine' statement** because now you can run it on a vanilla machine without all the tools we have installed, and without all the corporate settings etc.

## What it's not!

We've covered the 'nothing survives a restart' feature so.....

It's not finished or polished software yet, but hey we are running preview software so that is a given right.  There have been various posts about the issue with it failing out of the box, [see the post from the Register on how to fix that] (https://www.theregister.co.uk/2019/01/03/windows_10_sandbox/), and I'm getting errors when I restart the Sandbox OS.

![Unexpected Error](/img/2019/01/WindowsSandbox_02.jpg)

It's not fast.  I'm not saying it's annoyingly slow or unusable but it's just not going to be a super snappy beast.  Actually, it works pretty well on my slightly underpowered test machine.



## What do I need to run it

* You need Windows 10 Pro or Enterprise x64
* You need to be running Windows 10 build 18305 or higher
* On physical machines, you need virtualisation turned on in the BIOS.
* On a virtual machines, you need to enable 'Nested Virtualisation' 
* At least 4Gb RAM
* At least 2 Cores
* [Read this post from the Verge about removing the update that breaks it](https://www.theregister.co.uk/2019/01/03/windows_10_sandbox/)


## How do I get Windows Sandbox

On your Windows 10 machine go to *Settings -> Apps -> Apps & Features -> Programs and Features -> Turn Windows Features on or off.*  Scroll to the bottom of the list and you should see Windows Sandbox in the list, tick this and go to OK.

```PowerShell
# You will need the RSAT tools installed on your machine for this 
# https://www.microsoft.com/en-au/download/details.aspx?id=45520

Enable-WindowsOptionalFeature -Online -FeatureName "Containers-DisposableClientVM"
```


If you want more detail on the features and tech involved, then take a look at [the post over on the MS Tech community](https://techcommunity.microsoft.com/t5/Windows-Kernel-Internals/Windows-Sandbox/ba-p/301849).

What do you think?  
If you have a use for it that I haven't spotted or you love/hate it for some reason, then [tweet your thoughts at me](https://twitter.com/mattbrowne)









