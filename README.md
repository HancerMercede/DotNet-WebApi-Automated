# New-WebApi.ps1 - .NET Web API Project Generator

![.NET Web API](https://img.shields.io/badge/.NET-8.0-512BD4)
![PowerShell](https://img.shields.io/badge/PowerShell-5.1+-5391FE)

## Table of Contents

- [Description](#description)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Parameters](#parameters)
- [Examples](#examples)
- [Common Scenarios](#common-scenarios)
- [Directory Structure](#directory-structure)
- [Troubleshooting](#troubleshooting)
- [Best Practices](#best-practices)
- [Contributing](#contributing)

## Description

`New-WebApi.ps1` is a PowerShell script designed to streamline the creation of new .NET Web API projects. With a single command, this script automates the entire setup process, saving you time and ensuring consistency across your API projects.

**Key Features:**

- One-command project creation
- Automatic Git initialization (optional)
- Proper directory structure following .NET conventions
- Minimal API configuration
- Comprehensive error handling
- Input validation for project names
- Clear user feedback and progress reporting

This script is particularly useful for developers who frequently create new Web API projects and want to maintain a standardized approach to project setup.

## Prerequisites

Before using this script, ensure you have the following installed:

- **.NET SDK 8.0** or later
  - Verify with: `dotnet --version`
  - Your current version: 8.0.400
- **PowerShell 5.1** or later
  - Verify with: `$PSVersionTable.PSVersion`
  - Your current version: 5.1.26100.4202
- **Git** (optional, only for repository initialization)
  - Verify with: `git --version`

## Installation

1. **Download the Script**

   The script is already located at: `C:\Users\HANCER MERCEDE\Scripts\New-WebApi.ps1`

2. **Make the Script Accessible (Optional)**

   To make the script accessible from any location, add the script's directory to your PATH:

   ```powershell
   $currentPath = [Environment]::GetEnvironmentVariable("PATH", "User")
   $scriptsPath = "$HOME\Scripts"
   [Environment]::SetEnvironmentVariable("PATH", "$currentPath;$scriptsPath", "User")
   ```

3. **Set Execution Policy (If Needed)**

   If you encounter execution policy restrictions:

   ```powershell
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```

## Usage

Basic usage requires only the project name:

```powershell
.\New-WebApi.ps1 -ProjectName "MyAwesomeApi"
```

To view the script's help information:

```powershell
Get-Help .\New-WebApi.ps1 -Detailed
```

## Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `-ProjectName` | String | Yes | The name of the Web API project. Must follow C# naming conventions (start with a letter or underscore, contain only letters, numbers, or underscores). |
| `-SkipGit` | Switch | No | If specified, skips Git repository initialization. |
| `-NoHttps` | Switch | No | If specified, configures the API without HTTPS support. |
| `-WhatIf` | Switch | No | Shows what would happen if the script runs without making any changes. |

## Examples

### Example 1: Create a Basic Web API

```powershell
.\New-WebApi.ps1 -ProjectName "CustomerApi"
```

This creates a new Web API project named `CustomerApi` with default settings (including HTTPS and Git initialization).

### Example 2: Create a Web API Without Git Initialization

```powershell
.\New-WebApi.ps1 -ProjectName "ProductService" -SkipGit
```

This creates a new Web API project without initializing a Git repository.

### Example 3: Create a Web API Without HTTPS

```powershell
.\New-WebApi.ps1 -ProjectName "InternalApi" -NoHttps
```

This creates a new Web API project configured without HTTPS support, suitable for internal services.

### Example 4: Perform a Dry Run

```powershell
.\New-WebApi.ps1 -ProjectName "TestApi" -WhatIf
```

This simulates creating a Web API project without actually making any changes.

## Common Scenarios

### Creating a Microservice

```powershell
# Create a directory for your microservices
mkdir Microservices
cd Microservices

# Create individual microservices
.\New-WebApi.ps1 -ProjectName "UserService"
.\New-WebApi.ps1 -ProjectName "OrderService"
.\New-WebApi.ps1 -ProjectName "PaymentService"
```

### Setting Up an Internal API

```powershell
# Create an API for internal use only
.\New-WebApi.ps1 -ProjectName "InternalToolsApi" -NoHttps
```

### Creating a Project Within an Existing Solution

```powershell
# Navigate to your solution directory
cd MyCompanySolution

# Create the API project
.\New-WebApi.ps1 -ProjectName "AdminApi"

# Add to existing solution
dotnet sln add .\AdminApi\AdminApi.csproj
```

## Directory Structure

After running the script, your project will have the following structure:

```
ProjectName/
├── Controllers/
│   └── WeatherForecastController.cs
├── Properties/
│   └── launchSettings.json
├── appsettings.json
├── appsettings.Development.json
├── Program.cs
├── ProjectName.csproj
└── WeatherForecast.cs
```

If Git is initialized, it will also include:

```
ProjectName/
├── .git/
└── .gitignore
```

## Troubleshooting

### Common Error Messages

#### "The term '.\New-WebApi.ps1' is not recognized..."

**Solution:**
- Ensure you're in the correct directory (`C:\Users\HANCER MERCEDE\Scripts`)
- Use the full path: `& "C:\Users\HANCER MERCEDE\Scripts\New-WebApi.ps1" -ProjectName "MyApi"`

#### "Project name is invalid"

**Solution:**
- Use only letters, numbers, and underscores
- Ensure the name starts with a letter or underscore
- Avoid using C# reserved keywords

#### "Failed to create .NET Web API project. dotnet CLI returned exit code"

**Solution:**
- Verify .NET SDK installation: `dotnet --version`
- Ensure the path doesn't contain invalid characters
- Check if you have proper permissions in the directory

#### "Git command not found. Skipping Git initialization."

**Solution:**
- Install Git from: https://git-scm.com/downloads
- Add Git to your PATH environment variable
- Use `-SkipGit` parameter if Git is not needed

### Execution Policy Restrictions

If you encounter execution policy restrictions:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

## Best Practices

1. **Use Meaningful Project Names**
   - Choose names that reflect the API's purpose (e.g., `UserManagementApi` instead of `Api1`)

2. **Organize Related APIs**
   - Create a parent directory for related APIs or microservices

3. **Initialize Git Early**
   - Let the script handle Git initialization to track changes from the beginning

4. **Add to Source Control**
   - Commit the script itself to your repository for team consistency

5. **Customize After Creation**
   - After creation, consider adding:
     - Authentication/Authorization
     - Swagger documentation
     - Logging framework
     - Database context

6. **Use with CI/CD**
   - Incorporate the script into your CI/CD pipeline for standardized project creation

7. **Create Project Templates**
   - For more specialized APIs, consider creating custom templates:
     ```powershell
     dotnet new --install <path-to-your-template>
     ```

## Contributing

Suggestions for improving this script are welcome! Consider these enhancements:

1. Add support for different authentication options
2. Include Docker file generation
3. Add database context setup options
4. Support for different API styles (REST, GraphQL)
5. Integration with specific cloud platforms

---

**Script Version:** 1.0  
**Last Updated:** 2025-06-19  
**Author:** System Administrator
