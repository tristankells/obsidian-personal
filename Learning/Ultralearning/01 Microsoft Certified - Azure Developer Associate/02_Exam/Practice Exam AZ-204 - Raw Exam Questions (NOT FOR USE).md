Question 2 of 50

You plan to use a shared access signature to protect access to services within a general-purpose v2 storage account.

You need to identify the type of service that you can protect by using the user delegation shared access signature.

Which service should you identify?

Select only one answer.

Blob

**This answer is correct.**

File

Queue

**This answer is incorrect.**

Table

This item tests the candidate’s knowledge of identifying the supported authorization method, which is the first step of implementing it.

The blob service is the only one that supports user delegation shared access signatures. The file service supports account and service shared access signatures. The queue service supports account and service shared access signatures. The table service supports account and service shared access signatures.

[Discover shared access signatures - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-shared-access-signatures/2-shared-access-signatures-overview)

---
Question 3 of 50

You have blobs in an Azure storage account.

You need to implement a stored access policy that will apply to shared access signatures generated for the blobs.

To which type of storage resource should you associate the policy?

Select only one answer.

the storage account

**This answer is incorrect.**

the blob service of the storage account

the container that is hosting blobs

**This answer is correct.**

each individual blob

This item tests the candidate’s knowledge of configuring stored access policy, which is part of implementing authorization.

The container that is hosting blobs is used for associating the corresponding stored access policies. The storage account can be associated with shared access signatures keys but not stored access policies. The blob service of the storage account can be associated with shared access signatures keys but not stored access policies. Each individual blob can be associated with shared access signatures keys but not stored access policies.

[Define a stored access policy](https://learn.microsoft.com/en-us/rest/api/storageservices/define-stored-access-policy)

---
Question 4 of 50

You manage a Microsoft Entra ID registered application named **app1**. App1 calls a web API, which then calls Microsoft Graph.

You need to ensure the signed-in user identity is delegated through the request chain.

Which authentication flow should you use?

Select only one answer.

Authorization code

On-Behalf-Of

**This answer is correct.**

Client credentials

Implicit

This item tests the candidate’s knowledge of accessing user data from Microsoft Graph, which is part of implementing user authentication and authorization.

OAuth 2.0 On-Behalf-Of flow (OBO) is used when an application invokes a service or web API, which in turn needs to call another service or web API. The idea is to propagate the delegated user identity and permissions through the request chain. The OAuth 2.0 authorization code grant can be used in apps that are installed on a device to gain access to protected resources, such as web APIs. The OAuth 2.0 client credentials grant flow permits a web service (confidential client) to use its own credentials, instead of impersonating a user, to authenticate when calling another web service. Implicit is a redirection-based flow. The client must be capable of interacting with the resource owner's user-agent (typically a web browser). Authorization code, On-Behalf-Of, and implicit cannot be used to delegate user permission and identity.

[Implement authentication by using the Microsoft Authentication Library - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-authentication-by-using-microsoft-authentication-library/)

---
Question 5 of 50

You develop a multitenant web application named **App1**. You plan to register App1 with multiple Microsoft Entra ID tenants.

You need to identify the relationship between the application objects and security principals associated with App1.

Which relationship should you identify?

Select only one answer.

App1 will have multiple application objects and multiple service principals.

App1 will have multiple application objects and a single service principal.

App1 will have a single application object and multiple service principals.

**This answer is correct.**

App1 will have a single application object and a single service principal.

This item tests the candidate’s knowledge of configuring authentication of multitenant applications, which is a common scenario when implementing authentication.

App1 will have a single application object and multiple service principals. App1 will not have multiple application objects. multiple application objects and a single service principal., or a single service principal.

[Explore service principals - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/explore-microsoft-identity-platform/3-app-service-principals)

---
Question 6 of 50

You plan to generate a shared access signature (SAS) token for read access to a blob in a storage account.

You need to secure the token from being compromised.

What should you use?

Select only one answer.

Primary account key

Secondary account key

Microsoft Entra ID credentials assigned the Contributor role

**This answer is correct.**

Microsoft Entra ID credentials assigned the Reader role

**This answer is incorrect.**

This item tests the candidate's knowledge of Azure Storage shared access signatures (SAS).

Microsoft Entra ID credentials are required to generate the SAS token. The account used must have the Microsoft.Storage/storageAccounts/blobServices/generateUserDelegationKey permission, which is present in the following built-in roles: Contributor, Storage Account Contributor, Storage Blob Data Contributor, Storage Blob Data Owner, Storage Blob Data Reader, and Storage Blob Delegator. The account key can be used to generate the SAS token, but it can be more easily compromised.

[Discover shared access signatures - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-shared-access-signatures/2-shared-access-signatures-overview)

---
Question 7 of 50

You need to generate a shared access signature token that grants the Read permission to a blob container.

Which code segment should you use?

Select only one answer.

```
BlobSasBuilder sasBuilder = new BlobSasBuilder()
{
BlobContainerName = containerClient.Name,
Resource = "b"
};
sasBuilder.ExpiresOn = DateTimeOffset.UtcNow.AddHours(1);
sasBuilder.SetPermissions(BlobContainerSasPermissions.Read);
Uri sasUri = containerClient.GenerateSasUri(sasBuilder);
```

**This answer is incorrect.**

```
BlobSasBuilder sasBuilder = new BlobSasBuilder()
{
BlobContainerName = containerClient.Name,
Resource = "c"
};
sasBuilder.ExpiresOn = DateTimeOffset.UtcNow.AddHours(1);
sasBuilder.SetPermissions(BlobContainerSasPermissions.Read);
Uri sasUri = containerClient.GenerateSasUri(sasBuilder);
```

**This answer is correct.**

```
BlobSasBuilder sasBuilder = new BlobSasBuilder()
{
BlobContainerName = containerClient.Name,
Resource = “c”
};
sasBuilder.ExpiresOn = DateTimeOffset.UtcNow.AddHours(1);
sasBuilder.SetPermissions(BlobContainerSasPermissions.Create);
Uri sasUri = containerClient.GenerateSasUri(sasBuilder);
```

```
BlobSasBuilder sasBuilder = new BlobSasBuilder()
{
BlobContainerName = containerClient.Name,
Resource = "b"
};
sasBuilder.ExpiresOn = DateTimeOffset.UtcNow.AddHours(1);
sasBuilder.SetPermissions(BlobContainerSasPermissions.Create);
Uri sasUri = containerClient.GenerateSasUri(sasBuilder);
```

This item tests the candidate’s knowledge of creating and implementing shared access signatures.

The code segment that includes `Resource = "c"` and `sasBuilder.SetPermissions(BlobContainerSasPermissions.Read); will generate the shared access signatures token that grants the Read permission to a blob container. The code segment that includes resource = ‘b’ will generate a shared access signatures token at the blob level. The code segments that include sasBuilder.SetPermissions(BlobContainerSasPermissions.Create); will generate a shared access signatures token with the Create permission at the blob level.`

[Store data in Azure learning path - Training | Microsoft Learn](https://learn.microsoft.com/training/paths/store-data-in-azure/)

---
Question 8 of 50

You manage an Azure App Service Functions app named **app1** and a storage account named **account1**.

You have the following requirements:

- App1 should access account1 without managing credentials.
- The service principal associated with app1 cannot be explicitly deleted.

You need to configure a security principal for app1.

Which security principal should you use?

Select only one answer.

application

**This answer is incorrect.**

system-assigned managed identity

**This answer is correct.**

user-assigned managed identity

legacy

This item tests the candidate’s knowledge of implementing managed identities, which is part of implementing secure cloud solutions.

Managed identities for Azure resources eliminate the need to manage credentials in code. A system-assigned managed identity is restricted to one per resource and is tied to the lifecycle of the resource. Once enabled for app1, it will automatically create a service principal without the need to manage credentials and cannot be explicitly deleted.

A Microsoft Entra ID application is defined by its one and only application object, which resides in the Microsoft Entra ID tenant where the application was registered (known as the application's home tenant). It cannot be used by app1 to access a storage account without managing credentials. A user-assigned managed identity can be created and assigned to one or more instances of an Azure service. Once enabled for app1, a user-assigned managed identity will automatically create a service principal without the need to manage but will need to be explicitly deleted. The legacy service principal represents a legacy app, which is an app created before app registrations were introduced or an app created through legacy experiences. The legacy service principal cannot be used to access a storage account without managing credentials.

[Implement managed identities - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-managed-identities/)

---
Question 9 of 50

You have 10 applications running in Azure App Service.

You need to ensure the applications have access to items stored in Azure App Configuration by using a common configuration. Passwords or keys must not be used.

Which solution should you use?

Select only one answer.

system-assigned managed identities

user-assigned managed identity

**This answer is correct.**

service principal with permissions to Azure App Configuration

**This answer is incorrect.**

developer's credentials in code

This item tests the candidate's knowledge of managed identities.

User-assigned managed identities are a way to reuse the permissions across applications. User-assigned managed identities associate the managed identity to the new applications, with no keys or passwords. System-assigned managed identities use a new identity for each application, which does not meet the common configuration requirement. A service principal has keys that need to be rotated. The developer does not run the application, so the developer’s identity cannot be assumed.

[Implement Azure App Configuration - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-azure-app-configuration/)

---
Question 10 of 50

You plan to create a key namespace hierarchy in Azure App Configuration.

You need to separate individual key names.

Which character should you use?

Select only one answer.

:

**This answer is correct.**

*

,

**This answer is incorrect.**

\

This item tests the candidate’s knowledge of configuring key namespace hierarchy of App Configuration, which is part of implementing secure cloud solutions.

The colon character (:) is used to separate names of individual keys when creating a namespace hierarchy in Azure App Configuration. The asterisk character (*) is one of reserved characters in Azure App Configuration, so it cannot be used to separate names of individual keys when creating a namespace hierarchy in Azure App Configuration. The comma character (,) is one of reserved characters in Azure App Configuration, so it cannot be used to separate names of individual keys when creating a namespace hierarchy in Azure App Configuration. The backslash character () is one of reserved characters in Azure App Configuration, so it cannot be used to separate names of individual keys when creating a namespace hierarchy in Azure App Configuration.

[Create paired keys and values - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-azure-app-configuration/3-keys-values)

---
Question 11 of 50

A container group in Azure Container Instances has multiple containers.

The containers must restart when the process executed in the container group terminates due to an error.

You need to define the restart policy for the container group.

Which Azure CLI command should you use?

Select only one answer.

`az container restart \    --name mycontainer \    --resource-group myResourceGroup \    --no-wait`

`az container create \    --resource-group myResourceGroup \    --name mycontainer \    --image mycontainerimage \    --restart-policy Always`

`az container create \    --resource-group myResourceGroup \    --name mycontainer \    --image mycontainerimage \    --restart-policy Never`

`az container create \    --resource-group myResourceGroup \    --name mycontainer \    --image mycontainerimage \    --restart-policy OnFailure`

**This answer is correct.**

This item tests the candidate’s knowledge of running containers by using Azure Container Instances (ACI). Configurable restart policies can be specified for a container group in ACI. A configurable restart policy allows you to specify that containers are stopped when their processes have completed. When you create a container group in ACI, you can specify one of three restart policy settings: Always, Never, and OnFailure.

If the –restart-policy is mentioned as OnFailure, the containers in the container group are restarted only when the process executed in the container fails (when it terminates with a nonzero exit code). If the –restart-policy is mentioned as Always, the containers in the container group are always restarted irrespective of the success or failure of process execution in a container. If the –restart-policy is mentioned as Never, the containers in the container group will only run at most once.

The az container restart command is used to restart all the containers in a container group, not to define a restart policy for a container group.

[Run containerized tasks with restart policies](https://learn.microsoft.com/training/modules/create-run-container-images-azure-container-instances/4-run-containerized-tasks-restart-policies)

---
Question 12 of 50

Your company is developing a new web application that will be deployed as a containerized solution on Azure. The application is expected to have fluctuating workloads and needs to be highly available.

You need to create a solution that allows the application to scale based on demand and recover from failures automatically.

Each correct answer presents part of the solution. Which two actions should you perform? (Choose two.)

Select all answers that apply.

Deploy the containerized application to Azure Container Apps.

**This answer is correct.**

Store the application's images in Azure Blob Storage.

Deploy the containerized application to Azure Container Instance.

Publish the application's image to Azure Container Registry.

**This answer is correct.**

Publishing the application's image to Azure Container Registry allows it to be easily accessed and deployed to Azure services. Azure Container Apps is a serverless container service that automatically scales and recovers from failures, making it suitable for applications with fluctuating workloads and high availability requirements. Running containers using Azure Container Instance does not provide automatic scaling or recovery from failures. Azure Blob Storage is not designed for storing container images.  
[Implement Azure Container Apps - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/implement-azure-container-apps/)  
[Manage container images in Azure Container Registry - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/publish-container-image-to-azure-container-registry/)

---
Question 13 of 50

Your company is developing an application that includes a backend web API service. The development team has decided to use Azure Container Apps to host the API. They have a Dockerfile in the root of their repository that defines the containerized app.

You need to deploy the container app using the Dockerfile.

What should you do?

Select only one answer.

Use the `az containerapp env create` command with the `--name` parameter.

Use the `az containerapp create` command with the `--image` parameter.

Use the `az containerapp create` command with the `--containername` parameter.

Use the `az containerapp up` command with the `--source .` parameter.

**This answer is correct.**

The `az containerapp up` command with the `--source .` parameter builds and deploys the container app using the Dockerfile in the root of the repository. The other options either do not exist or do not fulfill the requirement.

[Quickstart: Build and deploy from local source code to Azure Container Apps - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/container-apps/quickstart-code-to-cloud?tabs=bash%2Ccsharp)

---
Question 14 of 50

You develop a web application hosted on the Web Apps feature of Microsoft Azure App Service.

You need to enable and configure Azure Web Service Local Cache with 1.5 GB.

Which two code segments should you use? Each correct answer presents part of the solution.

Select all answers that apply.

`“WEBSITE_LOCAL_CACHE_OPTION”: “Always”`

**This answer is correct.**

`“WEBSITE_LOCAL_CACHE_SIZEINMB”: “1500”`

**This answer is correct.**

`“WEBSITE_LOCAL_CACHE_OPTION”: “Enable”`

`“WEBSITE_LOCAL_CACHE_SIZEINMB”: “1.5”`

This item tests the candidate’s knowledge of configuring the settings of the Web Apps feature of Azure App Service.

By using `WEBSITE_LOCAL_CACHE_OPTION = Always`, local cache will be enabled. `WEBSITE_LOCAL_CACHE_SIZEINMB` will properly configure Local Cache with 1.5 GB of size. `WEBSITE_LOCAL_CACHE_OPTION = Enable` is not a valid value. `1.5` will not configure 1.5 GB for the local cache.

[Configure web app settings - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-web-app-settings/)

---
Question 15 of 50

You plan to develop an Azure App Service web app named **app1** by using a Windows custom container.

You need to load a TLS/SSL certificate in application code.

Which app setting should you configure?

Select only one answer.

`WEBSITE_LOAD_CERTIFICATES`

**This answer is correct.**

`WEBSITE_ROOT_CERTS_PATH`

**This answer is incorrect.**

`WEBSITE_CORS_ALLOWED_ORIGINS`

`WEBSITE_AUTH_TOKEN_CONTAINER_SASURL`

This item tests the candidate’s knowledge of configuring app settings, which is part of creating Azure App Service Web Apps.

The `WEBSITE_LOAD_CERTIFICATES` app setting makes the specified certificates accessible to Windows or Linux custom containers as files. The `WEBSITE_ROOT_CERTS_PATH` app setting is read-only and does not allow comma-separated thumbprint values to be mentioned to the certificates and then be loaded in the code. The `WEBSITE_AUTH_TOKEN_CONTAINER_SASURL` app setting is used to instruct the auth module to store and load all encrypted tokens to the specified blob storage container. This setting is used for Azure Storage and cannot be used to load certificates inside a Windows custom container.

[Configure web app settings - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-web-app-settings/)

---
Question 16 of 50

You manage a multi-instance deployment of an Azure App Service web app named **app1**.

You need to ensure a client application is routed to the same instance for the life of the session.

Which platform setting should you use?

Select only one answer.

WebSocket

Always on

HTTP version

ARR Affinity

**This answer is correct.**

This item tests the candidate’s knowledge of configuring web app settings, which is part of creating Azure App Service Web Apps.

In a multi-instance deployment, the ARR Affinity setting ensures a client application is routed to the same instance for the life of the session. WebSocket is a standardized protocol that provides full-duplex communication. Always on keeps the app loaded even when there is no traffic. In HTTP/2, a persistent connection can be used to service multiple simultaneous requests. WebSocket, Always on, and HTTP version are not used to ensure a client application is routed to the same instance for the life of the session.

[Configure web app settings - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-web-app-settings/)

---
Question 17 of 50

You are developing a Linux web app on Azure App Service.

You need to deploy the web app to the production environment based on the following requirements:

- App changes must be validated in an environment identical to the production environment before moving the app to the production environment.
- Downtime must be eliminated when the app is deployed to the production environment.

What should you use?

Select only one answer.

Deployment slots

**This answer is correct.**

Auto-scaling

Hybrid connection

App cloning

This item tests the candidate’s knowledge of when to use deployment slots. Deployment slots are live apps with unique host names, which allow swapping configuration and content between them. Auto-scaling is a feature that allows adding more capacity to an Azure Functions app hosting environment. This capacity can be added to an individual hosting environment (for example, scaling up or adding memory or CPU), or adding more hosts (scaling out). The scaling can be triggered based on a schedule or when breaching thresholds defined for certain metrics. Hybrid connections are available for consuming on-premises apps without needing to expose them to the internet. App cloning is a process to obtain an existing app and copy it to another destination, which can be a new app or a deployment slot, for example. However, this is not supported on Linux apps.

[Explore staging environments - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/understand-app-service-deployment-slots/2-app-service-staging-environments)

[Discover App Service networking features - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/introduction-to-azure-app-service/6-network-features)

[Examine Azure App Service plans - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/introduction-to-azure-app-service/3-azure-app-service-plans)

---
Question 18 of 50

A company has an App Service web app that requires a TLS/SSL certificate. The certificate will be used in other App Service apps. The certificate must be automatically renewed with the least management overhead.

You need to add the certificate.

What should you do?

Select only one answer.

Create a free App Service managed certificate.

**This answer is incorrect.**

Purchase an App Service certificate.

**This answer is correct.**

Upload a certificate from a third party.

Import a certificate from a Key Vault.

This item tests the candidate’s knowledge of configuring web app settings including SSL, API settings, and connection strings. Purchasing an App Service certificate automates the process of requesting, renewing, and synchronizing the certificate with the App Service apps that use them. Free App Service certificates offer basic functionalities and cannot be exported. Obtaining the certificate from a third party and uploading it to Azure App Service is also an option but lacks the automation and integration offered by the App Service certificates. It is recommended to store certificates in and retrieve them from a Key Vault, but if they are obtained from a third party, the renewal and synchronization with the App Service apps need to be automated in other ways.

[Configure security certificates - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-web-app-settings/6-configure-security-certificates)

---
Question 19 of 50

You plan to create an Azure Functions app named **app1**.

You need to ensure that app1 will satisfy the following requirements:

- Supports automatic scaling.
- Has event-based scaling behavior.
- Provides a serverless pricing model.

Which hosting plan should you use?

Select only one answer.

App Service

**This answer is incorrect.**

App Service Environment

Consumption

**This answer is correct.**

Functions Premium

This item tests the candidate’s knowledge of selecting the appropriate hosting plan, which is part of the implementation of Azure Functions.

The Consumption hosting plan satisfies all requirements. It supports autoscaling, has event-based scaling behavior, and provides a serverless pricing model. The App Service, App Service Environment, and Functions Premium hosting plans support autoscaling but does not provide the serverless pricing model. Its scaling behavior is not event based but performance based.

[Compare Azure Functions hosting options - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/explore-azure-functions/3-compare-azure-functions-hosting-options)

---
Question 20 of 50

You have an Azure Key Vault named **MyVault**.

You need to change the Azure App Service settings by using a key vault reference to access a secret named **MyConnection** from MyVault.

Which code segment should you use?

Select only one answer.

`@Microsoft.KeyVault(Secret=MyConnection;VaultName=MyVault)`

**This answer is incorrect.**

`@Microsoft.KeyVault(SecretName=MyConnection;VaultName=MyVault)`

**This answer is correct.**

`@Microsoft.KeyVault(Secret=MyConnection;Vault=MyVault)`

`@Microsoft.KeyVault(SecretName=MyConnection;Vault=MyVault)`

This item tests the candidate’s knowledge of retrieving secrets from Key Vault in Azure Functions.

The code segment `@Microsoft.KeyVault(SecretName=MyConnection;VaultName=MyVault)` segment reads the secret from Key Vault. The code segment that includes `Secret us`es an invalid parameter. The code segment that includes `Secret` and `Vault` use invalid parameters. The code segment that includes `SecretName` and `Vault` use invalid parameters.

[Create serverless applications learning path - Training | Microsoft Learn](https://learn.microsoft.com/training/paths/create-serverless-applications/)

---

Question 21 of 50

You plan to create a C# script-based Azure Functions app.

You need to configure the trigger and bindings for the functions of the Azure Functions app.

What should you do?

Select only one answer.

Create a function.json file for each function.

**This answer is correct.**

Create a host.json file for the Azure Functions app.

**This answer is incorrect.**

Decorate methods of each function with C# attributes.

Decorate parameters of each function with C# attributes.

This item tests the candidate’s knowledge of configuring triggers and bindings.

When using scripting languages, such as C# script, the function.json file for each function contains its triggers and bindings, and it needs to be explicitly created. The file host.json has runtime-specific configurations, not definitions of triggers and bindings. Decorating methods and Decorating parameters are used to define triggers and bindings when using compiled languages, not scripted ones.

[Create triggers and bindings - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/develop-azure-functions/3-create-triggers-bindings)

---
Question 22 of 50

A company plans to create an Azure Functions app.

You need to recommend a solution that meets the following requirements:

- Executes multiple functions concurrently.
- Performs aggregation on the results from the functions.
- Avoids cold starts.
- Minimizes costs.

Which two components should you recommend? Each correct answer presents part of the solution

Select all answers that apply.

The Consumption plan

The Premium plan

**This answer is correct.**

Fan-out/fan-in pattern

**This answer is correct.**

Function chaining pattern

This item tests the candidate’s knowledge of Azure Durable Functions and hosting plans.

The Premium plan avoids cold starts and offers unlimited execution duration. The fan-out/fan-in pattern enables multiple functions to be executed in parallel, waiting for all functions to finish. Often, some aggregation work is done on the results that are returned from the functions. The Consumption plan avoids paying for idle time but might face cold starts. Furthermore, each function run is limited to 10 minutes. The function chaining pattern is a sequence of functions that execute in a specific order. In this pattern, the output of one function is applied to the input of another function.

[AZ-204: Implement Azure Functions - Training | Microsoft Learn](https://learn.microsoft.com/training/paths/implement-azure-functions/)

---
Question 23 of 50

You create a batch routine by using a timer trigger in Azure Functions.

You need to configure the batch routine to execute every 15 minutes, from Monday through Friday.

Which code segment should you use?

Select only one answer.

[Function(nameof(TimerTriggerCSharp))]  
[FixedDelayRetry(5, "00:00:10")]  
public static void Run([TimerTrigger("0 */15 * * * 1-5")] TimerInfo myTimer,  
  FunctionContext context)  
{  
  var log = context.GetLogger(nameof(TimerFunction));  
  if (myTimer.IsPastDue)  
  {  
    log.LogInformation("Timer is running late!");  
  }  
  log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");  
}

**This answer is correct.**

[Function(nameof(TimerTriggerCSharp))]  
[FixedDelayRetry(5, "00:00:10")]  
public static void Run([TimerTrigger("*/15 * * * 0-4")] TimerInfo myTimer,  
  FunctionContext context)  
{  
  var log = context.GetLogger(nameof(TimerFunction));  
  if (myTimer.IsPastDue)  
  {  
    log.LogInformation("Timer is running late!");  
  }  
  log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");  
}

**This answer is incorrect.**

[Function(nameof(TimerTriggerCSharp))]  
[FixedDelayRetry(5, "00:00:10")]  
public static void Run([TimerTrigger("0 15 * * * ")] TimerInfo myTimer,  
  FunctionContext context)  
{  
  var log = context.GetLogger(nameof(TimerFunction));  
  if (myTimer.IsPastDue)  
  {  
    log.LogInformation("Timer is running late!");  
  }  
  log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");  
}

[Function(nameof(TimerTriggerCSharp))]  
[FixedDelayRetry(5, "00:00:10")]  
public static void Run([TimerTrigger("* 15 * * 1-5")] TimerInfo myTimer,  
  FunctionContext context)  
{  
  var log = context.GetLogger(nameof(TimerFunction));  
  if (myTimer.IsPastDue)  
  {  
    log.LogInformation("Timer is running late!");  
  }  
  log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");  
}

This item tests the candidate’s knowledge of working with timer triggers in Azure Functions.

The code segment that includes `Run([TimerTrigger("0 */15 * * * 1-5")` executes the function every 15 minutes from Monday to Friday. The code segment that includes `Run([TimerTrigger("*/15 * * * 0-4")` is missing the second part, and it is not using the proper range for days of the week. The code segment that includes `Run([TimerTrigger("0 15 * * * ")` executes only once at 15:00 (3 PM). The code segment that includes `Run([TimerTrigger("* 15 * * 1-5")` is missing the seconds attribute and the step (‘/’) part for the minutes.

https://learn.microsoft.com/training/modules/execute-azure-function-with-triggers/

[Timer trigger for Azure Functions - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-timer?tabs=python-v2%2Cisolated-process%2Cnodejs-v4&pivots=programming-language-csharp)

---
Question 24 of 50

You are developing an Azure Functions app that will be deployed to a Consumption plan. The app consumes data from a database server that has limited throughput.

You need to use the `functionAppScaleLimit` property to control the number of instances of the app that will be created.

Which value should you use for the property setting?

Select only one answer.

0

10

**This answer is correct.**

null

This item tests the candidate’s knowledge of configuring an Azure Functions app. Imposing limits on the scaling out capacity of an Azure Functions app can help when the app connects to components that have limited throughput. The `functionAppScaleLimit` property lets you define the number of instances of the Azure Functions app that will be created. Therefore, setting it to a low value, such as 10, is appropriate in this scenario. Azure Functions apps in the Consumption plan can scale out and have 200 instances as a default. A value of 0 or null for the `functionAppScaleLimit` property means that an unrestricted number of instances of the Azure Functions app will be created.

[Scale Azure Functions - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/explore-azure-functions/4-scale-azure-functions)

---
Question 25 of 50

You are a developing a serverless API using Azure Functions. The API is expected to handle a large number of HTTP requests and make outbound requests to a third-party service. The third-party service has a rate limit on the number of requests it can handle per minute.

You need to ensure that the Azure Function does not exceed the rate limit of the third-party service and manage resource utilization effectively.

Each correct answer presents part of the solution. Which two actions should you perform?

Select all answers that apply.

Enable 'dynamicThrottlesEnabled' property in the host.json file to reject requests with a 429 'Too Busy' response when system performance counters are over a high threshold.

Enable 'hsts' property in the host.json file to enforce HTTP Strict Transport Security (HSTS) behavior.

**This answer is incorrect.**

Set the 'maxConcurrentRequests' property in the host.json file to limit the number of parallel executions.

**This answer is correct.**

Set the 'maxOutstandingRequests' property in the host.json file to limit the number of outstanding requests at any given time.

**This answer is correct.**

Set the 'routePrefix' property in the host.json file to an empty string to remove the default prefix.

Setting the 'maxConcurrentRequests' property in the host.json file will limit the number of HTTP functions that are executed in parallel, which can help manage resource utilization and avoid exceeding the rate limit of the third-party service. The 'maxOutstandingRequests' property limits the number of outstanding requests that are held at any given time, including queued requests and in-progress executions, which can also help manage resource utilization. Enabling 'dynamicThrottlesEnabled' property would not help in this scenario as it rejects requests based on system performance counters, not based on the rate limit of a third-party service. The 'hsts' property is used to enforce HTTP Strict Transport Security (HSTS) behavior and is not related to managing resource utilization or rate limiting. The 'routePrefix' property is used to set the route prefix for all routes and does not affect resource utilization or rate limiting.

[Azure Functions HTTP triggers and bindings overview - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook?tabs=isolated-process%2Cfunctionsv2&pivots=programming-language-csharp)

---
Question 26 of 50

You need to read an Azure Cosmos DB change feed by using a push model.

Which two components can you use to achieve this goal? Each correct answer presents a complete solution.

Select all answers that apply.

Azure Functions with an Azure Cosmos DB trigger

**This answer is correct.**

Change feed processor library

**This answer is correct.**

Azure Functions with an Azure Event Grid trigger

Change feed pull model

This item tests the candidate’s knowledge of developing solutions that use Azure Cosmos DB storage.

Azure Functions with an Azure Cosmos DB trigger allows you to select the container to connect, and the Azure Function is triggered whenever there is a change in the container. The change feed processor library follows the observer pattern, where the processing function is called by the library. The change feed processor library will automatically check for changes and, if changes are found, push them to the client. Azure Functions with an Event Grid trigger will execute the function when an Event Grid event is dispatched. It has no relationship with an Azure Cosmos DB change feed. A change feed pull model will use a pull model rather than a push model.

[Consume an Azure Cosmos DB for NoSQL change feed using the SDK - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/consume-azure-cosmos-db-sql-api-change-feed-use-sdk/)

[Handle events with Azure Functions and Azure Cosmos DB for NoSQL change feed - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/handle-events-azure-functions-azure-cosmos-db-sql-api-change-feed/)

---
Question 27 of 50

You manage an Azure Cosmos DB container named **container1**.

You need to use the `ReadItemAsync` method to read an item from the Azure Cosmos service.

Which two parameters should you provide? Each correct answer presents part of the solution.

Select all answers that apply.

`consistencyLevel`

**This answer is incorrect.**

`eTag`

`partitionKey`

**This answer is correct.**

`sessionToken`

`id`

**This answer is correct.**

This item tests the candidate’s knowledge of setting the partition key, which is part of developing Azure Cosmos DB solutions.

The `ReadItemAsync` method of the container class of .NET SDK for Azure Cosmos DB has two mandatory parameters: `partitionKey` and `itemId`. The `consistencyLevel` parameter is part of the optional `requestOptions` parameter of the `ReadItemAsync`.

The `eTag` and `sessionToken` parameters are part of the optional `requestOptions` parameter of the `ReadItemAsync` method.

[Explore Microsoft .NET SDK v3 for Azure Cosmos DB - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/work-with-cosmos-db/2-cosmos-db-dotnet-overview)

---
Question 28 of 50

You plan to implement a storage mechanism for managing state across multiple change feed consumers.

You need to configure the change feed processor in the .NET SDK for Azure Cosmos DB for NoSQL API.

Which component should you use?

Select only one answer.

Delegate

Compute instance

Lease container

**This answer is correct.**

Monitored container

This item tests the candidate’s knowledge of configuring change feed processor as part of developing solutions that use Azure Cosmos DB.

The lease container component serves as a storage mechanism to manage state across multiple change feed consumers. The delegate component is the code within the client application that implements business logic for each batch of changes. The compute instance is a client application instance that listens for changes from the change feed. The monitored container component is monitored for any insert or update operations. It does not serve as a storage mechanism to manage state across multiple change feed consumers.

[Understand change feed features in the SDK - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/consume-azure-cosmos-db-sql-api-change-feed-use-sdk/2-understand-features-sdk)

---
Question 29 of 50

You manage the deployment of an Azure Cosmos DB account.

You must define custom logic by using the .NET SDK change feed processor to process changes that the change feed reads.

You need to select the appropriate change feed processor component.

Which component should you use?

Select only one answer.

monitored container

**This answer is incorrect.**

delegate

**This answer is correct.**

compute instance

lease container

This item tests the candidate’s knowledge of implementing change feed notifications in Azure Cosmos DB. The change feed processor in Azure Cosmos DB simplifies the process of reading the change feed and can be used to distribute the event processing across multiple consumers effectively. There are four main components in the change feed processor: the monitored container, the lease container, the compute instance, and the delegate. The monitored container has the data from which the change feed is generated. The delegate component can be used to define custom logic to process the changes that the change feed reads. The compute instance hosts the change feed processor to listen for changes. It can be represented by a VM, a Kubernetes pod, an Azure App Service instance, or an actual physical machine. The lease container acts as a state storage and coordinates the processing of the change feed across multiple workers.

[Understand change feed features in the SDK](https://learn.microsoft.com/training/modules/consume-azure-cosmos-db-sql-api-change-feed-use-sdk/2-understand-features-sdk)

---
Question 30 of 50

You have blobs in Azure Blob storage. The blobs store pictures.

You need to record the location and weather condition information from when the pictures were taken. You must ensure you can use up to 2,000 characters when recording the information.

What should you do?

Select only one answer.

Append a suffix to the blob name by using the location and weather. Add a delimiter between them.

Use metadata headers defined with a POST request.

**This answer is incorrect.**

Use metadata headers defined with a PUT request.

**This answer is correct.**

Create one container for each location. Inside each container, define the blob name as the weather type and a random suffix.

This item tests the candidate's knowledge about structuring data for blob storage.

Metadata is the proper way to define this kind of data, allowing independent modification and supporting up to 8 KB in total size. The HTTP verb to define metadata is a PUT, and this is the correct format to define metadata values. The maximum size of a blob name is 1,024 characters. Also, this is not an optimal approach because metadata can be obtained and set independently, maintaining the same file name. Metadata is the proper way to define this kind of data, allowing independent modification and supporting up to 8 KB in total size. But the HTTP verb to define metadata is a PUT, not POST. The combination of locations and weather types can be potentially unlimited, and container names are limited to 63 characters.

[AZ-204: Develop solutions that use Blob storage - Training | Microsoft Learn](https://learn.microsoft.com/training/paths/develop-solutions-that-use-blob-storage/)

---
Question 31 of 50

You need to download blob content to a byte array by using an operation that automatically recovers from transient failures.

Which code statement should you use?

Select only one answer.

```
byte[] data;
BlobClient client = new BlobClient(new Uri("https://mystorageaccount.blob.core.windows.net/containers/blob.txt"), null);
Response<BlobDownloadResult> response = client.DownloadContent(data);
```

```
BlobRequestOptions optionsWithRetryPolicy = new BlobRequestOptions();
byte[]destinationArray = blob.DownloadContent( index: 0, accessCondition: null, options: optionsWithRetryPolicy);
```

```
byte[] data;
BlobClient client = new BlobClient(new Uri(“https://mystorageaccount.blob.core.windows.net/containers/blob.txt”), null);
Response<BlobDownloadResult> response = client.DownloadContent();
data = response.Value.Content.ToArray();
```

```
byte[] data;
BlobClientOptions options = new BlobClientOptions();
options.Retry.MaxRetries = 10;
options.Retry.Delay = TimeSpan.FromSeconds(20);
BlobClient client = new BlobClient(new Uri("https://mystorageaccount.blob.core.windows.net/containers/blob.txt"), options);
Response<BlobDownloadResult> response = client.DownloadContent();
data = response.Value.Content.ToArray();
```

**This answer is correct.**

This item tests the candidate’s knowledge of implementing storage policies.

The code segment that includes `options.Retry.MaxRetries = 10;` and `options.Retry.Delay = TimeSpan.FromSeconds(20);` defines the retry strategy and downloads the content to the variable data. The code segments that do not include these parameters do not define the retry strategy.

[Azure Fundamentals: Describe Azure architecture and services - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/paths/azure-fundamentals-describe-azure-architecture-services/)

---
You have an Azure storage lifecycle policy for block blobs.

You need to create a prefixMatch filter rule that will contain an array of strings for prefixes to be matched.

What should be the first element of the prefix string?

Select only one answer.

a block blob index tag

a block blob name

**This answer is incorrect.**

a container name

**This answer is correct.**

a storage account name

This item tests the candidate’s knowledge of configuring prefixMatch filter, which is an essential part of setting up storage policy and is part of solution development for blob storage.

When creating a prefixMatch filter rule for an Azure storage lifecycle policy for block blobs, the first element of the prefix string must be a container name not a block blob index tag, block blob name, or storage account name.

[Discover Blob storage lifecycle policies - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/manage-azure-blob-storage-lifecycle/3-blob-storage-lifecycle-policies)

---
Question 33 of 50

You need to rehydrate a blob stored in the Archive tier by changing the access tier.

Which destination blob should you use?

Select only one answer.

A blob in the Archive tier in the same region.

A blob in the Archive tier in a different region.

A blob in the Cool tier in a different region.

A blob in the Cool tier in the same region.

**This answer is correct.**

This item tests the candidate’s knowledge of rehydrating blobs.

Blobs in the Archive tier can be rehydrated only to online tiers (that is, Cool or Hot). The destination can be any storage account in the same region.

[Rehydrate blob data from the archive tier - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/manage-azure-blob-storage-lifecycle/5-rehydrate-blob-data)

---
Question 34 of 50

A company uses Azure API Management to expose some of its services.

Each developer consuming APIs must use a single key to obtain access to various APIs without requiring approval from the API publisher.

You need to recommend a solution.

Which solution should you recommend?

Select only one answer.

Define a subscription with all APIs scope.

**This answer is incorrect.**

Define a subscription with product scope.

**This answer is correct.**

Restrict access based on caller IPs.

Restrict APIs based on client certificate.

This item tests the candidate's knowledge of Azure API Management subscriptions.

When creating a product, several APIs can be added to the product and a subscription can be associated with it. Access should not be granted to all APIs. Developer access should be granted regardless of the caller IP. A client certificate would require a policy to validate the certificate and specific logic to map the client to specific APIs.

[Secure APIs by using subscriptions - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/explore-api-management/6-secure-access-api-subscriptions)

---
Question 35 of 50

You manage an Azure API Management instance.

You need to limit the maximum number of API calls allowed from a single source for a specific time interval.

What should you configure?

Select only one answer.

Product

Policy

**This answer is correct.**

Subscription

API

This item tests the candidate’s knowledge of polices in Azure API Management, which is part of implementing API Management.

API publishers can change API behavior through configuration using policies. Policies are a collection of statements that run sequentially on the request or response of an API. A product has one or more APIs, a usage quota, and the terms of use and cannot be used to restrict the number of API calls. Subscriptions are the most common way for API consumers to access APIs published through an API Management instance. API is a representation of a back-end API and needs to be configured with a policy to implement a rate limit.

[How Azure API Management Works - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/introduction-to-azure-api-management/3-how-azure-api-management-works)

---
A company is using Azure API Management to expose their APIs to external partners. The company wants to ensure that the APIs are accessible only to users authenticated with OAuth 2.0, and that usage quotas are enforced to prevent abuse.

You need to configure the API Management instance to meet the security and usage requirements.

Which two actions should you perform?

Select all answers that apply.

Configure a validate-jwt policy to authenticate incoming requests.

**This answer is correct.**

Deploy an Azure Application Gateway in front of the API Management instance.

Implement IP filtering by defining access restriction policies.

Set up a rate limit by key policy to enforce call quotas.

**This answer is correct.**

Configuring a validate-jwt policy is necessary to authenticate users with OAuth 2.0. Setting up a rate limit by key policy helps enforce usage quotas. IP filtering does not address the authentication and quota requirements. Deploying an Azure Application Gateway is not required for these specific needs.

[Quickstart: Create a new Azure API Management instance by using the Azure CLI](https://learn.microsoft.com/en-us/azure/api-management/get-started-create-service-instance-cli)  
[Authentication and authorization to APIs in Azure API Management](https://learn.microsoft.com/en-us/azure/api-management/authentication-authorization-overview)

---
Question 37 of 50

You have an Azure event hub.

You need to add partitions to the event hub.

Which code segment should you use?

Select only one answer.

`az eventhubs eventhub consumer-group update --resource-group MyResourceGroupName --namespace-name MyNamespaceName --eventhub-name MyEventHubName --set partitioncount=12`

**This answer is incorrect.**

`az eventhubs eventhub consumer-group create --resource-group MyResourceGroupName --namespace-name MyNamespaceName --eventhub-name MyEventHubName --set partitioncount=12`

`az eventhubs eventhub update --resource-group MyResourceGroupName --namespace-name MyNamespaceName --name MyEventHubName --partition-count 12`

**This answer is correct.**

`az eventhubs eventhub create --resource-group MyResourceGroupName --namespace-name MyNamespaceName --name MyEventHubName --partition-count 12`

This item tests the candidate’s knowledge of developing event-based solutions.

The code segment that includes `az eventhubs eventhub update` adds partitions to an existing event hub. The code segment that includes `az eventhubs eventhub consumer-group update` updates the event hub consumer group. The code segment that includes `az eventhubs eventhub consumer-group create` will create an event hub consumer group. The code segment that includes `az eventhubs eventhub create --resource-group` segment will create an event hub with partitions, not change an existing one

[Control Azure services with the CLI - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/control-azure-services-with-cli/)

---
Question 38 of 50

You need to capture events streaming from Azure Event Hubs.

To which three locations can you capture data? Each correct answer presents a complete solution.

Select all answers that apply.

Azure Blob storage

**This answer is correct.**

Azure Data Lake Storage Gen1

**This answer is correct.**

Azure Functions

Azure Stream Analytics

**This answer is incorrect.**

Azure Data Lake Storage Gen2

**This answer is correct.**

This item tests the candidate’s knowledge of implementing solutions that use Azure Event Hubs.

Azure Event Hubs Capture can automatically deliver the streaming data in Event Hubs to Azure Blob storage. Azure Event Hubs Capture can automatically deliver the streaming data in Event Hubs to Azure Data Lake Storage Gen1. Azure Event Hubs Capture can automatically deliver the streaming data in Event Hubs to Azure Data Lake Storage Gen2. Azure Functions and Azure Stream Analytics cannot be used to capture events from Azure Event Hubs.

[Explore Azure Event Hubs - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/azure-event-hubs/)

---
Question 39 of 50

You have an Azure Service Bus instance.

You need to provide first-in, first-out (FIFO) guarantee for message processing.

What should you configure?

Select only one answer.

dead-letter queue

message deferral

message sessions

**This answer is correct.**

scheduled delivery

This item tests the candidate’s knowledge of setting up FIFO guarantees in Azure Service Bus, which is a common task when implementing solutions by using Azure Service Bus.

To provide FIFO guarantees in Service Bus, sessions must be configured. Message sessions enable exclusive, ordered handling of unbounded sequences of related messages. A dead-letter queue holds messages that cannot be delivered to any receiver. Message deferral makes it possible to defer retrieval of a message until a later time. Scheduled delivery allows submitting messages to a queue or topic for delayed processing. A dead-letter queue, message deferral, and scheduled delivery do not provide FIFO guarantees.

[Explore Azure Service Bus - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/discover-azure-message-queue/3-azure-service-bus-overview)

---
Question 40 of 50

You create an Azure Service Bus topic with a default message time to live of 10 minutes.

You need to send messages to this topic with a time to live of 15 minutes. The solution must not affect other applications that are using the topic.

What should you recommend?

Select only one answer.

Change the topic’s default time to live to 15 minutes.

Change the specific message’s time to live to 15 minutes.

**This answer is incorrect.**

Create a new topic with a default time to live of 15 minutes. Send the messages to this topic.

**This answer is correct.**

Update the time to live for the queue containing the topic.

This question tests the candidate's knowledge of Azure Service Bus message expiration.

To avoid affecting existing applications, the time to live of the existing topic must not be changed. A new topic needs to be created. Changing the topic's default time to live will affect other applications. A message-level time to live cannot be higher than the topic's time to live. To avoid affecting existing applications, the time to live of the existing topic or queue must not be changed.

[Exercise: Send and receive message from a Service Bus queue by using .NET. - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/discover-azure-message-queue/6-send-receive-messages-service-bus)

---
Question 41 of 50

You need to write a filter condition for an Azure Service Bus topic.

Which three filters can you use? Each correct answer presents a complete solution.

Select all answers that apply.

SQL

**This answer is correct.**

Boolean

**This answer is correct.**

Size

**This answer is incorrect.**

Correlation

**This answer is correct.**

Content

**This answer is incorrect.**

This item tests the candidate’s knowledge of implementing solutions that use Azure Service Bus.

A SqlFilter holds a SQL-like conditional expression that is evaluated in the broker against the arriving message’s user-defined properties and system properties. The TrueFilter and FalseFilter either cause all arriving messages (true) or none of the arriving messages (false) to be selected for the subscription. A CorrelationFilter holds a set of conditions that are matched against one or more of an arriving message's user and system properties. Size Filter and Content are not valid options for Service Bus topic filtering.

[Implement message-based communication workflows with Azure Service Bus - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-message-workflows-with-service-bus/)

---
Question 42 of 50

You have an Azure Service Bus queue.

You need to ensure a publisher can send messages into a topic and multiple subscribers can become eligible to consume the messages.

Which message routing pattern should you use?

Select only one answer.

simple request/reply

multicast request/reply

**This answer is correct.**

multiplexing

multiplexed request/reply

**This answer is incorrect.**

This item tests the candidate’s knowledge of message routing in Azure Service Bus, which is part of developing message-based solutions.

A publisher can send a message into a topic and multiple subscribers can become eligible to consume the message. A publisher can send a message into a queue and expect a reply from the message consumer, but multiple subscribers cannot consume the message. This session feature enables multiplexing of streams of related messages through a single queue but cannot be consumed by multiple subscribers. This session feature enables multiplexed replies, allowing several publishers to share a reply queue, but a message cannot be consumed by multiple subscribers.

[Explore Service Bus message payloads and serialization - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/discover-azure-message-queue/5-messages-payloads-serialization)

---
Question 43 of 50

You are developing a .NET project that will manage messages in Azure Storage queues.

You need to verify the presence of messages in a queue without removing them from the queue.

Which method should you use?

Select only one answer.

Peek

PeekMessages

**This answer is correct.**

ReceiveMessages

ReceiveMessageAsync

This item tests the candidate’s knowledge of processing messages in Azure Queue Storage, which is an integral part of implementing solutions that use Azure Queue Storage queues.

Messages can be peeked at in the queue without removing them from the queue by calling the PeekMessages method of the QueueClient class. The Peek method of the QueueClient class is used with Azure Service Bus, not Azure Queue Storage. The ReceiveMessages method of the QueueClient class removes them from the queue. The ReceiveMessageAsync method of the QueueClient class is used with Azure Service Bus, not Azure Queue Storage.

[Create and manage Azure Queue Storage and messages by using .NET - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/discover-azure-message-queue/8-queue-storage-code-examples)

---
Question 44 of 50

You have an application that requires message queuing.

You need to recommend a solution that meets the following requirements:

- automatic duplicate message detection.
- ability to send 2 MB messages.

Which message queuing solution should you recommend?

Select only one answer.

Azure Service Bus Premium tier

**This answer is correct.**

Azure Service Bus Standard tier

Azure Storage queues with locally redundant storage (LRS)

Azure Storage queues with zone-redundant storage (ZRS)

This item tests the candidate's knowledge of Azure Service Bus.

Service Bus detects duplicate messages. The Premium tier is required to send messages larger than 256 KB. Although Service Bus detects duplicate messages, the Standard tier only supports messages that are up to 256 KB in size. Azure Storage queues do not support duplicate message detection. Azure Storage queues do not support duplicate message detection.

[Explore Azure Service Bus - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/discover-azure-message-queue/3-azure-service-bus-overview)

---
Question 45 of 50

A logistics company requires a messaging system that can automatically handle messages that cannot be processed after several attempts, moving them to a separate storage for later analysis.

You need to choose a queue service that supports automatic handling of non-processable messages.

What should you use?

Select only one answer.

Azure Event Grid with advanced filtering

Azure Queue Storage with message expiration

Azure Service Bus dead-letter queue

**This answer is correct.**

Azure Storage queues with visibility timeout

Azure Service Bus dead-letter queue is designed to hold messages that cannot be delivered to any receiver or are not processed successfully, which is suitable for the company's requirement. Azure Storage queues with visibility timeout only hide messages temporarily and do not move them to separate storage. Azure Event Grid with advanced filtering is for event routing, not for handling failed message processing. Azure Queue Storage with message expiration simply deletes expired messages rather than moving them for analysis.

[Discover Azure message queues - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/discover-azure-message-queue)  
[Storage queues and Service Bus queues - compared and contrasted - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted)

---
Question 46 of 50

A financial services company is implementing a system to process transactions that are received as messages. The system must ensure that transactions are processed only once, and in the exact order they are received to maintain data integrity.

You need to design a messaging solution that guarantees first-in-first-out (FIFO) message delivery and processing.

Which two services should you use?

Select all answers that apply.

Azure Event Grid with advanced filtering

Azure Queue Storage with visibility timeout

Azure Service Bus with duplicate detection

**This answer is correct.**

Azure Service Bus with sessions enabled

**This answer is correct.**

Azure Service Bus with sessions enabled allows for FIFO processing by using sessions to ensure that related messages are handled in the order they are received. Duplicate detection helps to ensure that the system does not process the same transaction more than once. Azure Queue Storage does not guarantee FIFO processing as it does not support sessions, and visibility timeout only hides the message temporarily from other consumers. Azure Event Grid is an event routing service and does not provide FIFO guarantees or message sessions.

[Discover Azure message queues - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/discover-azure-message-queue)  
[What is Azure Service Bus? - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview)

---
Question 47 of 50

You have an Azure web app that occasionally experiences high response times.

You need to be notified when the response time exceeds a certain threshold.

What should you do?

Select only one answer.

Configure Azure Advisor alerts.

Create a Resource Health alert in Azure Monitor.

**This answer is incorrect.**

Implement Application Insights web tests and alerts.

**This answer is correct.**

Use Azure Service Health to monitor the status of Azure services.

Application Insights allows you to create web tests that simulate user interactions with your application and then set up alerts based on the results of these tests. Azure Monitor Resource Health alerts are used for infrastructure monitoring, not application performance. Azure Service Health provides information about Azure service issues and planned maintenance, not application performance. Azure Advisor provides best practice recommendations, not application performance alerts.  
[Monitor app performance - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/monitor-app-performance/)

---
Question 48 of 50

Your team is developing a new feature for an existing Azure-based application that relies heavily on real-time data processing. The feature involves integrating multiple Azure services and third-party APIs.

You need to create a strategy to ensure that the integration of these services does not introduce any performance issues or failures. You need to design the monitoring solution to detect and address potential issues

What should you do?

Select only one answer.

Create a single availability test in Application Insights to monitor the endpoint of the new feature.

**This answer is incorrect.**

Deploy a custom logging solution to capture and review logs manually at the end of each day.

Schedule nightly runs of Azure Automation runbooks to check the health of each service individually.

Use Live Metrics in Application Insights to observe the activity of the deployed application in real-time.

**This answer is correct.**

Option D is correct because Live Metrics provides real-time observation of the application's activity, allowing for immediate detection and response to performance issues. Option C is incorrect as nightly checks may not be sufficient for real-time data processing needs. Option A is incorrect because a single availability test does not provide comprehensive monitoring of all integrated services. Option B is incorrect as manual review of logs is not efficient for real-time monitoring and may delay the response to issues.

[Monitor app performance - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/monitor-app-performance)  
[Analyze metrics with Azure Monitor metrics explorer - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/analyze-metrics)

---
Question 49 of 50

An e-commerce platform is planning to expand its services globally. The platform is hosted on Azure and utilizes various Azure services and third-party integrations.

You need to design and create a robust monitoring solution that can scale with the expansion and provide insights into the performance of the platform across different regions.

What should you do?

Select only one answer.

Deploy multiple Application Insights instances for each region and use Azure Monitor to aggregate the data.

**This answer is correct.**

Implement a single Application Insights instance with default settings to monitor the entire platform.

Create web tests and alerts for each region within a single Application Insights instance.

Use manual instrumentation to log user activities and store them in Azure Blob Storage for later analysis.

Option A is correct because deploying multiple Application Insights instances for each region allows for localized monitoring, and using Azure Monitor to aggregate the data provides a centralized view of global performance. Option B is incorrect as a single instance may not scale effectively for global monitoring. Option D is incorrect because manual instrumentation and storage in Azure Blob Storage do not provide real-time monitoring and analysis capabilities. Option C is incorrect web tests and alerts are just part of a robust monitoring solution.

[Monitor app performance - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/monitor-app-performance)  
[Analyze metrics with Azure Monitor metrics explorer - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/analyze-metrics)

---
Question 50 of 50

A development team is using Application Insights to monitor their web application deployed on Azure. They have noticed discrepancies in the reported metrics due to high telemetry volume.

You need to ensure that the reported metrics accurately reflect the application's performance without being affected by telemetry sampling.

What should you implement to achieve this goal?

Select only one answer.

Configure Application Insights to use preaggregated standard metrics for dashboarding and real-time alerting.

**This answer is correct.**

Create a custom Kusto query in Application Insights to manually aggregate log-based metrics.

Disable all telemetry sampling in Application Insights to ensure all events are collected.

Increase the sampling rate in Application Insights to collect more data points for log-based metrics.

**This answer is incorrect.**

Preaggregated standard metrics are not affected by telemetry sampling and provide accurate real-time data, which makes them suitable for dashboarding and alerting. Increasing the sampling rate or disabling sampling altogether would increase costs and may still not provide accurate metrics due to the volume of data. Creating a custom Kusto query would require manual effort and does not address the issue of sampling affecting the metrics.

[Metrics in Application Insights - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/app-insights-metrics "Metrics in Application Insights - Training | Microsoft Learn")

[Discover log-based metrics - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/monitor-app-performance/3-logs-based-metrics "Discover log-based metrics - Training | Microsoft Learn")