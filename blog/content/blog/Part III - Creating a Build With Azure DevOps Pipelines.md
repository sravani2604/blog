+++
author = "Matt Browne"
categories = [""]
date = "2018-12-18"
description = "Step by step run through of how to create a build of the Hugo blog in Azure DevOps from a GitHub Repo"
featured = "buildit.jpg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "Part III - Creating a Build With Azure DevOps Pipelines"
tags = [""]
type = "post"
draft = "true"
+++

Now that we have a Hugo site built and the Azure Web App spun up and ready to go, the next step is to look at Azure DevOps Pipelines and create an automated build of the site.

---
This is some text

about something

or another

---

Firstly you are going to need the following two item:

* Go to https://devops.azure.com and [create an 'organisation'](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/create-organization?view=vsts) if you don't have one already.  It's very simple, so I'm not going to run through that here.
* Your Hugo site needs to be in it's own GitHub Repo.  This is where the  Azure DevOps (ADO) build will be triggered from and where Hugo gets all the config from etc.  This will need to be the full Hugo directory from the build and not just the 'public' directory.

## Create a New Project

In your new organisation, click on the 'New Project' button, fill in the project name, set it as Public and click Create.

![App Service Plan Config](/img/2018/12/AzureDevOps_Build_01.png)

Now you have everything you need to create you build, so goto Pipelines on the left, then click the New Pipeline button.  On the wizard, select the options as follows:
1. Choose your Repos.  I am using GitHub for this but Azure Repos and just as good.
2. Select the Repos



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