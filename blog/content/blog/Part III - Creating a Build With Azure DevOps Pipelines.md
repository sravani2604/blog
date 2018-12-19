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

Now you have everything you need to create you build, go to Pipelines on the left, then click the New Pipeline button.  On the wizard, select the options as follows:
1. Location - Click on the 'Use the Visual Designer' link.
2. Select the Repos that you are using, and the branch it's going to pull from.
3. Template - Select 'Empty Job' at the top of the selection.  We will fill it out later.
4. Save - Click on the 'Save & queue' selection box at the top and select 'Save'.

![App Service Plan Config](/img/2018/12/AzureDevOps_Build_02.gif)

Now we have a build, it just needs some configuration....
* Make sure that 'Pipeline' is selected on the left part of the config screen/  Look for the 'Agent Pool' dropdown and select 'Windows Container'.
* Select 'Get Sources' on the left and check through the config.  This has already been selected in a previous step, so there shouldn't be anything to change here.
* Select 'Agent Job' and git the plus symbol.  Type Hugo into the search box that appears on the right and hit return.  You will now see the Hugo extension available from the marketplace.  Just click on the 'Get it Free' option and it will take you to the marketplace to install it.  Run through this until it takes you back to the organisation.
* Go back to the original browser tab for the config (the marketplace opens a new tab).  Click on refresh on the right and search for Hugo again



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