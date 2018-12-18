+++
author = "Matt Browne"
categories = [""]
date = ""
description = ""
featured = "rougecafe.jpg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "Part II - Creating a Web App in Azure "
tags = [""]
type = "post"
draft = "true"
+++

Once you have a site to created with Hugo, or any other static site generator for that matter, you will need somewhere to host it.  In this post we are going to create a new Azure App Service on the free tier to host the site.

## Stage 1 - Create the App Service Plan

Before we create an App Service, we are going to need an App Service Plan to put it in.

In the Azure Portal, click on 'All Services' at the top left of the page and search for 'App Service Plan'.  Click on the only item that appears and click the '+ Add' button to start creating the plan

![App Service Plan Config](/img/2018/12/AppServicePlan_01.png)

Add the details like the name and resource group you want it in, and at the bottom of the blade notice that it defaults to the 'S1 Standard' pricing tier.  Click on this as we are going to need to change it to the free version for this demo.

![App Service Plan Config](/img/2018/12/AppServicePlan_02.png)

Click on 'Dev / Test', select the F1 plan (ie the free one) and click 'Apply'.  Once you are back at the blade with all the details click 'Create' and you new App Service Plan will start creating.  It only takes a few seconds normally.

## Stage 2 - Create the App Service

Now that we have the App Service Plan created, we can get to creating the App Service itself.  As before go to the Azure Portal, then All Services and search for 'App Service'.  You will get a few more options this time so click on the one just called 'App Services'.

Click on '+ Add' button and it will take you to the marketplace where you need to select 'Web App' (normally the first one in the list).  On the Web App page that appear, click the 'Create' button at the bottom.

From here you should see the Web App blade that you need to put the details into.

![App Service Plan Config](/img/2018/12/AppServicePlan_03.png)

Just put in the name and the Resource Group you wish to use and Select the App Service you have just created.  All that is left then is to click create.

