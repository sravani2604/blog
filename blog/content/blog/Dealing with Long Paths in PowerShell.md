+++
author = "Matt Browne"
categories = [""]
date = "2019-01-10"
description = ""
featured = "pipes.jpeg"
featuredalt = ""
featuredpath = "date"
linktitle = ""
title = "Dealing with Long Paths in PowerShell"
tags = [""]
type = "post"
draft = "true"
+++

*Boss : Can you get me a list of all the files on these shares?*

*Me : Sure that’s super easy.*

```PowerShell
Get-Childitem -path “\\server\sharename” -recurse
```

Ah ok, so this share has some really long paths.  This causes a lot of errors if the paths are over 260 characters, which is gong to be pretty normal on a lot of file servers.  No problem though because we can use the Unicode version of the path….

To use the Unicode version of the path we need to replace the double slash at the beginning of the UNC path with ‘\\?\UNC\’

 
So \\server\sharename becomes -> \\?\UNC\server\sharename
 

If we want to use this with the get-childitem cmdlet, we are going to need to use the -literalpath variable so that non of the characters are interpreted as wildcards or special character.  I.e. it take the path exactly as it is specified.  So, our command now becomes :

```PowerShell
Get-Childitem -literalpath "\\?\UNC\server\sharename" -recurse
```

Great, so now we can put the UNC path the boss has given us and just use ‘-replace’ to put the new beginning on the path.  Something like this:

``` PowerShell
$share -replace “\\”, “\\?\UNC\”
```
![Long File Paths](/img/2019/01/LonFilePaths01.png)
 

OK, so that hasn’t gone well.  That UNC path is very broken now!  This is because it’s interpreting the slashes as escape characters.  Luckily we can get around this by using the [regex]::escape method.  This will make the command interpret all the characters exactly as they are and not see them as escape characters.

So now we have this :

```PowerShell
$share -replace [regex]::escape("\\"), "\\?\UNC\"
```
![Long File Paths](/img/2019/01/LonFilePaths01.png)

Bingo!  That looks perfect.

Now we have everything put together, we can creat a simple function that will take in the UNC path and output the list of file just like the boss asked.

 

```PowerShell
function Get-ListOfFiles ($path) {
    $share -replace [regex]::escape("\\"), "\\?\UNC\"
    Get-Childitem -path $share -Recurse | Where-Object {$_.Extension -like ".*"}      
}
```



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