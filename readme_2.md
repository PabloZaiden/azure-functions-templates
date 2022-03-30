# Overview
This repository is home to a collection of templates used by development tools to provide a quick start experience for Azure Functions. A template in this context is a sample Azure Function that demonstrates use of one or more bindings supported by Azure Functions. Following are the development tools that use templates from this repository:

- [Azure Function Core Tools](https://github.com/Azure/azure-functions-core-tools)
- [Azure Portal](https://portal.azure.com)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Visual Studio](https://visualstudio.microsoft.com/vs/)

## Build Status
|Branch|Status|
|---|---|
|dev|[![Build Status](https://azfunc.visualstudio.com/Azure%20Functions/_apis/build/status/Azure.azure-functions-templates?branchName=dev)](https://azfunc.visualstudio.com/Azure%20Functions/_build/latest?definitionId=43&branchName=dev)
|master|[![Build Status](https://azfunc.visualstudio.com/Azure%20Functions/_apis/build/status/Azure.azure-functions-templates?branchName=master)](https://azfunc.visualstudio.com/Azure%20Functions/_build/latest?definitionId=43&branchName=master)

## Repository structure and guidelines



## ra

On a high level this repository contains the following things

# target clients (include bundles here)

# building the repository 
Creating and testing templates
1. C# pre-compiled template
1.1 Creating a new template
<!-- - only includes information on what files to add -->
 
1.3 Testing C# per-compiled template in VS
1.4 Testing C# per-compiled template in VS Code
    1.2 Adding the template to the appropriate runtime / client
    <!-- Nuspec and non template file information -->

1.5 Testing C# per-compiled template in Core tools

2. Creating a csharp script (csx) and non-dotnet script type templates
    2.1 Testing template in Core tools
        1.2 Adding the template to the appropriate runtime / client
    2.2 Testing template in portal
    2.3 Testing template in VS Code

3. Submitting a templates PR

4. Additional testing information