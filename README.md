# PowerShell Tutorial

## Table of Contents

1. [Introduction to PowerShell](#1-introduction-to-powershell)
2. [Setting Up PowerShell](#2-setting-up-powershell)
3. [Basic PowerShell Commands](#3-basic-powershell-commands)
4. [Variables and Data Types](#4-variables-and-data-types)
5. [Operators](#5-operators)
6. [Conditional Statements](#6-conditional-statements)
7. [Loops](#7-loops)
8. [Arrays and Hash Tables](#8-arrays-and-hash-tables)
9. [Functions](#9-functions)
10. [Error Handling](#10-error-handling)
11. [Working with Files and Folders](#11-working-with-files-and-folders)
12. [PowerShell Pipeline](#12-powershell-pipeline)
13. [Remote Management](#13-remote-management)
14. [Modules and Scripting](#14-modules-and-scripting)  
15. [Advanced Automation](#15-advanced-automation)  
16. [PowerShell in DevOps](#16-powershell-in-devops)  
17. [Security Best Practices](#17-security-best-practices)  
18. [Debugging and Optimization](#18-debugging-and-optimization)  
19. [Practical Scripting Examples](#19-practical-scripting-examples)  

## 1. Introduction to PowerShell

PowerShell is:

- A command-line shell for executing commands.
- A scripting language for automation.
- Built on .NET, allowing deep integration with Windows.
- Cross-platform (PowerShell Core works on Linux/macOS).

### Key Features

✔ Task automation  
✔ Object-oriented output (not just text)  
✔ Remote management  
✔ Extensible with modules

## 2. Setting Up PowerShell

### Installation

- Windows: Comes pre-installed (check with `$PSVersionTable`).
- Latest Version: Download from [Microsoft Docs](https://aka.ms/powershell).
- VS Code: Recommended for scripting (install the PowerShell extension).

### First Script

1. Open VS Code.
2. Create a file `hello.ps1`:
   ```powershell
   Write-Output "Hello, PowerShell!"
   ```
3. Run it:
   ```powershell
   .\hello.ps1
   ```

## 3. Basic PowerShell Commands

### Cmdlets (Command-Lets)

- Follow `Verb-Noun` format (e.g., `Get-Process`, `Stop-Service`).
- Common Verbs:
  - `Get` (retrieve data)
  - `Set` (modify settings)
  - `New` (create objects)
  - `Remove` (delete objects)

### Examples

```powershell
Get-Process              # List running processes
Get-Service              # List services
Get-ChildItem C:\        # List files/folders
Get-Help Get-Process     # Show help for a cmdlet
```

### Aliases

Shortcuts for cmdlets:

```powershell
ls          # Alias for Get-ChildItem
ps          # Alias for Get-Process
kill -name notepad  # Alias for Stop-Process
```

## 4. Variables and Data Types

### Declaring Variables

```powershell
$name = "John"
$age = 30
$isActive = $true
```

### Data Types

| Type      | Example              |
| --------- | -------------------- |
| String    | `"Hello"`            |
| Integer   | `42`                 |
| Boolean   | `$true`, `$false`    |
| Array     | `1, 2, 3`            |
| Hashtable | `@{ Key = "Value" }` |

### Type Casting

```powershell
[int]$number = "42"  # Converts string to integer
```

## 5. Operators

### Arithmetic Operators

```powershell
5 + 3    # Addition
10 - 4   # Subtraction
2 * 6    # Multiplication
8 / 2    # Division
10 % 3   # Modulus
```

### Comparison Operators

```powershell
5 -eq 5      # Equal
5 -ne 3      # Not equal
5 -gt 3      # Greater than
5 -lt 10     # Less than
"abc" -like "a*"  # Wildcard match
```

### Logical Operators

```powershell
($age -gt 18) -and ($name -eq "John")
($status -eq "Active") -or ($isAdmin)
```

## 6. Conditional Statements

### If-Else

```powershell
if ($age -lt 18) {
    Write-Output "Minor"
} elseif ($age -lt 60) {
    Write-Output "Adult"
} else {
    Write-Output "Senior"
}
```

### Switch Statement

```powershell
switch ($day) {
    "Monday"    { Write-Output "Start of week" }
    "Friday"    { Write-Output "Weekend soon!" }
    default     { Write-Output "Regular day" }
}
```

## 7. Loops

### For Loop

```powershell
for ($i = 1; $i -le 5; $i++) {
    Write-Output "Count: $i"
}
```

### While Loop

```powershell
$count = 1
while ($count -le 5) {
    Write-Output "Count: $count"
    $count++
}
```

### ForEach Loop

```powershell
$fruits = "Apple", "Banana", "Cherry"
foreach ($fruit in $fruits) {
    Write-Output "Fruit: $fruit"
}
```

## 8. Arrays and Hash Tables

### Arrays

```powershell
$numbers = 1, 2, 3
$numbers[0]        # First element (1)
$numbers += 4      # Add element
```

### Hash Tables (Dictionaries)

```powershell
$person = @{
    Name = "John"
    Age  = 30
}
$person["Name"]   # Access value
$person.Keys      # List all keys
```

## 9. Functions

### Basic Function

```powershell
function Greet($name) {
    Write-Output "Hello, $name!"
}
Greet "Alice"
```

### Advanced Function (With Parameters)

```powershell
function Add-Numbers {
    param (
        [int]$a,
        [int]$b
    )
    return $a + $b
}
Add-Numbers -a 5 -b 3
```

## 10. Error Handling

### Try-Catch-Finally

```powershell
try {
    Get-Content "nonexistent.txt" -ErrorAction Stop
}
catch {
    Write-Output "Error: $_"
}
finally {
    Write-Output "Cleanup done."
}
```

## 11. Working with Files and Folders

### Read a File

```powershell
Get-Content "C:\example.txt"
```

### Write to a File

```powershell
"Hello, World!" | Out-File "C:\output.txt"
```

### List Files in a Directory

```powershell
Get-ChildItem C:\ -Recurse | Where-Object { $_.Extension -eq ".txt" }
```

## 12. PowerShell Pipeline

Pass output from one cmdlet to another:

```powershell
Get-Process | Where-Object { $_.CPU -gt 50 } | Sort-Object CPU -Descending
```

## 13. Remote Management

### Enter a Remote Session

```powershell
Enter-PSSession -ComputerName "Server01"
```

### Run Commands Remotely

```powershell
Invoke-Command -ComputerName "Server01" -ScriptBlock { Get-Service }
```
## 14. Modules and Scripting  

### What are Modules?  
Modules are reusable PowerShell scripts that contain functions, cmdlets, and variables.  

#### List Installed Modules  
```powershell
Get-Module -ListAvailable
```

#### Import a Module  
```powershell
Import-Module ActiveDirectory
```

#### Create a Custom Module  
1. Create a `.psm1` file (e.g., `MyModule.psm1`).  
2. Define functions inside it.  
3. Import it:  
   ```powershell
   Import-Module .\MyModule.psm1
   ```


## 15. Advanced Automation  

### Scheduled Tasks  
Automate scripts using Task Scheduler:  
```powershell
$action = New-ScheduledTaskAction -Execute "PowerShell.exe" -Argument "-File C:\Scripts\Backup.ps1"
$trigger = New-ScheduledTaskTrigger -Daily -At "3:00 AM"
Register-ScheduledTask -TaskName "DailyBackup" -Action $action -Trigger $trigger
```

### Web Requests (REST API Calls)  
```powershell
$response = Invoke-RestMethod -Uri "https://api.example.com/data" -Method Get
$response | ConvertTo-Json
```

### Working with JSON  
```powershell
$json = '{"name": "John", "age": 30}' | ConvertFrom-Json
$json.name  # Output: John
```


## 16. PowerShell in DevOps  

### Azure Automation  
Manage Azure resources:  
```powershell
Connect-AzAccount
Get-AzVM
```

### Docker Integration  
```powershell
docker ps | ConvertFrom-Json | Select-Object ID, Names
```

### CI/CD with PowerShell  
Example Azure DevOps Pipeline:  
```yaml
steps:
- powershell: |
    Write-Host "Running PowerShell in CI/CD"
    ./Deploy.ps1
```


## 17. Security Best Practices  

### Execution Policy  
Restrict script execution:  
```powershell
Set-ExecutionPolicy RemoteSigned
```

### Secure Credentials  
```powershell
$cred = Get-Credential
$securePassword = ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force
```

### Logging and Auditing  
```powershell
Start-Transcript -Path "C:\Logs\ScriptLog.txt"
# Your script here
Stop-Transcript
```


## 18. Debugging and Optimization  

### Debugging Techniques  
- Breakpoints:  
  ```powershell
  Set-PSBreakpoint -Script .\Script.ps1 -Line 10
  ```
- Verbose Output:  
  ```powershell
  Write-Verbose "Debugging info" -Verbose
  ```

### Performance Optimization  
- Avoid `+=` with large arrays (use `ArrayList` instead).  
- Use `Where-Object` early in pipelines.  


## 19. Practical Scripting Examples  

### Example 1: Automated System Report  
```powershell
$report = @"
System Report----------
Date: $(Get-Date)
CPU: $(Get-WmiObject Win32_Processor | Select-Object -ExpandProperty LoadPercentage)%
Memory: $(Get-WmiObject Win32_OperatingSystem | Select-Object -ExpandProperty FreePhysicalMemory) MB free
"@
$report | Out-File "C:\Reports\SystemReport.txt"
```

### Example 2: Active Directory User Management  
```powershell
Import-Module ActiveDirectory
New-ADUser -Name "John Doe" -SamAccountName "jdoe" -Enabled $true
```

### Example 3: Bulk Image Resizing  
```powershell
Add-Type -AssemblyName System.Drawing
Get-ChildItem *.jpg | ForEach-Object {
    $img = [System.Drawing.Image]::FromFile($_.FullName)
    $newImg = $img.GetThumbnailImage(800, 600, $null, [IntPtr]::Zero)
    $newImg.Save("Resized_$($_.Name)")
}
```
