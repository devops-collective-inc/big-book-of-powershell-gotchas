# Getting Folder Sizes

Folks often ask how to use PowerShell to get the size of a folder, such as a user home folder.

Problem is, _folders don't have a size. _Windows literally doesn't track size for folder objects. A folder's "size" is merely the sum of it's files' sizes. Which means you have to add them up.

```
Get-ChildItem -Path <whatever> -File -Recurse |
Measure-Object -Property Length -Sum
```

As one example. Bottom line, you need to get all the files, and add up their Length properties.

