+++
author = "Matt Browne"
categories = [""]
date = "2018-12-17"
description = ""
featured = "engine.jpg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "Blog Series - Creating and Deploying a Static Website with Azure DevOps Pipelines"
tags = [""]
type = "post"
draft = "true"
+++

This blog series all kicked of from a conversation I was having with [Adam Listek](https://twitter.com/alistek) a while back about using a static site generator for creating a blog.  He is a bit of a wizard with these things and put me on to [Hugo](https://gohugo.io/).  From the initial scan it looked like a simple way, once it's setup, to create a static site/blog from a few markdown file.  This got me thinking!

Hugo just creates the static files for the site, but they are going to need to be hosted somewhere, and Hugo needs to run every time I create a new post.  It started to feel like we needed a pipeline for this.  Enter [Azure DevOps](https://azure.microsoft.com/en-gb/services/devops/)!  This is free for Open Source projects, which is perfect because I was planning to put the 'code' in GitHub anyway.

The only missing part is somewhere to host the site, which can be done very cheaply (possibly even free) and easily with an Azure App Service.  It doesn't have to be in Azure of course, but it fits nicely with what I'm doing, and the good part with all this is that we can swap out the parts without too much of an issue.  The hosting, repo, build servers could all change in the future if needed.  Let's do it!

That's what this series of posts is all about. ie blog posts on how I created this blog (very meta hey!)

[Part I - Installing and Creating a Static Website with Hugo](/blog/part-i-installing-and-creating-a-static-website-with-hugo/)

[Part II - Creating a New App Service in Azure](/blog/part-ii-creating-a-new-app-service-in-azure/)

[Part III - Creating a Build With Azure DevOps Pipelines](/blog/part-iii-creating-a-build-with-azure-devops-pipelines/)

[Part IV - Creating a Release with Azure DevOps Pipelines](/blog/part-iv-creating-a-release-with-azure-devops-pipelines/)

