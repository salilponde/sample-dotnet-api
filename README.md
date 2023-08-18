# Sample .NET API

## Build locally
You should be in the root directory of your code. not inside the project directory.

    dotnet build -f  sample-dotnet-api/Dockerfile . -t sample-dotnet-api

## Build in Azure DevOps
If you create an Azure Pipeline from Azure DevOps, ensure that you add *buildContext: $(Build.SourcesDirectory)* to the Docker task as shown in the below snippet.

    - task: Docker@2
      displayName: Build an image
      inputs:
        command: build
        buildContext: $(Build.SourcesDirectory)
        dockerfile: '$(Build.SourcesDirectory)/sample-dotnet-api/Dockerfile'
        tags: |
          $(tag)
          