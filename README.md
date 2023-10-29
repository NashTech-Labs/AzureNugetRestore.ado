# AzureNugetRestore.ado
With this template of NuGet Package Restore, you can install all your project's dependency without having to store them in source control. This allows for a cleaner development environment and a smaller repository size. 

## Pipeline Requirements

The dotNet Module pipeline requires the following parameters to be defined:

Parameters:


| Name  | Displayname | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | :-------------: | :-------------: | :-------------: | :-------------: | ------------- |
| NugetGitHubSource | ------------- | String |  | | Required | ------------- |
| restoreSolution | ------------- | String | **/*.csproj |  | Optional | Required when command = restore. Path to solution, packages.config, or project.json. Default: **/*.sln. |
| nugetConfigPath | ------------- | String | nuget.config |  |  Optional |  Use when selectOrConfig = config && command = restore |
| externalFeedCredentials | ------------- | String |  | |  Optional | Credentials for feeds outside this organization/collection |
| feedsToUse | ------------- | String | config | |  Optional | Feeds to use |
| vstsFeed | ------------- | String |  |  | Optional | Use packages from this Azure Artifacts/TFS feed |
| noCache | ------------- | Boolean | False |true / false |  Optional | Disable local cache |
| restoreDirectory | ------------- | String |  | |  Optional | Use when command = restore. Destination directory |
| disableParallelProcessing | ------------- | Boolean | False | true / false |  Optional | Use when command = restore. Disable parallel processing |
| verbosityRestore | ------------- | String | Detailed |  |  Optional |  Specifies the amount of detail displayed in the output |

