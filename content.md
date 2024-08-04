## Introduction

This tutorial is designed to introduce software architects to PowerShell, covering both basic and advanced concepts. Through practical examples, you'll learn how to leverage PowerShell for system administration, automation, and scripting tasks.

### 1. Introduction to PowerShell

#### 1.1 What is PowerShell and PowerShell Versions

PowerShell is a task automation and configuration management framework from Microsoft, consisting of a command-line shell and the associated scripting language. It is built on the .NET framework and helps IT professionals and power users control and automate the administration of Windows operating systems and applications.

- **Versions**:
  - **Windows PowerShell**: Integrated into Windows, supports .NET Framework.
  - **PowerShell Core**: Cross-platform (Windows, macOS, Linux), supports .NET Core.
  - **PowerShell 7**: The latest version, combining the best features of Windows PowerShell and PowerShell Core.

#### 1.2 Why PowerShell and Examples

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

#### 1.3 Word of Note

PowerShell is a powerful tool that can make system administration more efficient. However, improper use can lead to significant issues, so it's crucial to understand the commands and scripts you run.

### 2. Module 1: PowerShell Basics

#### 2.1 Module 1 Introduction

In this module, you'll get acquainted with the fundamentals of PowerShell, including basic commands (cmdlets), syntax, and how to use the pipeline.

#### 2.2 Getting to Know PowerShell

PowerShell cmdlets are the building blocks of scripts and automation tasks.

#### 2.3 Cmdlets and Parameters - Examples with Get and Set

Cmdlets are lightweight commands used in the PowerShell environment. They follow a verb-noun naming pattern.

**Example 1**: Using `Get-Process`
```powershell
Get-Process
```

**Example 2**: Using `Set-Service`
```powershell
Set-Service -Name "wuauserv" -Status "Stopped"
```

#### 2.4 Getting Help for PowerShell

Use the `Get-Help` cmdlet to find information about cmdlets and concepts in PowerShell.

**Example**:
```powershell
Get-Help Get-Process
```

#### 2.5 Which Cmdlet Does the Job for You?

Use `Get-Command` to discover cmdlets.

**Example**:
```powershell
Get-Command -Verb Get
```

#### 2.6 What Are Modules?

Modules are packages of cmdlets, functions, and other tools. Import modules to extend PowerShell's functionality.

**Example**:
```powershell
Import-Module ActiveDirectory
```

#### 2.7 How Does the Pipeline Work?

The pipeline (`|`) passes the output of one cmdlet as input to another.

**Example**:
```powershell
Get-Process | Where-Object { $_.CPU -gt 100 }
```

#### 2.8 Outputting to a Text File

Redirect output to a text file using `Out-File`.

**Example**:
```powershell
Get-Process | Out-File "processes.txt"
```

#### 2.9 Parameters vs Properties

Parameters modify cmdlet behavior, while properties are attributes of objects returned by cmdlets.

#### 2.10 Formatting Data in PowerShell

Use `Format-Table` or `Format-List` to format output.

**Example**:
```powershell
Get-Process | Format-Table -Property Name, CPU
```

#### 2.11 PowerShell Objects: A Deeper Look

PowerShell is object-oriented. Each output from a cmdlet is an object with properties and methods.

#### 2.12 Getting to Properties and Methods

Access properties using `.` notation.

**Example**:
```powershell
(Get-Process)[0].Name
```

#### 2.13 What Kind of Properties Do We Have?

Properties can be simple data types (string, int) or complex objects.

#### 2.14 What Kind of Parameters Do We Have?

Parameters can be mandatory, optional, positional, or named.

#### 2.15 Using Where-Object to Filter Properties

**Example**:
```powershell
Get-Process | Where-Object { $_.CPU -gt 100 }
```

#### 2.16 Select-Object for Outputting Specific Information

**Example**:
```powershell
Get-Process | Select-Object -Property Name, CPU
```

#### 2.17 Sorting with Sort-Object

**Example**:
```powershell
Get-Process | Sort-Object -Property CPU -Descending
```

#### 2.18 Outputting to CSV

**Example**:
```powershell
Get-Process | Export-Csv -Path "processes.csv"
```

### 3. Module 2: Advanced PowerShell Concepts

#### 3.1 Module 2 Introduction

This module delves into advanced topics like scripting, variables, loops, and automation.

#### 3.2 Our Old Friend the ISE

The Integrated Scripting Environment (ISE) is a graphical host for PowerShell, providing a rich scripting experience.

#### 3.3 Writing Our First Script

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

#### 3.4 What Are Variables?

Variables store data for reuse. Declare variables using `$`.

#### 3.5 Different Kinds of Variables

PowerShell supports various variable types, including strings, integers, arrays, and hash tables.

**Example**:
```powershell
$string = "Hello, PowerShell!"
$array = @(1, 2, 3)
$hashTable = @{Name="John"; Age=30}
```

#### 3.6 Defining Data Types in PowerShell

Specify data types explicitly.

**Example**:
```powershell
[int]$number = 42
[string]$text = "PowerShell"
```

#### 3.7 Read-Host: Dealing with Data

**Example**:
```powershell
$name = Read-Host "Enter your name"
Write-Output "Hello, $name"
```

#### 3.8 How Operators Operate

PowerShell supports arithmetic, comparison, and logical operators.

**Example**:
```powershell
$result = 5 + 3
$isEqual = 5 -eq 5
```

#### 3.9 Objects, Objects, Objects!

PowerShell's core is its object-oriented nature, allowing manipulation of complex data structures.

#### 3.10 Decisions with If (Part 1)

**Example**:
```powershell
if ($true) {
    Write-Output "Condition is true"
}
```

#### 3.11 Decisions with If (Part 2)

**Example**:
```powershell
if ($false) {
    Write-Output "Condition is false"
} else {
    Write-Output "Condition is true"
}
```

#### 3.12 Decisions with If (Part 3)

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

#### 3.13 Nesting Our If Statement

**Example**:
```powershell
if ($true) {
    if ($true) {
        Write-Output "Nested true"
    }
}
```

#### 3.14 Comparison Operators

**Example**:
```powershell
$isEqual = 5 -eq 5
$isNotEqual = 5 -ne 4
```

#### 3.15 Logical Operators

**Example**:
```powershell
$and = ($true -and $false)
$or = ($true -or $false)
```

#### 3.16 Looping with the While Loop

**Example**:
```powershell
$count = 0
while ($count -lt 5) {
    Write-Output $count
    $count++
}
```

#### 3.17 Looping with Foreach

**Example**:
```powershell
$array = @(1, 2, 3)
foreach ($item in $array) {
    Write-Output $item
}
```

#### 3.18 In Case You Didn't Get My Two Where-Objects One-Liners Remark

#### 3.19 Getting Text Input

**Example**:
```powershell
$text = Read-Host "Enter some text"
Write-Output $text
```

#### 3.20 Importing CSV Files

**Example**:
```powershell
$csv = Import-Csv -Path "data.csv"
```

#### 3.21 Using a CSV File to Create Something

**Example**:
```powershell
$csv = Import-Csv -Path "users.csv"
foreach ($user in $csv) {
    New

-ADUser -Name $user.Name -SamAccountName $user.SamAccountName
}
```

#### 3.22 Practical Example: Automation Using PowerShell

#### 3.23 Additional Scripting Best Practices

### 4. Module 3: Advanced PowerShell Scripting

#### 4.1 Module 3 Introduction

#### 4.2 Writing Functions

**Example**:
```powershell
function Get-Square {
    param ($number)
    return $number * $number
}
```

#### 4.3 Writing Advanced Functions with Parameters and Validation

**Example**:
```powershell
function Get-Square {
    param (
        [int]$number
    )
    return $number * $number
}
```

#### 4.4 Error Handling with Try, Catch, Finally

**Example**:
```powershell
try {
    # Code that might throw an error
    $result = 1 / 0
} catch {
    Write-Output "An error occurred: $_"
} finally {
    Write-Output "Execution completed"
}
```

#### 4.5 Working with Modules

Create reusable modules for your scripts.

#### 4.6 Using Custom Modules

**Example**:
```powershell
Import-Module MyCustomModule
```

#### 4.7 Advanced Automation Scenarios

#### 4.8 Interacting with REST APIs

**Example**:
```powershell
$response = Invoke-RestMethod -Uri "https://api.example.com/data" -Method Get
```

#### 4.9 Advanced Logging Techniques

#### 4.10 Task Scheduling with PowerShell

**Example**:
```powershell
$action = New-ScheduledTaskAction -Execute "PowerShell.exe" -Argument "-File C:\Scripts\MyScript.ps1"
$trigger = New-ScheduledTaskTrigger -Daily -At 9am
Register-ScheduledTask -Action $action -Trigger $trigger -TaskName "MyDailyTask"
```

#### 4.11 Monitoring and Notification

#### 4.12 Advanced Data Processing

#### 4.13 Managing Remote Systems with PowerShell

**Example**:
```powershell
Invoke-Command -ComputerName Server01 -ScriptBlock { Get-Process }
```

### Conclusion

By the end of this tutorial, you should have a solid understanding of both basic and advanced PowerShell concepts, enabling you to automate complex tasks and manage systems efficiently.
