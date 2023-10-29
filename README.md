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

These parameters provide multiple use case options for the dotnet templates, enable/disable flags for the utilization of different templates as per the requirements.

## Use Cases

You can directly call a particular template as per the requirement. for example: 

  ```yaml
  # azure-pipeline.yml
  resources:
  repositories:
    - repository: Template
      type: github
      name: your_username/AzureNugetRestore.ado
      ref: <respective branch name>
      endpoint: 'githubServiceConnectioNname'

  steps:
  # passing the parameters
- ${{ if eq( parameters.feedsToUse, 'select') }}:
  - template: templates/Nuget_Restore.yaml
    parameters: 
      restoreSolution: '${{ parameters.restoreSolution }}'   
      feedsToUse: '${{ parameters.feedsToUse }}'             
      vstsFeed: '${{ parameters.vstsFeed }}'     
      noCache: '${{ parameters.noCache }}'                   
      disableParallelProcessing: '${{ parameters.disableParallelProcessing }}'  
      restoreDirectory: '${{ parameters.restoreDirectory }}'   
      verbosityRestore: '${{ parameters.verbosityRestore }}' 

- ${{ elseif eq( parameters.feedsToUse, 'config') }}:
  - template: templates/Nuget_Restore.yaml
    parameters:
      restoreSolution: '${{ parameters.restoreSolution }}'    
      feedsToUse: '${{ parameters.feedsToUse }}'             
      nugetConfigPath: '${{ parameters.nugetConfigPath }}'    
      externalFeedCredentials: '${{ parameters.externalFeedCredentials }}' 
      noCache: '${{ parameters.noCache }}'                   
      disableParallelProcessing: '${{ parameters.disableParallelProcessing }}'  
      restoreDirectory: '${{ parameters.restoreDirectory }}'   
      verbosityRestore: '${{ parameters.verbosityRestore }}'

        
  
Make sure to adjust the repository name, branch name, and parameter values according to your project's requirements.

  ```

