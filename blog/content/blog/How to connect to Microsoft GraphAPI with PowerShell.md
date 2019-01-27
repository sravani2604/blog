+++
author = "Matt Browne"
categories = [""]
date = "2019-01-27"
description = "Using a credentials file to connect to the GraphAPI"
featured = "Circuit.jpg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "How to connect to Microsoft GraphAPI with PowerShell"
tags = ["PowerShell, GraphAPI"]
type = "post"
draft = "true"
+++



Using the GraphAPI we can query data from just about any of the Microsoft 365 products.  So if we need to get a list of users or a list of devices in InTune this can all done done with Graph.  However it's a bit different from getting data from the console or from PowerShell, and has been difficult to automate in the past because we need to get an authentication token.  Thankfully Microsoft have created a set of example scripts to authenticate and run queries.

 

## Getting the PowerShell file for Authenticating

 

The example script that I'm going to use for this test is here:

 

https://github.com/microsoftgraph/powershell-intune-samples/blob/master/Authentication/Auth_From_File.ps1

 

This script will allow us to store credentials in a local file and get an authorisation token for running queries.

 

However, the script requires that you have the AzureAD PowerShell module installed.  If you don't already have this installed, you can run:

 

```PowerShell

Install-Module AzureAD

```

 

## Setting up the Credentials to use

 

If you read though the Auth_From_File.ps1, you will notice that there is a credential file referenced.  This an encrypted file that stores the password of the account you are going to use for authentication.  To create this we can use:

 

```PowerShell

read-host -assecurestring | convertfrom-securestring | out-file C:\cred.txt

```
 

This will create the file we need to reference in the script.  However, the file will only work on the machine that it created on, so make sure you create it on the machine where are going to run the script on.  There is nothing stopping you storing this file on a file share somewhere, or even in Azure Vault, but it just needs to be created on the target machine.
 

## Using the Script to Query the GraphAPI

 

Now that we have the credentials in a file, we need to go through the Auth_From_File.ps1 script and change the $User and $Password variables to reference the account we are using, and the password file we just created.

 

If we run the ps1 file we will have a token in the $authToken variable that we can use for connecting to the GraphAPI.  It should look something like this:

![Graph Explorer](/img/2019/01/GraphExplorer03.jpg)

 

Next we need to create an HTTP string to query the GraphAPI for the details we need.  For example if we need to get all users, we can send the following http get:


```

GET https://graph.microsoft.com/v1.0/users

```
This is fairly crude query but it will give us an idea of the results we will get from one of these queries.  Also it shows that we need to think about filtering our queries because a simple query like this can produce a LOT of results if you have a big environment.
 

When you need to build you own query, a good place to start is the Graph REST API v1.0 reference page on Microsoft Docs:

https://docs.microsoft.com/en-us/graph/api/overview?view=graph-rest-1.0


Now that we have a simple uri for our query, we can use 'Invoke-RestMethod' like this:
 

```PowerShell

$uri = "https://graph.microsoft.com/v1.0/users"

$users = (Invoke-RestMethod -Uri $uri -Headers $authToken -Method Get).Value

```
 

If you run this, you will get a stream of all the user details you have in your subscription.  Warning, this could take a while is you have a large estate ;)
 

## Filtering the queries


If we want to filter the search down a little we can add some query parameters to the URI using the following pattern:


```

https://graph.microsoft.com/beta/{resource}?[query_parameters]

```

 

So if we want to query all the users that have a givenName starting with M then we can do this for example:

 

$uri = "https://graph.microsoft.com/v1.0/users/?$filter=startswith(givenName,'M')"

 

To get more detail on the filters, refer to the documentation mentioned above.

 

For testing on the queries go over to Graph Explorer (https://developer.microsoft.com/en-us/graph/graph-explorer).  This gives us a page to enter the queries and will show the results that it returns.  This can be invaluable when test etc.  Just build up you query from the documentation and put it in here and we can tell if we have got the format right before committing it to code etc.  This can be a quick easy way of running a query if you are doing a one off etc.

 
![Graph Explorer](/img/2019/01/GraphExplorer01.jpg)
 
SO, that's it.  You now have the script and credentials to query the GraphAPI with PowerShell.  Nothing is stopping you from scheduling this script to produce reports or notification etc.  
 