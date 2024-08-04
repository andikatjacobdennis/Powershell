## Introduction

This tutorial is designed to introduce software architects to PowerShell, covering both basic and advanced concepts. Through practical examples, you'll learn how to leverage PowerShell for system administration, automation, and scripting tasks.

### Introduction to PowerShell

### Module 0: Getting Started

#### What is PowerShell and PowerShell Versions

PowerShell is a task automation and configuration management framework from Microsoft, consisting of a command-line shell and the associated scripting language. It is built on the .NET framework and helps IT professionals and power users control and automate the administration of Windows operating systems and applications.

- **Versions**:
  - **Windows PowerShell**: Integrated into Windows, supports .NET Framework.
  - **PowerShell Core**: Cross-platform (Windows, macOS, Linux), supports .NET Core.
  - **PowerShell 7**: The latest version, combining the best features of Windows PowerShell and PowerShell Core.

#### Why PowerShell and Examples

PowerShell is favored for its powerful scripting capabilities, access to .NET libraries, and its ability to interact seamlessly with various system components.

**Example 1**: Automating User Creation in Active Directory
```powershell
Import-Module ActiveDirectory
New-ADUser -Name "John Doe" -GivenName "John" -Surname "Doe" -SamAccountName "jdoe" -UserPrincipalName "jdoe@domain.com" -Path "OU=Users,DC=domain,DC=com"
```

**Example 2**: Fetching System Information
```powershell
Get-ComputerInfo
```

#### Word of Note

PowerShell is a powerful tool that can make system administration more efficient. However, improper use can lead to significant issues, so it's crucial to understand the commands and scripts you run.

### Module 1: PowerShell Basics

#### Module 1 Introduction

In this module, you'll get acquainted with the fundamentals of PowerShell, including basic commands (cmdlets), syntax, and how to use the pipeline.

#### Getting to Know PowerShell

PowerShell cmdlets are the building blocks of scripts and automation tasks.

#### Cmdlets and Parameters - Examples with Get and Set

Cmdlets are lightweight commands used in the PowerShell environment. They follow a verb-noun naming pattern.

**Example 1**: Using `Get-Process`
```powershell
Get-Process
```

**Example 2**: Using `Set-Service`
```powershell
Set-Service -Name "wuauserv" -Status "Stopped"
```

#### Getting Help for PowerShell

Use the `Get-Help` cmdlet to find information about cmdlets and concepts in PowerShell.

**Example**:
```powershell
Get-Help Get-Process
```

#### Which Cmdlet Does the Job for You?

Use `Get-Command` to discover cmdlets.

**Example**:
```powershell
Get-Command -Verb Get
```

#### What Are Modules?

Modules are packages of cmdlets, functions, and other tools. Import modules to extend PowerShell's functionality.

**Example**:
```powershell
Import-Module ActiveDirectory
```

#### How Does the Pipeline Work?

The pipeline (`|`) passes the output of one cmdlet as input to another.

**Example**:
```powershell
Get-Process | Where-Object { $_.CPU -gt 100 }
```

#### Outputting to a Text File

Redirect output to a text file using `Out-File`.

**Example**:
```powershell
Get-Process | Out-File "processes.txt"
```

#### Parameters vs Properties

Parameters modify cmdlet behavior, while properties are attributes of objects returned by cmdlets.

#### Formatting Data in PowerShell

Use `Format-Table` or `Format-List` to format output.

**Example**:
```powershell
Get-Process | Format-Table -Property Name, CPU
```

#### PowerShell Objects: A Deeper Look

PowerShell is object-oriented. Each output from a cmdlet is an object with properties and methods.

#### Getting to Properties and Methods

Access properties using `.` notation.

**Example**:
```powershell
(Get-Process)[0].Name
```

#### What Kind of Properties Do We Have?

Properties can be simple data types (string, int) or complex objects.

#### What Kind of Parameters Do We Have?

Parameters can be mandatory, optional, positional, or named.

#### Using Where-Object to Filter Properties

**Example**:
```powershell
Get-Process | Where-Object { $_.CPU -gt 100 }
```

#### Select-Object for Outputting Specific Information

**Example**:
```powershell
Get-Process | Select-Object -Property Name, CPU
```

#### Sorting with Sort-Object

**Example**:
```powershell
Get-Process | Sort-Object -Property CPU -Descending
```

#### Outputting to CSV

**Example**:
```powershell
Get-Process | Export-Csv -Path "processes.csv"
```

### Module 2: Advanced PowerShell Concepts

#### Module 2 Introduction

This module delves into advanced topics like scripting, variables, loops, and automation.

#### Our Old Friend the ISE

The Integrated Scripting Environment (ISE) is a graphical host for PowerShell, providing a rich scripting experience.

#### Writing Our First Script

Save commands in a `.ps1` file and execute it.

**Example**:
```powershell
# MyScript.ps1
Get-Process
```

Run the script:
```powershell
.\MyScript.ps1
```

#### What Are Variables?

Variables store data for reuse. Declare variables using `$`.

#### Different Kinds of Variables

PowerShell supports various variable types, including strings, integers, arrays, and hash tables.

**Example**:
```powershell
$string = "Hello, PowerShell!"
$array = @(1, 2, 3)
$hashTable = @{Name="John"; Age=30}
```

#### Defining Data Types in PowerShell

Specify data types explicitly.

**Example**:
```powershell
[int]$number = 42
[string]$text = "PowerShell"
```

#### Read-Host: Dealing with Data

**Example**:
```powershell
$name = Read-Host "Enter your name"
Write-Output "Hello, $name"
```

#### How Operators Operate

PowerShell supports arithmetic, comparison, and logical operators.

**Example**:
```powershell
$result = 5 + 3
$isEqual = 5 -eq 5
```

#### Objects, Objects, Objects!

PowerShell's core is its object-oriented nature, allowing manipulation of complex data structures.

#### Decisions with If (Part 1)

**Example**:
```powershell
if ($true) {
    Write-Output "Condition is true"
}
```

#### Decisions with If (Part 2)

**Example**:
```powershell
if ($false) {
    Write-Output "Condition is false"
} else {
    Write-Output "Condition is true"
}
```

#### Decisions with If (Part 3)

**Example**:
```powershell
$number = 5
if ($number -gt 10) {
    Write-Output "Greater than 10"
} elseif ($number -lt 5) {
    Write-Output "Less than 5"
} else {
    Write-Output "Between 5 and 10"
}
```

#### Nesting Our If Statement

**Example**:
```powershell
if ($true) {
    if ($true) {
        Write-Output "Nested true"
    }
}
```

#### Comparison Operators

**Example**:
```powershell
$isEqual = 5 -eq 5
$isNotEqual = 5 -ne 4
```

#### Logical Operators

**Example**:
```powershell
$and = ($true -and $false)
$or = ($true -or $false)
```

#### Looping with the While Loop

**Example**:
```powershell
$count = 0
while ($count -lt 5) {
    Write-Output $count
    $count++
}
```

#### Looping with Foreach

**Example**:
```powershell
$array = @(1, 2, 3)
foreach ($item in $array) {
    Write-Output $item
}
```

#### In Case You Didn't Get My Two Where-Objects One-Liners Remark

#### Getting Text Input

**Example**:
```powershell
$text = Read-Host "Enter some text"
Write-Output $text
```

#### Importing CSV Files

**Example**:
```powershell
$csv = Import-Csv -Path "data.csv"
```

#### Using a CSV File to Create Something

**Example**:
```powershell
$csv = Import-Csv -Path "users.csv"
foreach ($user in $csv) {
    New-ADUser -Name $user.Name -GivenName $user.GivenName -Surname $user.Surname -SamAccountName $user.SamAccountName -UserPrincipalName $user.UserPrincipalName -Path "OU=Users,DC=domain,DC=com"
}
```

#### Moving to Active Directory and Creating a User

**Example**:
```powershell
New-ADUser -Name "John Doe" -GivenName "John" -Surname "Doe" -SamAccountName "jdoe" -UserPrincipalName "jdoe@domain.com" -Path "OU=Users,DC=domain,DC=com"
```

#### Moving to Active Directory and Retrieving a User

**Example**:
```powershell
Get-ADUser -Identity "jdoe"
```

#### Moving to Active Directory and Setting AD User Properties

**Example**:
```powershell


Set-ADUser -Identity "jdoe" -Title "Manager"
```

#### Moving to Active Directory and Creating and Moving Between OUs

**Example**:
```powershell
New-ADOrganizationalUnit -Name "NewOU" -Path "DC=domain,DC=com"
Move-ADObject -Identity "CN=John Doe,OU=Users,DC=domain,DC=com" -TargetPath "OU=NewOU,DC=domain,DC=com"
```

#### Creating Active Directory Users from a Simple Text File

**Example**:
```powershell
Get-Content -Path "users.txt" | ForEach-Object { New-ADUser -Name $_ -Path "OU=Users,DC=domain,DC=com" }
```

#### Creating Active Directory Users from a CSV File

**Example**:
```powershell
$csv = Import-Csv -Path "users.csv"
foreach ($user in $csv) {
    New-ADUser -Name $user.Name -GivenName $user.GivenName -Surname $user.Surname -SamAccountName $user.SamAccountName -UserPrincipalName $user.UserPrincipalName -Path "OU=Users,DC=domain,DC=com"
}
```

#### What Is PowerShell Remoting?

PowerShell Remoting allows you to run commands on remote computers.

#### Enabling PowerShell Remoting

**Example**:
```powershell
Enable-PSRemoting -Force
```

#### One-To-Many and Using Persistent Sessions

**Example**:
```powershell
$s = New-PSSession -ComputerName Server01
Invoke-Command -Session $s -ScriptBlock { Get-Process }
```
