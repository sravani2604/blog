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

This should produce a directory structure that looks like this:

![Base directory structure](/img/2018/12/Hugo_2.png)

The first thing we need to do is grab a theme from the Hugo site and put it in the themes directory.  
* Go to https://themes.gohugo.io/ and select a theme you would like.  I am using [Future Imperfect](https://themes.gohugo.io/future-imperfect/) in this example.  
* On the page for the theme there will be a download button that will take you to the GutHub page for the theme. 
* From there click on the 'Clone or Download' button and Download the ZIP. 
* Extract/Open the ZIP file and copy everything, apart from the .github  directory to your themes directory in the new site file structure.
* The path to my theme is now "C:\Hugo\blog\themes\hugo-future-imperfect-master" 


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
