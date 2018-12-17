+++
author = "Matt Browne"
categories = [""]
date = "1900-12-31"
description = ""
featured = "pipes.jpeg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "Installing and Creating a Static Website with Hugo"
tags = ["default"]
type = "post"
draft = "true"
+++

## Installing Hugo on a Windows Machine

The first thing is to make sure you have Chocolatey Installed.  I know if is a little off topic, but it makes it so easy to install Hugo that it's worth doing. Take a look at [this page](https://chocolatey.org/install) if you are having issues or want to learn more.

To do this run the following line in an elevated PowerShell prompt:


```PowerShell
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

From there, just run the following line to get Hugo installed:

```PowerShell
choco install hugo -confirm
```

## Creating a New Site with Hugo

Now that you have Hugo installed we need to create the blank site to build up.  I have create a directory called 'C:\Hugo' to create everything in.

Open a new PowerShell prompt and navigate to the new Hugo folder.  Then simply type the following to create a new site called 'blog'.  You can call it anything you like but I am starting with a new blog.

```PowerShell
hugo new site blog
```

![Creating a New Site](/img/2018/12/Hugo_1.gif)

This should produce a directory struct that looks like this:

![Base directory structure](/img/2018/12/Hugo_2.gif)


https://themes.gohugo.io/




# Section 1
## Sub-Section 1

[some words](http://google.com)

[I'm an inline-style link with title - Markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet "Google's Homepage")

![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Image")


```PowerShell
#A PowerShell code block
Get-Service
Get-AzureRMVM 
```
