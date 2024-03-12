# ADO Azure Image Pull

Use this Pipeline template to pull an image from one azure container registry to another azure container rehistry

## Parameters

The pipeline requires the following parameters to be defined:

| Name  | Displayname | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| sourceImageTag | tag used in image | string | 'latest' |  | Required ||
| armServiceConnection | Azure Service Connection for acr registry or azure resource manager in your Azure pipeline | string | | | Required | This helps the module to authenticate with registry or azure cli |
| servicePrincipalApplicationId |  | string | | | Required | |
| imageRepository | acr docker repository | string | | | Required | docker registry imagename |
| servicePrincipalClientAuth  | | string | | | Required ||
| targetContainerRegistry | The container registry where image is to be pushed  | string |  | | Required | |
| sourceContainerRegistry  | the container registry from where image is to be pulled | string | '.' | | Required | |
--------------------------------------------------------------------------------------------------------------------------------------------------

These parameters provide multiple use case options for the template, enable/disable flags for the utilization of different templates as per the requirements.

## Use Cases

You can directly call a particular template as per the requirement. for example:

  ```yaml
  # azure-pipeline.yml
  resources:
  repositories:
    - repository: Template
      type: github
      name: NashTech-Labs/adoacrimageimport
      ref: main
      endpoint: <githubServiceConnectionName>

  steps:
  # passing the parameters
  - template: adoacrimport.yml@Template
    parameters:
        armServiceConnection: ${{parameters.armServiceConnection}}
        sourceImageTag: ${{ parameters.sourceImageTag }}
        imageRepository: '${{parameters.imageRepository}}'
        servicePrincipalApplicationId: '${{parameters.servicePrincipalApplicationId}}'
        servicePrincipalClientAuth: '${{parameters.servicePrincipalClientAuth}}'
        targetContainerRegistry: ${{parameters.targetContainerRegistry}}
        sourceContainerRegistry: ${{parameters.sourceContainerRegistry}}      
  ```

* Make sure to adjust the repository name, branch name, and parameter values according to your project's requirements.
