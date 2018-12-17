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


## Adding a Theme to your Site
The first thing we need to do is grab a theme from the Hugo site and put it in the themes directory.  
* Go to https://themes.gohugo.io/ and select a theme you would like.  I am using [Future Imperfect](https://themes.gohugo.io/future-imperfect/) in this example.  
* On the page for the theme there will be a download button that will take you to the GutHub page for the theme. 
* From there click on the 'Clone or Download' button and Download the ZIP. 
* Extract/Open the ZIP file and copy everything, apart from the .github  directory to your themes directory in the new site file structure.
* The path to my theme is now "C:\Hugo\blog\themes\hugo-future-imperfect-master" 

## Applying a Config for the Site

Now you theme is in place you will need to add some bits to the config file for the site so that it can use the theme.  

If you look at the theme files you copied over, there is an exampleSite directory with some examples that you can copy.  In there copy the config.toml file and paste it to the root of your new site.  In my case this is at **C:\Hugo\blog**.  I'm not going to go into detail [about the config file](https://gohugo.io/getting-started/configuration/) but take a look and you can edit things like the title to configure the site the way you want.


## Create your first page for the site

The site now has a theme and config setup, you just need to add your first page.

In the PowerShell window, make sure you are at the root of the new site (C:\hugo\blog in my case) and type the following:

```PowerShell
hugo new posts/my_first_blog_post.md
```

This will create a single markdown file in the /content/posts directory.  You can then go to the file and use it as a template for your first post to the site.  Just edit it with the content you want, using markdown and this is what Hugo will use to create the page.  Notice the "draft: true" in the frontmatter section of the file.  This will mean that the page won't be shown to start with but there is a way we can see these, more on this later.

## Build the Site and Inspect the Output

The last thing we need to do is build the site and take a look at what it outputs for us.  To do this, just type 'Hugo' into the command line at the root of the blog.  Hugo will now use the post markdown file, and the template to build the site.  We should get an output something like this:


![Building the site](/img/2018/12/Hugo_3.png)

Once this is complete, it normally take a few milliseconds, you should have bunch of file in the 'C:\Hugo\blog\public' directory.  This is our static site which can be copied to a web server or host to serve.  It's as simple as that ;)

## Testing the site.

One of the great features of Hugo is that it can serve the pages on your local machine to test them.  To do this run:
```
hugo server -D
```
Now you can browse to http://localhost:1313/ and you will see your newly created site, Complete with your new post that you created.

