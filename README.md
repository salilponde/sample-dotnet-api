# Sample .NET API

## Build locally
You should be in the root directory of your code. not inside the project directory.

    dotnet build -f  sample-dotnet-api/Dockerfile . -t sample-dotnet-api

## Run

    docker run -p 8080:80 sample-dotnet-api

Open http://localhost:8080/weatherforecast in your browser to see if it works.

## Build in Azure DevOps
If you create an Azure DevOps Pipeline, ensure that you add *buildContext: $(Build.SourcesDirectory)* to the Docker task as shown in the below snippet.

    - task: Docker@2
      displayName: Build an image
      inputs:
        command: build
        buildContext: $(Build.SourcesDirectory)
        dockerfile: '$(Build.SourcesDirectory)/sample-dotnet-api/Dockerfile'
        tags: |
          $(tag)

## Pushing image to Docker Hub
Ensure that you specify the *repository* as shown below. Your username is used as a prefix on Docker Hub.

    - task: Docker@2
      displayName: Build image
      inputs:
        command: build
        buildContext: $(Build.SourcesDirectory)
        dockerfile: '$(Build.SourcesDirectory)/sample-dotnet-api/Dockerfile'
        repository: salilponde/sample-dotnet-api
        tags: |
          $(tag)
    - task: Docker@2
      displayName: Push image to Docker Hub
      inputs:
        containerRegistry: 'Docker Hub'
        repository: salilponde/sample-dotnet-api
        command: 'push'
        tags: |
          $(tag)
