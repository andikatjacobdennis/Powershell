A PowerShell script to automate the creation of a .NET solution with WPF and Console projects, including various configurations and tasks:

```powershell
# PowerShell Script to Create a .NET Solution with WPF and Console Projects

# 1. Create a .NET Solution
$solutionName = "MySolution"
$wpfProjectName = "MyWpfApp"
$consoleProjectName = "MyConsoleApp"
$nugetPackage = "CsvHelper"
$certificateName = "MyCert.pfx"
$certificatePassword = "password"

# Navigate to the desired directory
$solutionPath = "C:\Projects\$solutionName"
if (!(Test-Path $solutionPath)) {
    New-Item -Path $solutionPath -ItemType Directory
}
Set-Location -Path $solutionPath

# Create the solution
dotnet new sln -n $solutionName

# 2. Add a WPF Project to the Solution
dotnet new wpf -n $wpfProjectName
dotnet sln add "$wpfProjectName\$wpfProjectName.csproj"

# 3. Add a Console Project to the Solution
dotnet new console -n $consoleProjectName
dotnet sln add "$consoleProjectName\$consoleProjectName.csproj"

# 4. Add a NuGet Package (CSV Helper)
dotnet add "$wpfProjectName\$wpfProjectName.csproj" package $nugetPackage
dotnet add "$consoleProjectName\$consoleProjectName.csproj" package $nugetPackage

# 5. Clean the Solution
dotnet clean "$solutionName.sln"

# 6. Restore the NuGet Packages
dotnet restore "$solutionName.sln"

# 7. Build the Solution
dotnet build "$solutionName.sln"

# 8. Clear the NuGet Cache and Restore Again
dotnet nuget locals all --clear
dotnet restore "$solutionName.sln"

# 9. Rebuild the Solution as x86 or x64
dotnet build "$solutionName.sln" -r win-x86
dotnet build "$solutionName.sln" -r win-x64

# 10. Logging the Build Process
dotnet build "$solutionName.sln" > build.log

# 11. Zip for Distribution
$timestamp = Get-Date -Format "yyyyMMdd_HHmmss"
$zipFileName = "MySolution_${timestamp}_v1.0.0.tar.gz"
Compress-Archive -Path "$solutionPath\*" -DestinationPath "$solutionPath\$zipFileName"

# 12. Create a Self-Signed Certificate
dotnet dev-certs https -ep "./$certificateName" -p $certificatePassword

# 13. Link Self-Signed Certificate with Projects
$certificateConfig = @"
<ItemGroup>
  <None Update="$certificateName">
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
  </None>
</ItemGroup>
"@

Add-Content -Path "$wpfProjectName\$wpfProjectName.csproj" -Value $certificateConfig
Add-Content -Path "$consoleProjectName\$consoleProjectName.csproj" -Value $certificateConfig

# 14. Generate XML Documentation for Swagger
$xmlDocConfig = @"
<PropertyGroup>
  <GenerateDocumentationFile>true</GenerateDocumentationFile>
</PropertyGroup>
"@

Add-Content -Path "$wpfProjectName\$wpfProjectName.csproj" -Value $xmlDocConfig
Add-Content -Path "$consoleProjectName\$consoleProjectName.csproj" -Value $xmlDocConfig

# Build the projects to generate XML documentation
dotnet build "$wpfProjectName\$wpfProjectName.csproj"
dotnet build "$consoleProjectName\$consoleProjectName.csproj"

Write-Output "All tasks completed successfully."
```

### Explanation:

1. **Create a .NET Solution**: Creates a new solution named `MySolution`.
2. **Add a WPF Project to the Solution**: Adds a new WPF project named `MyWpfApp` to the solution.
3. **Add a Console Project to the Solution**: Adds a new console project named `MyConsoleApp` to the solution.
4. **Add a NuGet Package**: Adds the CSV Helper NuGet package to both projects.
5. **Clean the Solution**: Cleans the solution to remove build artifacts.
6. **Restore the NuGet Packages**: Restores NuGet packages for the solution.
7. **Build the Solution**: Builds the solution.
8. **Clear the NuGet Cache and Restore Again**: Clears the NuGet cache and restores packages again.
9. **Rebuild the Solution as x86 or x64**: Rebuilds the solution targeting both x86 and x64.
10. **Logging the Build Process**: Logs the build output to `build.log`.
11. **Zip for Distribution**: Compresses the solution's output for distribution.
12. **Create a Self-Signed Certificate**: Creates a self-signed certificate.
13. **Link Self-Signed Certificate with Projects**: Adds the certificate to both projects.
14. **Generate XML Documentation for Swagger**: Configures the projects to generate XML documentation and builds them to produce the documentation files.

Run this PowerShell script in an elevated (administrator) PowerShell prompt to perform all the tasks sequentially.
