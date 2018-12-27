+++
author = "Matt Browne"
categories = [""]
date = "2018-12-18"
description = ""
featured = "blocks.jpg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "Part IV - Creating a Release with Azure DevOps Pipelines"
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

Now that we have a build configured in Azure DevOps, and it is outputting the files for the site as an artifact, the next stage is to create a release.  This will take the files and deploy them to the Azure Web App we configured before.

## Create the Release

* Firstly go to https://devops.azure.com and click on 'Pipelines', 'Releases' and then click on the 'New Pipeline' button.

* You will be asked to select a template for the release.  Just click on 'Azure App Service deployment' and click 'Apply'.  Leave the name as 'Stage 1' and close the 'Stage' box.

![Configuring the release](/img/2018/12/AzureDevOps_Release_01.gif)

## Configure the Artifact

* To add the artifact to your release (ie the built Hugo site) click on the 'Add an Artifact' box on the left-hand side of the config window.  In there select a source from the drop-down, this is the build that you previously configured.

* Change the 'Default version' selection to the latest, because we want this to deploy the version that has just built.

* Click on 'Add' to save the configuration.

* Finally, we need to configure the 'Continuous Deployment Trigger' by clicking on the lightning icon at the top of the artifact item and enabling it.  The will cause it to trigger the release every time there is a new build.  Save this by closing the box with the X at the top right.

![Configuring the release](/img/2018/12/AzureDevOps_Release_03.gif)

## Configure the Stages

* Now that you have the artifact configured you need to configure the 'Stages' by clicking on the '1 job, 1 task' link.

* In the 'Stage 1' config select the subscription (you may need to authorise this), then select the 'App service name' as the app service you created previously.
* There is nothing that you need to configure on the 'Run on agent' stage.

* Click on the 'Deploy Azure App Service' item and scroll down to the 'Package on folder' item.  This should read "$(System.DefaultWorkingDirectory)/_Hugo Blog Demo-CI/drop".  This is the build name with the artifact folder after it.

* Now you are done, so click on 'Save' towards the top.

![Configuring the release](/img/2018/12/AzureDevOps_Release_04.gif)

## Testing it all Works

To test that it all works you just need to trigger a build and it will all automatically run through.

We do this by going to 'Pipelines', 'Builds' and click the 'Queue' button on the top right of the page.  This will create a new item in the list that you can click on and follow the progress through.  Once the build is done click on the release and you can follow that through also.

![Configuring the release](/img/2018/12/AzureDevOps_Release_05.gif)

Now we have a shiny new website deployed to the Azure Web App

![Configuring the release](/img/2018/12/AzureDevOps_Release_06.png)
