# PowerShell Tutorial

PowerShell is a powerful scripting language and automation framework developed by Microsoft. It is used for task automation, configuration management, and system administration. This guide covers everything from basic commands to advanced scripting techniques.

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
14. [Scripting Best Practices](#14-scripting-best-practices)
15. [Practical Examples](#15-practical-examples)

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

## 14. Scripting Best Practices

✔ Use descriptive variable names (`$userName` instead of `$x`).  
✔ Comment your code (`# This is a comment`).  
✔ Handle errors (`Try-Catch`).  
✔ Avoid hardcoding paths (use parameters).

## 15. Practical Examples

### Example 1: Backup Files

```powershell
$source = "C:\Data"
$destination = "D:\Backup"
Copy-Item $source $destination -Recurse
```

### Example 2: Monitor CPU Usage

```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 5
```

### Example 3: Bulk Rename Files

```powershell
Get-ChildItem *.txt | Rename-Item -NewName { $_.Name -replace ".txt", "_new.txt" }
```
