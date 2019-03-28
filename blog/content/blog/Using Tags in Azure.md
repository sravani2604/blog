+++
author = "Matt Browne"
categories = [""]
date = "2019-03-27"
description = "How and why we use Tags in Azure, why they are so useful"
featured = "pipes.jpeg"
featuredalt = ""
featuredpath = "date"
linktitle = "Using Tags in Azure"
title = "Using Tags in Azure"
tags = [""]
type = "post"
draft = "true"
+++


Tags are a really simple feature in Azure and if you've spent any time in the portal then you will probably have noticed them.  They are essential a set of key value pairs that are assigned to the machine to 'tag' them in some way.

![Tags in the Azure Console](/img/2019/03/Tags01.jpg "What tags look like in the console")

These tags free form, so you can add just about anything you like (within limits), and if a tag doesn't already exist you can just type away and save the new tag.

# Searching and Filtering using Tags

One of the simplest ways to use Azure Tags is simply for searching for objects, much like you would use Resource Groups to group things together, but this can span many groups or environments etc.  To demonstrate this, give something a tag and go to "All Resources" in the Portal.  Click on the "Edit columns" button at the top of the resources and add the 'Tags' column.  

![Filtering by Tags](/img/2019/03/Tags02.jpg "We can filter All Resources using Tags")

In this example I can use the tags to see all the resources associated with my blog.  So this could be the Azure SQL DB and the App Service etc.  It doesn't have to be tied to the same Resource Group or object either.

# Cost Management using Tags

Tags come in handy when we are looking at the bill too.  Once you have tagged your resources, go to "View my Bill" and click on "Cost Analysis".  This will show you the total cost and some nice doughnut charts for Resource Group costs etc, but up the top of the page is a "Group by" filter where you can select Tags.

![Sorting the Bill by Tags](/img/2019/03/Tags02.jpg "We can filter the bill using Tags too!")

This information doesn't appear straight away.  It can take a few days to filter through, but once you the tags setup then you don't have to touch it until you add more resources.

*Side Note* - I hadn't realised how cheap my blog was.  Feel free to link to it to make it more expensive ;)

# Tagging with PowerShell

Of course we can tag things with PowerShell! 

To find the tags that are assigned to resources is pretty simple using 'Get-AzResource', so I'm not going to go over that but these are some examples to give you an idea....

```PowerShell
# Get a list of resources and the tags assigned.
Get-AzResource | Select-Object ResourceName, Tags

# List resources with a specific tag
Get-AzResource -Tag @{Blog="Dev"}

# List resources with NO tag assigned
Get-AzResource -Tag @{}

# Get all resoures with a specifi tag name (with any value)
Get-AzResource -TagName Blog
```

This will add resources to a resource @@@@@
```PowerShell
Get-AzResource -Name dc01 | Set-AzResource -Tag @{Test="001"} -Force
```

This will add tags to a resource @@@@
```Powershell
$resource = Get-AzResource -Name dc01
$resource.Tags.add("CostCode","ABC123") 
Get-AzResource -Name DC01 | Set-AzResource -Tags $resource.Tags  
```

