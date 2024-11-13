# Snippets

## 1. Combine Multiple Text Files into a Single File

This script searches for all .txt files in a given directory (C:\tmp) and any of its subdirectories. 
It reads the content of each file and outputs the combined content into a single file (result.txt) on the user’s Desktop. 
The -NoClobber parameter ensures that result.txt is not overwritten if it already exists.

``` powershell
$directory = "C:\tmp"
$resultFile = $env:USERPROFILE + "\Desktop\result.txt"
Get-ChildItem -Path $directory -Include *.txt -Recurse | Get-Content | Out-File -FilePath $resultFile -NoClobber
```
