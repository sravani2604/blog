+++
author = "Matt Browne"
categories = [""]
date = "2019-03-27"
description = "How and why we use Azure Tags, why they are so useful"
featured = "pipes.jpeg"
featuredalt = ""
featuredpath = "date"
linktitle = "Using Tags in Azure"
title = "Using Tags in Azure"
tags = ["Tags", "Azure", "Cost Management"]
type = "post"
draft = "true"
+++


Tags are a really simple feature in Azure, and are amazingingly useful. If you've spent any time in the portal then you will probably have noticed them.  They are essential a set of key value pairs that are assigned to the machine to 'tag' them in some way.

![Tags in the Azure Console](/img/2019/03/Tags01.jpg "What tags look like in the console")

These tags are free form text, so you can add just about anything you like (within limits). If a tag doesn't already exist, you can just type away and save the new tag.

# Searching and Filtering using Tags

One of the simplest ways to use Azure Tags is for searching. Much like you use Resource Groups to group things together, but tags can span many groups or environments etc.  To demonstrate this, give something a tag and go to "All Resources" in the Portal.  Click on the "Edit columns" button at the top of the resources and add the 'Tags' column.  

![Filtering by Tags](/img/2019/03/Tags02.jpg "We can filter All Resources using Tags")

In this example we can use the tags to see all the resources associated with my blog.  This could be the Azure SQL DB and the App Service etc.  It doesn't have to be tied to the same Resource Group or object either.

# Cost Management using Tags

Tags come in handy when we are looking at the bill too.  Once you have tagged your resources, go to "View my Bill" and click on "Cost Analysis".  This will show you the total cost and some nice doughnut charts for Resource Group costs etc.  On the top of the page there is a "Group by" filter where you can select Tags.

![Sorting the Bill by Tags](/img/2019/03/Tags03.jpg "We can filter the bill using Tags too!")

This information doesn't appear straight away.  It can take a few days to filter through, but once the tag is setup, you don't have to touch it until you add more resources.

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

# Get all resoures with a specific tag name (with any value)
Get-AzResource -TagName Blog
```

This will add a tag to a resource.  However it will over write an tags that are already applied.
```PowerShell
Get-AzResource -Name dc01 | Set-AzResource -Tag @{Test="001"} -Force
```

If we want to add tags to the resource, and preserve the existing tags, then try.....
```Powershell
$resource = Get-AzResource -Name dc01
$resource.Tags.add("CostCode","ABC123") 
Get-AzResource -Name DC01 | Set-AzResource -Tags $resource.Tags  
```

# Tag Limits

One thing to be aware of, is the limits on tags.  You are limited by things like the number of tags per resource, or the length of tags.

- 50 = Max number of tags per resource 
- 512 = Max characters for the tag name (128 for strage accounts)
- 256 = Max characters for the tag value (256 for storage accounts)
- Not all resources support tags!  Most do though.  See [HERE](https://docs.microsoft.com/en-us/azure/azure-resource-manager/tag-support) for the Microsoft doc listing which ones do/don't.
- Avoid special character.  Stick to simple alphanumerics.

# Summary
Tags are simple but really usefull.  It's worth tagging everything you create with a something.  Even if you change this in the future, you will be able to identify and bill the items easier.

