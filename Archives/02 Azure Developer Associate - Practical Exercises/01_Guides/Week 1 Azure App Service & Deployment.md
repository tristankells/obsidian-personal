- https://portal.azure.com/#home
- Subscription
	- No
		- 1
	- Name
		- Pay-As-You-Go 
	- Id
		- c25ac33d-803e-44a3-821c-32b66adb47ea
	- Tenant
		- d2d76378-2628-4c65-b73e-40825f0ca037
	- **Resource Group**
		- Name
			- rg-envelopes-dev-nzn-01
		- Web App Service
			- Name
				- app-envelopes-dev-ro5pojtby3wwy
			- Web App
				- Name
					- app-envelopes-dev-ro5pojtby3wwy
				- Url
					- https://app-envelopes-dev-ro5pojtby3wwy.azurewebsites.net/
- Devops
	- https://tristankells.visualstudio.com/Envelopes
# 1. Create Resource Group and Azure App Service
## Powershell
```shell
# Download AZURE cli (REQUIRED: Winget)
winget install --exact --id Microsoft.AzureCLI

# Login to your AZURE CLI
az login --tenant d2d76378-2628-4c65-b73e-40825f0ca037

# List resource groups
az group list

# Create resource group
az group create --name rg-envelopesapp-dev-nzn --location newzealandnorth

# Create App Service Plan

# Create Web App


```

## Bicep
```yaml
// 1. Set the scope to subscription (needed to create a Resource Group)
targetScope = 'subscription'

// 2. Define parameters
param rgName string = 'rg-myapp-dev-nzn-01'
param rgLocation string = 'newzealandnorth'

// 3. Define the Resource Group
resource newRG 'Microsoft.Resources/resourceGroups@2024-03-01' = {
  name: rgName
  location: rgLocation
  tags: {
    Environment: 'Dev'
    ManagedBy: 'Bicep'
  }
}
```

### Bicep Cli

```shell
# Build the bicep
az bicep build-params --file "C:\Dev\Git\Envelopes.App\infra\params\dev.bicepparam"

# Deploy
az deployment sub create --location newzealandnorth --parameters "C:\Dev\Devops\envelopes.infra\params\dev.bicepparam"

# What if
az deployment group what-if \
  --resource-group ExampleGroup \
  --parameters "C:\Dev\Git\Envelopes.App\infra\params\dev.bicepparam"

# Drop resource group
az group delete --name rg-envelopes-dev-nzn-01 --yes 

az resource list --table

```

### References
- https://github.com/Azure/azure-quickstart-templates/blob/master/quickstarts/microsoft.web/app-service-docs-windows/main.bicep
## 2. Manual deployments
### Options
1. Locally Publish, zip, upload to deployment center.
	1. **Locally Publish, zip, upload via CLI**
2. **Visual Studio, right click publish project, configure new or existing resource**
3. Use Visual Studio Code
### Powershell
```shell
# --- Step 1: Configuration ---
# Update these variables with your specific Azure details
$resourceGroup = "rg-envelopes-dev-nzn-01"
$appName = "app-envelopes-dev-ro5pojtby3wwy"
$publishDir = "./publish"
$zipFile = "site.zip"

# --- Step 2: Publish the .NET Application ---
# This compiles your app and collects all required files into the 'publish' folder
dotnet publish -c Release -o "./publish"

# --- Step 3: Create a ZIP Archive ---
# We zip the *contents* of the publish folder, not the folder itself
if (Test-Path $zipFile) { Remove-Item $zipFile }
Compress-Archive -Path "$publishDir\*" -DestinationPath $zipFile -Force

# --- Step 4: Upload and Deploy to Azure ---
# This sends the zip to Azure and restarts the App Service
az webapp deploy --resource-group $resourceGroup --name $appName --src-path $zipFile

# --- Step 5: Cleanup (Optional) ---
# Remove the local publish folder and zip file after success
Remove-Item -Recurse -Force $publishDir
Remove-Item $zipFile
```

##  3. Configure Application Settings:
### Options
- Azure Portal > Web App > Settings > Environment Variables
- CLI
### Powershell
```shell
$resourceGroup = "rg-envelopes-dev-nzn-01"
$appName = "app-envelopes-dev-ro5pojtby3wwy"

az webapp config appsettings set --resource-group $resourceGroup --name $appName --settings ApiSettings__BaseUrl=https://envelopesapp.uk
```

*Note: This doesn't work for the the Web Assembly Envelopes, because the code is run on the browser, not on the machine with the environment variable.*
## 4. Enable Application Logging
*Note: Because we are Blazor Webassembly app, we have no server side logs, only client side console logs...* 
## 5. Create Deployment Slots
*Note: Standard or above, so not free.*
## 6. Configure CORS for API Communication
📌 Come back after deploying API
## 7. Custom Domain and SSL 
*Note: Not on free tier*
Original DNS entry
**Type**: cname
**Name**: envelopesapp.uk
**Target**: 3f7605fd-fd2e-4c28-a154-0deec82a31ee.cfargotunnel.com
## 8. Configure Authentication with Azure AD:
1. Configure a OAuth 2.0 client with Google
	1. https://developers.google.com/identity/gsi/web/guides/get-google-api-clientid
	2. Note client id and client secret.
	3. For **Authorized JavaScript origins**, add site url and development urls:
		1. https://app-envelopes-dev-ro5pojtby3wwy.azurewebsites.net
		2. http://localhost
		3. https://localhost
	4. Click **Audience**, then add your test users by email.
2. On Azure, go App Service > Settings > Authentication
3. Click **add identity provider.**
4. Fill in the details, including client id and client secret.
5. Wait for it to be deployed and try to access your app again.
6. You should get a **Authorized redirect URIs** failure from google.
7. Inspect the error details, and grab the correct redirect URI.
8. Go back to the google console and add the redirect URI to **Authorized redirect URIs**
9. Save and wait 5 mins.

https://learn.microsoft.com/en-us/azure/app-service/scenario-secure-app-authentication-app-service?tabs=external-configuration
https://developers.google.com/identity/gsi/web/guides/get-google-api-clientid
## 9. Create Azure DevOps Project: 
1. Create Azure DevOps Project
2. Go to https://tristankells.visualstudio.com/ and select **Create new project**
3. After creating new project, **Import a Git repository**
	1. Make sure you have a personal access token configured in git.
		1. **Settings** > **Developer Settings** > **Personal access tokens**
		2. Create a token with Contents > Read and Write permissions
![[Pasted image 20251222162800.png]]
## 10. Create Build Pipeline for Blazor App:
- Add the following pipeline to devops
```yaml
# Trigger pipeline on commits to master branch
trigger:
- master

pool:
  vmImage: 'ubuntu-latest'

steps:
# Test all projects (implicitly restores and builds)
- task: DotNetCoreCLI@2
  displayName: 'Test'
  inputs:
    command: 'test'
    projects: '**/*Tests.csproj'
    arguments: '--configuration Release'

# Publish app for deployment (reuses build cache from test step)
- task: DotNetCoreCLI@2
  displayName: 'Publish'
  inputs:
    command: 'publish'
    projects: 'Envelopes.App/Envelopes.App.csproj'
    arguments: '--configuration Release --output $(Build.ArtifactStagingDirectory)'
    zipAfterPublish: true

# Upload artifact for release pipeline
- publish: $(Build.ArtifactStagingDirectory)
  artifact: envelopes-app

```

## 11. Create Release Pipeline:
- Make sure you have a subscription connector in devops:
	- https://learn.microsoft.com/en-us/azure/devops/pipelines/library/connect-to-azure?view=azure-devops

![[Screenshot 2026-01-19 174631.png]]

- Create a azure-release-pipeline.yaml
	- azureSubscription will be the name of your conenctor in devops.
```yaml
# Release pipeline for Envelopes.App
# This pipeline is not triggered by commits. It is triggered by the completion of a build pipeline.
trigger: none

# This pipeline uses a resource trigger to run after the CI build pipeline completes.
resources:
  pipelines:
  - pipeline: ci-build # An identifier for the resource pipeline
    source: 'Envelopes.App' # The name of the build pipeline
    trigger:
      branches:
        include:
        - master

variables:
  # Replace with your Azure subscription service connection
  azureSubscription: 'Azure Resource Group Envelopes Dev New Zealand 01'
  
  # The name of your existing Web App
  webAppName: 'app-envelopes-dev-ro5pojtby3wwy'

  # The name of the artifact from the build pipeline
  artifactName: 'envelopes-app'

stages:
- stage: DeployDev
  displayName: 'Deploy to Dev Environment'
  jobs:
  - deployment: Deploy
    displayName: 'Deploy App'
    pool:
      vmImage: 'ubuntu-latest'
    environment: 'dev'
    strategy:
      runOnce:
        deploy:
          steps:
          # Download the build artifact
          - download: ci-build
            artifact: $(artifactName)

          # Deploy Application to App Service
          - task: AzureWebApp@1
            displayName: 'Deploy App to Azure App Service'
            inputs:
              azureSubscription: $(azureSubscription)
              appType: 'webAppLinux' # Assuming a Linux App Service from the ubuntu agent
              appName: $(webAppName) # Uses the new webAppName variable
              package: '$(Pipeline.Workspace)/ci-build/$(artifactName)/**/*.zip'
```
- Commit and push
- Navigate to pipelines
- Create new pipeline 
- Select Repository -> Azure Repos Git
- Choose existing azure pipeline yaml file > choose your azure-release-pipeline.yaml.
### Rename Pipelines
![[Pasted image 20260119182036.png]]

## How to install Terraform on windows
1. Download for windows: https://developer.hashicorp.com/terraform/install#windows
2. Extract to `c:\terraform`
3. Add  `c:\` to you `path` environment variable.
4. Open terminal, run `terraform -version`