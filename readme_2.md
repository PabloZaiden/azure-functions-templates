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
1.  `.template.config/template.json` : This file contains symbols and post action action configuration that is used to generate a function from the template. The key difference in this file for project vs item template file is that `tags -> type` property would say project vs item for corresponding template types
2.  `.template.config/vs-2017.3.host` : This file contains information required to generate UI elements in Visual studio
3. `.template.config/vs-2017.3/*.png`: Icon files for menu items in Visual studio.

## Adding dotnet template to Visual Studio / Visual Studio code
This section covers information you need to add your template to the list of templates that show up within Visual studio and Visual studio code. VS and VS code only support templates that point to a single major version of a particular extension. That means there currently is no way to simultaneously include templates that target different major versions of the same extension within the same template list. As a result we only include templates that target the latest major version of a particular extension for corresponding function runtime version. The build system in this repository uses .nuspec files to manage different release trains. Templates included in the nuspec file are included in their corresponding trains.

|Nuspec File |Description|
|---|---|
|[ProjectTemplates_v3.x.nuspec](Build/PackageFiles/Dotnet_precompiled/ProjectTemplates_v3.x.nuspec) | Project templates for dotnet in-proc function app targeting runtime v3 |
|[ProjectTemplates-Isolated_v3.x.nuspec](Build/PackageFiles/Dotnet_precompiled/ProjectTemplates-Isolated_v3.x.nuspec) | Project templates for dotnet isolated (out of proc) function app targeting runtime v3 |
|[ItemTemplates_v3.x.nuspec](Build/PackageFiles/Dotnet_precompiled/ItemTemplates_v3.x.nuspec) | Item templates for dotnet in-proc function app targeting runtime v3 |
|[ItemTemplates-Isolated_v3.x.nuspec](Build/PackageFiles/Dotnet_precompiled/ItemTemplates-Isolated_v3.x.nuspec) | Item templates for dotnet isolated (out of proc) function app targeting runtime v3 |
|[ProjectTemplates_v4.x.nuspec](Build/PackageFiles/Dotnet_precompiled/ProjectTemplates_v4.x.nuspec) | Project templates for dotnet in-proc function app targeting runtime v4 |
|[ProjectTemplates-Isolated_v4.x.nuspec](Build/PackageFiles/Dotnet_precompiled/ProjectTemplates-Isolated_v4.x.nuspec) | Project templates for dotnet isolated (out of proc)  function app targeting runtime v4 |
|[ItemTemplates_v4.x.nuspec](Build/PackageFiles/Dotnet_precompiled/ItemTemplates_v4.x.nuspec) | Item templates for dotnet in-proc function app targeting runtime v3 |
|[ItemTemplates-Isolated_v4.x.nuspec](Build/PackageFiles/Dotnet_precompiled/ItemTemplates-Isolated_v4.x.nuspec) | Item templates for dotnet isolated (out of proc)  function app targeting runtime v4 |


## Testing dotnet precompiled templates
Dotnet pre-compiled templates are currently hosted by the following clients. Please follow the instructions in this section to test the corresponding clients.

1. Visual Studio:

    1. Once the template files have been added / updated, build the templates using the [Build Steps](#build-steps)
    2. Make sure all instances of Visual Studio are closed;
    3. Open the directory `%userprofile%\AppData\Local\AzureFunctionsTools\Tags`
    4. Each of the directory within the tags directory represent a runtime, for testing runtime v4 templates open directory v4
    5. Open the `LastKnownGood` in v4 (runtime version templates you want to test) directory, Note the release version present in the file
    6. For testing in-proc templates, Open the templates folder `%userprofile%\AppData\Local\AzureFunctionsTools\Releases\<releaseVersion>\templates` matching the release version found in step 5. (Note: if adding the files to the release version folder found in `LastKnownGood` doesn't work, then try other release version folders.)
    7. Replace the contents of the folder with the one found in `..\bin\VS`
    8. Rename `Microsoft.Azure.WebJobs.ItemTemplates.X.0.0.nupkg` to `ItemTemplates.nupkg`, `Microsoft.Azure.WebJobs.ProjectTemplates.X.0.0.nupkg` to `ProjectTemplates.nupkg`
    9. For testing isolated templates, repeat the step 6 and 7, replace the contents of net5-isolated or net6-isolated instead of templates directory.
    10. Delete the `%userprofile%\.templateengine` directory
    11. Select corresponding function runtime when creating a new function app via Visual Studio 
    12. Run through the test scenarios

2. Core tools:
    1. Once the template files have been added / updated, build the templates using the [Build Steps](#build-steps)
    2. Find the location of core tools installation,you can use the command `where func` from windows command prompt
    3. Locate the `bin\tempaltes` directory relative to `azure-functions-core-tools` at install location
    4. Replace the contents of the folder with the one found in `..\bin\VS`
    5. Rename `Microsoft.Azure.WebJobs.ItemTemplates.X.0.0.nupkg` to `ItemTemplates.nupkg`, `Microsoft.Azure.WebJobs.ProjectTemplates.X.0.0.nupkg` to `ProjectTemplates.nupkg`
    6. For testing isolated templates, repeat the step 4 and 5, replace the contents of net5-isolated or net6-isolated directory instead.
    7. Delete the `%userprofile%\.templateengine` directory
    8. Run through the test scenarios

3. Visual Studio Code: We currently do not have a way to test templates in VS code without going to throuhgh extensive set up. Will update this section with instructions once we have the right set of hooks enabled.

## Creating script (non-precompiled) type templates templates
Script type templates are templates for functions that do not require a compilation step. Function from the deployed templates can be deployed as is. The templates includes metadata files in addition to the files required to execute a function. The metadata files help drive the user interface and development experience for creating a function using a template. In addition to the metadata file you would also need to add a code file for the correspionding language in the template. You can find information on the metadata files in the section below:

- **Resources.resx:** This file contains all the localized resource strings referenced in the metadata files. The strings are used for description, help, error text and other display text for the UI elements of the development tools. Strings in resources.resx file are reference by adding `$` before the corresponding string name. For example `TimerTriggerCSharp_description` is present in resources.resx file and is referenced in metadata.json file as `$TimerTriggerCSharp_description`

- **Sample.dat:** Sample.dat contains sample input data for each template.

- **Metadata.json:** This file includes basic information that explains the purpose of the template. It also includes configuration properties that help drive the UI required to create a function using a template. Individual properties are explain inline.

  ```Javascript
  {
      "defaultFunctionName": "TimerTrigger",      // Default name to be used for a function if the user does not provide one during deployment.
      "description": "$TimerTrigger_description", // Short description explaining the functionality of the generated function.
      "name": "Timer trigger",                    // The template name shown in UI.
      "language": "C#",
      "category": [                               // Category under which this template should be presented.
          "$temp_category_core", 
          "$temp_category_dataProcessing"
      ],
      "categoryStyle": "timer",                  // Category style used to pick the correct icon for the template.
      "enabledInTryMode": true,                  // Should this template be available in try mode: https://tryfunctions.com/ng-min/try?trial=true
      "userPrompt": [                            // The development tools will prompt to configure this setting during template deployment
          "schedule"
      ]
  }
  ```

- **Bindings.json:** This file contains metadata for all the configuration options available for all the bindings. This allows the development tools to provide the users with an option to configure additional settings for the bindings used by the template. It also drives to UI used to add / modify bindings of an existing functions. Here is a sample entry for timerTrigger binding. You only need to add a template for binding that does not exist in binding.json.

  ```Javascript
  {
    "type": "timerTrigger",                                     // The binding type property matching the "type" property in function.json
    "displayName": "$timerTrigger_displayName",                 // This is the text used by the UI element to display binding name.
    "direction": "trigger", 
    "enabledInTryMode": true,                                   // Should this binding be available in try mode https://tryfunctions.com/ng-min/try?trial=true
    "documentation": "$content=Documentation\\timerTrigger.md", // Location of the documentation related to this binding in the templates repository
    "settings": [                                               
        {
          "name": "schedule",
          "value": "string",
          "defaultValue": "0 * * * * *",
          "required": true,
          "label": "$timerTrigger_schedule_label",              // display text for the config option
          "help": "$timerTrigger_schedule_help",                // help text explaining what the config option is
          "validators": [
            {
              "expression": "",                                 // regex that can be used to validate the configuration value
              "errorText": "$timerTrigger_schedule_errorText"   // help text in case the regex validation fails
            }
          ]
        }
      ]
  }
  ```

## Adding template to extension bundle

## Testing script type template (added to extension bundle):
1. Once the template files have been added / updated, build the templates using the [Build Steps](#build-steps)
2. Locate the built templates at `..\bin\ExtensionBundle.Templates-v2`
3. Replace the contents of the `StaticContent\v1` directory for the bundle you want to test
    - Sample Location: `%userprofile%\AppData\Local\Temp\Functions\ExtensionBundles\Microsoft.Azure.Functions.ExtensionBundle\2.0.1\StaticContent\v1`
4. Create a new function app using `func init .` (If you are testing .csx files then run `func init . --csx`)
5. Create a new function using  `func new` (If you are testing .csx files then run `func new --csx`)
6. Start a function app by running `func host start` or `func start`

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
