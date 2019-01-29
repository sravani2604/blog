+++
author = "Matt Browne"
categories = [""]
date = "2019-01-26"
description = ""
featured = "keyboard.jpg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "Dealing with Long Paths in PowerShell"
tags = ["PowerShell, Get-Childitem"]
type = "post"
draft = "false"
+++

*Boss : Can you get me a list of all the files on these shares?*

*Me : Sure that’s super easy.*

Often these simple conversations seems like they should take 2 minutes of our time but the reality is that there is often something that catches us out.  We've all been there right!  This is a simple example of that, but once we know the issues there are a few simple fixes that get us to the goal without too much of a drama.

This is where we start the journey

```PowerShell
Get-Childitem -path "\\server\sharename" -recurse
```

Ah ok, so this share has some really long paths.  This causes a lot of errors if the paths are over 260 characters, which is going to be pretty normal on a lot of file servers.  No problem though because we can use the Unicode version of the path.

To use the Unicode version of the path we need to replace the double slash at the beginning of the UNC path with ‘\\?\UNC\’

 
So 
```
\\server\sharename becomes -> \\?\UNC\server\sharename
``` 

If we want to use this with the Get-ChildItem cmdlet, we are going to need to use the -literalpath variable so that none of the characters aren't interpreted as wildcards or special characters.  I.e. it takes the path exactly as it is specified.  So, our command now becomes :

```PowerShell
Get-Childitem -literalpath "\\?\UNC\server\sharename" -recurse
```

Great, so now we can put the UNC path the boss has given us and just use ‘-replace’ to put the new beginning on the path.  Something like this:

``` PowerShell
$share -replace "\\", "\\?\UNC\"
```
![Long File Paths](/img/2019/01/LonFilePaths01.png)
 

OK, so that hasn’t gone well.  That UNC path is very broken now!  This is because it’s interpreting the slashes as escape characters.  Luckily we can get around this by using the [regex]::escape method.  This will make the command interpret all the characters exactly as they are and not see them as escape characters.

So now we have this :

```PowerShell
$share -replace [regex]::escape("\\"), "\\?\UNC\"
```
![Long File Paths](/img/2019/01/LonFilePaths02.png)

Bingo!  That looks perfect.

Now we have everything put together, we can create a simple function that will take in the UNC path and output the list of files just like the boss asked.
 

```PowerShell
function Get-ListOfFiles ($path) {
    $share = $share -replace [regex]::escape("\\"), "\\?\UNC\"
    Get-Childitem -path $share -Recurse | Where-Object {$_.Extension -like ".*"}      
}
```


(Edit) Side note - See [@RSiddaway's](https://twitter.com/rsiddaway) [latest blog](https://richardspowershellblog.wordpress.com/2019/01/25/ntfssecurity-module/) about the NTFSsecurity module on github that deals with long file paths.