# Overview
This repository is home to a collection of templates used by development tools to provide a quick start experience for Azure Functions. A template in this context is a sample  that demonstrates use of one or more bindings supported by Azure Functions. Following are the development tools that use templates from this repository:

- [Azure Function Core Tools](https://github.com/Azure/azure-functions-core-tools)
- [Azure Portal](https://portal.azure.com)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Visual Studio](https://visualstudio.microsoft.com/vs/)

The repository contains precompliled C# and F# templates as well script type templates. Non-dotnet templates are consumed by the development tools via extension bundles. For more information on build and deployment infrastructure please refer to the section below.

## Build Status
|Branch|Status|Description|
|---|---|---|
|dev|[![Build Status](https://azfunc.visualstudio.com/Azure%20Functions/_apis/build/status/Azure.azure-functions-templates?branchName=dev)](https://azfunc.visualstudio.com/Azure%20Functions/_build/latest?definitionId=43&branchName=dev)| This is the primary development branch all pull request go against this branch. |
|master|[![Build Status](https://azfunc.visualstudio.com/Azure%20Functions/_apis/build/status/Azure.azure-functions-templates?branchName=master)](https://azfunc.visualstudio.com/Azure%20Functions/_build/latest?definitionId=43&branchName=master)| This is the deployment branch all releases are performed from this branch. |

## Build Requirements
- [Node (10.x)](https://nodejs.org/dist/latest-v10.x/)
- [Gulp](https://gulpjs.com/docs/en/getting-started/quick-start)

## Build Steps
```
cd Build
npm install
gulp build-all
```
> These build steps only work on Windows

## Creating a dotnet precompiled template

Dotnet templates contained in this repository adheres to the specification provided by the dotnet templating engine. The dotnet templating engine or an implementation of one is present within each of the dotnet client and is responsible for consuming dotnet templates. You can find more information on the templating engine at https://github.com/dotnet/templating. This section covers some basic information needed to add a pre-compiled template.

There are 2 kinds of dotnet templates.
1. Project templates: Project templates are responsible for creating intial set of files needed to build and run the project. For azure functions this would include, csproj file, host.json, local.settings.json file and so on.

2. Item templates: Item templates are templates include files that you would want to add to an existing project. For azure functions this would mean class files.

Template files:
1.  `.template.config/template.json` : This file contains symbols and post action action configuration that is used to generate a function from the template. The key difference in this file for project vs item template file is that `tags -> type` property would say project vs item for respective template types
2.  `.template.config/vs-2017.3.host` : This file contains information required to generate UI elements in Visual studio
3. `.template.config/vs-2017.3/*.png`: Icon files for menu items in Visual studio.

## Adding dotnet template to Visual Studio / Visual Studio code
This section covers information to add your template to the templates that show up within Visual studio and Visual studio code. VS and VS code only support templates that point to a single major version of a particular extension. That means there currently is no way to simultaneously include templates that target different major versions of the same extension within the same template list. As a result we only include templates that target the latest major version of a particular extension for respective function runtime version.

The build system in this repository uses .Nuspec files to manage different release trains.
|Nuspec File |Description|
|---|---|
|Build\PackageFiles\Dotnet_precompiled\ItemTemplates_v4.x.nuspec |
|Build\PackageFiles\Dotnet_precompiled\ItemTemplates-Isolated_v3.x.nuspec |
|Build\PackageFiles\Dotnet_precompiled\ItemTemplates-Isolated_v4.x.nuspec |
|Build\PackageFiles\Dotnet_precompiled\ProjectTemplates_v3.x.nuspec |
|Build\PackageFiles\Dotnet_precompiled\ProjectTemplates_v4.x.nuspec |
|Build\PackageFiles\Dotnet_precompiled\ProjectTemplates-Isolated_v3.x.nuspec |
|Build\PackageFiles\Dotnet_precompiled\ProjectTemplates-Isolated_v4.x.nuspec |

Testing dotnet template, 3 clients (either add instructions or say coming soon)
1. Core tools (white listed templates)
2. VS (File system modifications)
3. VS Code (no way hooks to inject templates)


<!-- Targeting a particular runtime version (should be included in the adding dotnet template section) -->

<!-- link to a dedicated section for PR guidelines -->

## Creating script (non-precompiled) type templates templates
<!-- Files and basic information neede to add a template  -->

<!-- Adding templates to bundles -->

<!-- testing instructions for script  -->
1. Core tools (white listed templates)
2. VS Code (no way hooks to inject templates)
3. Portal testing instructions

### Contribution guidelines:
- Include branch structure, build and test guidelines, diagrams that should the process of building to delivery
- Follow section x to add a template
- Send a PR

### Build, release and deployement information:


# License

This project is under the benevolent umbrella of the [.NET Foundation](http://www.dotnetfoundation.org/) and is licensed under [the MIT License](LICENSE.txt)

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## Related Github Repositories
- [Azure Function Core Tools](https://github.com/Azure/azure-functions-core-tools)
- [Azure Portal](https://github.com/Azure/azure-functions-ux)
- [Visual Studio Code](https://github.com/microsoft/vscode-azurefunctions)
- [Azure Function Host](https://github.com/Azure/azure-functions-host)
- [WebJobs SDK Extensions](https://github.com/Azure/azure-webjobs-sdk-extensions)

## Contribute Code or Provide Feedback
If you would like to become an active contributor to this project please follow the instructions provided in [Microsoft Azure Projects Contribution Guidelines](http://azure.github.com/guidelines.html).
If you encounter any bugs with the templates please file an issue in the [Issues](https://github.com/Azure/azure-webjobs-sdk-templates/issues) section of the project.
