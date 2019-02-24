+++
author = "Matt Browne"
categories = [""]
date = "2018-12-27"
description = "Step by step run through of how to create a build of the Hugo blog in Azure DevOps from a GitHub Repo"
featured = "buildit.jpg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "Part III - Creating a Build With Azure DevOps Pipelines"
tags = ["Azure DevOps", "Blog Series - BlogAsCode"]
type = "post"
draft = "false"
+++

---
This is part of a blog series titled "Creating and Deploying a Static Website with Azure DevOps Pipelines":

* [Part I - Installing and Creating a Static Website with Hugo](/blog/part-i-installing-and-creating-a-static-website-with-hugo/)

* [Part II - Creating a New App Service in Azure](/blog/part-ii-creating-a-new-app-service-in-azure/)

* [Part III - Creating a Build With Azure DevOps Pipelines](/blog/part-iii-creating-a-build-with-azure-devops-pipelines/)

* [Part IV - Creating a Release with Azure DevOps Pipelines](/blog/part-iv-creating-a-release-with-azure-devops-pipelines/)


---


Now that we have a Hugo site built and the Azure Web App spun up and ready to go, the next step is to look at Azure DevOps Pipelines and create an automated build of the site.

Firstly you are going to need the following two items:

* Go to https://devops.azure.com and [create an 'organisation'](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/create-organization?view=vsts) if you don't have one already.  It's very simple, so I'm not going to run through that here.
* Your Hugo site needs to be in its own GitHub Repo.  This is where the  Azure DevOps (ADO) build will be triggered from and where Hugo gets all the config from etc.  This will need to be the full Hugo directory from the build and not just the 'public' directory.

## Create a New Project

In your new organisation, click on the 'New Project' button, fill in the project name, set it as Public and click Create.

![App Service Plan Config](/img/2018/12/AzureDevOps_Build_01.png "App Service Plan Config")


## Create a New Build

Now you have everything you need to create your build, go to Pipelines on the left, then click the New Pipeline button.  On the wizard, select the options as follows:

1. Location - Click on the 'Use the Visual Designer' link.

2. Select the Repos that you are using, and the branch it's going to pull from.

3. Template - Select 'Empty Job' at the top of the selection.  We will fill it out later.

4. Save - Click on the 'Save & queue' selection box at the top and select 'Save'.


![App Service Plan Config](/img/2018/12/AzureDevOps_Build_02.gif "App Service Plan Config")

## Configure the New Build

Now we have a build, it just needs some configuration....

* Make sure that 'Pipeline' is selected on the left part of the config screen.  Look for the 'Agent Pool' drop-down and select 'Windows Container'.

* Select 'Get Sources' on the left and check through the config.  This has already been selected in a previous step, so there shouldn't be anything to change here.

* Select 'Agent Job' and git the plus symbol.  Type Hugo into the search box that appears on the right and hit return.  You will now see the Hugo extension available from the marketplace.  Just click on the 'Get it Free' option and it will take you to the marketplace to install it.  Run through this until it takes you back to the organisation.

* Go back to the original browser tab for the config (the marketplace opens a new tab).  Click on refresh on the right and search for Hugo again.

* Now you should have two options in the list for Hugo.  Select the top one and click on add.  This should make a new stage appear on the left under the 'Agent Job 1' stage.

* Now we need to fill in a few details for Hugo to understand what it is building.  Use these settings to fill in the blanks:

```
# My hugo site is in a subdir called 'blog', you may not need this.
Source = $(Build.SourcesDirectory)/blog

# This should be the same for everyone
Destination = $(Build.ArtifactStagingDirectory)

# This is the URL from the Azure Web App we created.
Base URL = https://mb-blog-demo.azurewebsites.net
```

* Finally, we just need to publish the artifact by clicking on the plus symbol next to the 'Agent Job 1' stage and searching for 'publish build artifacts'.  The config here should be left as default.
* Click on the 'Save & queue' drop down and select 'Save & queue', then you are done.





