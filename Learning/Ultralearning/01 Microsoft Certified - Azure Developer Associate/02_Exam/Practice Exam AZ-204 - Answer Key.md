# Azure Exam Answer Key

## Question 2

**Answer: A. Blob**

**Explanation:** The blob service is the only one that supports user delegation shared access signatures. The file service supports account and service shared access signatures. The queue service supports account and service shared access signatures. The table service supports account and service shared access signatures.

**Resource:** [Discover shared access signatures - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-shared-access-signatures/2-shared-access-signatures-overview)

---

## Question 3

**Answer: C. The container that is hosting blobs**

**Explanation:** The container that is hosting blobs is used for associating the corresponding stored access policies. The storage account can be associated with shared access signatures keys but not stored access policies. The blob service of the storage account can be associated with shared access signatures keys but not stored access policies. Each individual blob can be associated with shared access signatures keys but not stored access policies.

**Resource:** [Define a stored access policy](https://learn.microsoft.com/en-us/rest/api/storageservices/define-stored-access-policy)

---

## Question 4

**Answer: B. On-Behalf-Of**

**Explanation:** OAuth 2.0 On-Behalf-Of flow (OBO) is used when an application invokes a service or web API, which in turn needs to call another service or web API. The idea is to propagate the delegated user identity and permissions through the request chain. The OAuth 2.0 authorization code grant can be used in apps that are installed on a device to gain access to protected resources, such as web APIs. The OAuth 2.0 client credentials grant flow permits a web service (confidential client) to use its own credentials, instead of impersonating a user, to authenticate when calling another web service. Implicit is a redirection-based flow. The client must be capable of interacting with the resource owner's user-agent (typically a web browser). Authorization code, On-Behalf-Of, and implicit cannot be used to delegate user permission and identity.

**Resource:** [Implement authentication by using the Microsoft Authentication Library - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-authentication-by-using-microsoft-authentication-library/)

---

## Question 5

**Answer: C. App1 will have a single application object and multiple service principals**

**Explanation:** App1 will have a single application object and multiple service principals. App1 will not have multiple application objects, multiple application objects and a single service principal, or a single service principal.

**Resource:** [Explore service principals - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/explore-microsoft-identity-platform/3-app-service-principals)

---

## Question 6

**Answer: C. Microsoft Entra ID credentials assigned the Contributor role**

**Explanation:** Microsoft Entra ID credentials are required to generate the SAS token. The account used must have the Microsoft.Storage/storageAccounts/blobServices/generateUserDelegationKey permission, which is present in the following built-in roles: Contributor, Storage Account Contributor, Storage Blob Data Contributor, Storage Blob Data Owner, Storage Blob Data Reader, and Storage Blob Delegator. The account key can be used to generate the SAS token, but it can be more easily compromised.

**Resource:** [Discover shared access signatures - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-shared-access-signatures/2-shared-access-signatures-overview)

---

## Question 7

**Answer: B.**

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

**Explanation:** The code segment that includes `Resource = "c"` and `sasBuilder.SetPermissions(BlobContainerSasPermissions.Read);` will generate the shared access signatures token that grants the Read permission to a blob container. The code segment that includes resource = 'b' will generate a shared access signatures token at the blob level. The code segments that include `sasBuilder.SetPermissions(BlobContainerSasPermissions.Create);` will generate a shared access signatures token with the Create permission at the blob level.

**Resource:** [Store data in Azure learning path - Training | Microsoft Learn](https://learn.microsoft.com/training/paths/store-data-in-azure/)

---

## Question 8

**Answer: B. System-assigned managed identity**

**Explanation:** Managed identities for Azure resources eliminate the need to manage credentials in code. A system-assigned managed identity is restricted to one per resource and is tied to the lifecycle of the resource. Once enabled for app1, it will automatically create a service principal without the need to manage credentials and cannot be explicitly deleted.

A Microsoft Entra ID application is defined by its one and only application object, which resides in the Microsoft Entra ID tenant where the application was registered (known as the application's home tenant). It cannot be used by app1 to access a storage account without managing credentials. A user-assigned managed identity can be created and assigned to one or more instances of an Azure service. Once enabled for app1, a user-assigned managed identity will automatically create a service principal without the need to manage but will need to be explicitly deleted. The legacy service principal represents a legacy app, which is an app created before app registrations were introduced or an app created through legacy experiences. The legacy service principal cannot be used to access a storage account without managing credentials.

**Resource:** [Implement managed identities - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-managed-identities/)

---

## Question 9

**Answer: B. User-assigned managed identity**

**Explanation:** User-assigned managed identities are a way to reuse the permissions across applications. User-assigned managed identities associate the managed identity to the new applications, with no keys or passwords. System-assigned managed identities use a new identity for each application, which does not meet the common configuration requirement. A service principal has keys that need to be rotated. The developer does not run the application, so the developer's identity cannot be assumed.

**Resource:** [Implement Azure App Configuration - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-azure-app-configuration/)

---

## Question 10

**Answer: A. :**

**Explanation:** The colon character (:) is used to separate names of individual keys when creating a namespace hierarchy in Azure App Configuration. The asterisk character (*) is one of reserved characters in Azure App Configuration, so it cannot be used to separate names of individual keys when creating a namespace hierarchy in Azure App Configuration. The comma character (,) is one of reserved characters in Azure App Configuration, so it cannot be used to separate names of individual keys when creating a namespace hierarchy in Azure App Configuration. The backslash character (\) is one of reserved characters in Azure App Configuration, so it cannot be used to separate names of individual keys when creating a namespace hierarchy in Azure App Configuration.

**Resource:** [Create paired keys and values - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-azure-app-configuration/3-keys-values)

---

## Question 11

**Answer: D.**

```
az container create \
    --resource-group myResourceGroup \
    --name mycontainer \
    --image mycontainerimage \
    --restart-policy OnFailure
```

**Explanation:** If the –restart-policy is mentioned as OnFailure, the containers in the container group are restarted only when the process executed in the container fails (when it terminates with a nonzero exit code). If the –restart-policy is mentioned as Always, the containers in the container group are always restarted irrespective of the success or failure of process execution in a container. If the –restart-policy is mentioned as Never, the containers in the container group will only run at most once. The az container restart command is used to restart all the containers in a container group, not to define a restart policy for a container group.

**Resource:** [Run containerized tasks with restart policies](https://learn.microsoft.com/training/modules/create-run-container-images-azure-container-instances/4-run-containerized-tasks-restart-policies)

---

## Question 12

**Answer: A and D**

- A. Deploy the containerized application to Azure Container Apps
- D. Publish the application's image to Azure Container Registry

**Explanation:** Publishing the application's image to Azure Container Registry allows it to be easily accessed and deployed to Azure services. Azure Container Apps is a serverless container service that automatically scales and recovers from failures, making it suitable for applications with fluctuating workloads and high availability requirements. Running containers using Azure Container Instance does not provide automatic scaling or recovery from failures. Azure Blob Storage is not designed for storing container images.

**Resources:**

- [Implement Azure Container Apps - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/implement-azure-container-apps/)
- [Manage container images in Azure Container Registry - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/publish-container-image-to-azure-container-registry/)

---

## Question 13

**Answer: D. Use the `az containerapp up` command with the `--source .` parameter**

**Explanation:** The `az containerapp up` command with the `--source .` parameter builds and deploys the container app using the Dockerfile in the root of the repository. The other options either do not exist or do not fulfill the requirement.

**Resource:** [Quickstart: Build and deploy from local source code to Azure Container Apps - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/container-apps/quickstart-code-to-cloud?tabs=bash%2Ccsharp)

---

## Question 14

**Answer: A and B**

- A. `"WEBSITE_LOCAL_CACHE_OPTION": "Always"`
- B. `"WEBSITE_LOCAL_CACHE_SIZEINMB": "1500"`

**Explanation:** By using `WEBSITE_LOCAL_CACHE_OPTION = Always`, local cache will be enabled. `WEBSITE_LOCAL_CACHE_SIZEINMB` will properly configure Local Cache with 1.5 GB of size. `WEBSITE_LOCAL_CACHE_OPTION = Enable` is not a valid value. `1.5` will not configure 1.5 GB for the local cache.

**Resource:** [Configure web app settings - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-web-app-settings/)

---

## Question 15

**Answer: A. `WEBSITE_LOAD_CERTIFICATES`**

**Explanation:** The `WEBSITE_LOAD_CERTIFICATES` app setting makes the specified certificates accessible to Windows or Linux custom containers as files. The `WEBSITE_ROOT_CERTS_PATH` app setting is read-only and does not allow comma-separated thumbprint values to be mentioned to the certificates and then be loaded in the code. The `WEBSITE_AUTH_TOKEN_CONTAINER_SASURL` app setting is used to instruct the auth module to store and load all encrypted tokens to the specified blob storage container. This setting is used for Azure Storage and cannot be used to load certificates inside a Windows custom container.

**Resource:** [Configure web app settings - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-web-app-settings/)

---

## Question 16

**Answer: D. ARR Affinity**

**Explanation:** In a multi-instance deployment, the ARR Affinity setting ensures a client application is routed to the same instance for the life of the session. WebSocket is a standardized protocol that provides full-duplex communication. Always on keeps the app loaded even when there is no traffic. In HTTP/2, a persistent connection can be used to service multiple simultaneous requests. WebSocket, Always on, and HTTP version are not used to ensure a client application is routed to the same instance for the life of the session.

**Resource:** [Configure web app settings - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-web-app-settings/)

---

## Question 17

**Answer: A. Deployment slots**

**Explanation:** Deployment slots are live apps with unique host names, which allow swapping configuration and content between them. Auto-scaling is a feature that allows adding more capacity to an Azure Functions app hosting environment. This capacity can be added to an individual hosting environment (for example, scaling up or adding memory or CPU), or adding more hosts (scaling out). The scaling can be triggered based on a schedule or when breaching thresholds defined for certain metrics. Hybrid connections are available for consuming on-premises apps without needing to expose them to the internet. App cloning is a process to obtain an existing app and copy it to another destination, which can be a new app or a deployment slot, for example. However, this is not supported on Linux apps.

**Resources:**

- [Explore staging environments - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/understand-app-service-deployment-slots/2-app-service-staging-environments)
- [Discover App Service networking features - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/introduction-to-azure-app-service/6-network-features)
- [Examine Azure App Service plans - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/introduction-to-azure-app-service/3-azure-app-service-plans)

---

## Question 18

**Answer: B. Purchase an App Service certificate**

**Explanation:** Purchasing an App Service certificate automates the process of requesting, renewing, and synchronizing the certificate with the App Service apps that use them. Free App Service certificates offer basic functionalities and cannot be exported. Obtaining the certificate from a third party and uploading it to Azure App Service is also an option but lacks the automation and integration offered by the App Service certificates. It is recommended to store certificates in and retrieve them from a Key Vault, but if they are obtained from a third party, the renewal and synchronization with the App Service apps need to be automated in other ways.

**Resource:** [Configure security certificates - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-web-app-settings/6-configure-security-certificates)

---

## Question 19

**Answer: C. Consumption**

**Explanation:** The Consumption hosting plan satisfies all requirements. It supports autoscaling, has event-based scaling behavior, and provides a serverless pricing model. The App Service, App Service Environment, and Functions Premium hosting plans support autoscaling but does not provide the serverless pricing model. Its scaling behavior is not event based but performance based.

**Resource:** [Compare Azure Functions hosting options - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/explore-azure-functions/3-compare-azure-functions-hosting-options)

---

## Question 20

**Answer: B. `@Microsoft.KeyVault(SecretName=MyConnection;VaultName=MyVault)`**

**Explanation:** The code segment `@Microsoft.KeyVault(SecretName=MyConnection;VaultName=MyVault)` segment reads the secret from Key Vault. The code segment that includes `Secret` uses an invalid parameter. The code segment that includes `Secret` and `Vault` use invalid parameters. The code segment that includes `SecretName` and `Vault` use invalid parameters.

**Resource:** [Create serverless applications learning path - Training | Microsoft Learn](https://learn.microsoft.com/training/paths/create-serverless-applications/)

---

## Question 21

**Answer: A. Create a function.json file for each function**

**Explanation:** When using scripting languages, such as C# script, the function.json file for each function contains its triggers and bindings, and it needs to be explicitly created. The file host.json has runtime-specific configurations, not definitions of triggers and bindings. Decorating methods and Decorating parameters are used to define triggers and bindings when using compiled languages, not scripted ones.

**Resource:** [Create triggers and bindings - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/develop-azure-functions/3-create-triggers-bindings)

---

## Question 22

**Answer: B and C**

- B. The Premium plan
- C. Fan-out/fan-in pattern

**Explanation:** The Premium plan avoids cold starts and offers unlimited execution duration. The fan-out/fan-in pattern enables multiple functions to be executed in parallel, waiting for all functions to finish. Often, some aggregation work is done on the results that are returned from the functions. The Consumption plan avoids paying for idle time but might face cold starts. Furthermore, each function run is limited to 10 minutes. The function chaining pattern is a sequence of functions that execute in a specific order. In this pattern, the output of one function is applied to the input of another function.

**Resource:** [AZ-204: Implement Azure Functions - Training | Microsoft Learn](https://learn.microsoft.com/training/paths/implement-azure-functions/)

---

## Question 23

**Answer: A. `[TimerTrigger("0 */15 * * * 1-5")]`**

**Explanation:** The code segment that includes `Run([TimerTrigger("0 */15 * * * 1-5")` executes the function every 15 minutes from Monday to Friday. The code segment that includes `Run([TimerTrigger("*/15 * * * 0-4")` is missing the second part, and it is not using the proper range for days of the week. The code segment that includes `Run([TimerTrigger("0 15 * * * ")` executes only once at 15:00 (3 PM). The code segment that includes `Run([TimerTrigger("* 15 * * 1-5")` is missing the seconds attribute and the step ('/') part for the minutes.

**Resources:**

- [Execute an Azure Function with triggers - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/execute-azure-function-with-triggers/)
- [Timer trigger for Azure Functions - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-timer?tabs=python-v2%2Cisolated-process%2Cnodejs-v4&pivots=programming-language-csharp)

---

## Question 24

**Answer: B. 10**

**Explanation:** Imposing limits on the scaling out capacity of an Azure Functions app can help when the app connects to components that have limited throughput. The `functionAppScaleLimit` property lets you define the number of instances of the Azure Functions app that will be created. Therefore, setting it to a low value, such as 10, is appropriate in this scenario. Azure Functions apps in the Consumption plan can scale out and have 200 instances as a default. A value of 0 or null for the `functionAppScaleLimit` property means that an unrestricted number of instances of the Azure Functions app will be created.

**Resource:** [Scale Azure Functions - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/explore-azure-functions/4-scale-azure-functions)

---

## Question 25

**Answer: C and D**

- C. Set the 'maxConcurrentRequests' property in the host.json file to limit the number of parallel executions
- D. Set the 'maxOutstandingRequests' property in the host.json file to limit the number of outstanding requests at any given time

**Explanation:** Setting the 'maxConcurrentRequests' property in the host.json file will limit the number of HTTP functions that are executed in parallel, which can help manage resource utilization and avoid exceeding the rate limit of the third-party service. The 'maxOutstandingRequests' property limits the number of outstanding requests that are held at any given time, including queued requests and in-progress executions, which can also help manage resource utilization. Enabling 'dynamicThrottlesEnabled' property would not help in this scenario as it rejects requests based on system performance counters, not based on the rate limit of a third-party service. The 'hsts' property is used to enforce HTTP Strict Transport Security (HSTS) behavior and is not related to managing resource utilization or rate limiting. The 'routePrefix' property is used to set the route prefix for all routes and does not affect resource utilization or rate limiting.

**Resource:** [Azure Functions HTTP triggers and bindings overview - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook?tabs=isolated-process%2Cfunctionsv2&pivots=programming-language-csharp)

---

## Question 26

**Answer: A and B**

- A. Azure Functions with an Azure Cosmos DB trigger
- B. Change feed processor library

**Explanation:** Azure Functions with an Azure Cosmos DB trigger allows you to select the container to connect, and the Azure Function is triggered whenever there is a change in the container. The change feed processor library follows the observer pattern, where the processing function is called by the library. The change feed processor library will automatically check for changes and, if changes are found, push them to the client. Azure Functions with an Event Grid trigger will execute the function when an Event Grid event is dispatched. It has no relationship with an Azure Cosmos DB change feed. A change feed pull model will use a pull model rather than a push model.

**Resources:**

- [Consume an Azure Cosmos DB for NoSQL change feed using the SDK - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/consume-azure-cosmos-db-sql-api-change-feed-use-sdk/)
- [Handle events with Azure Functions and Azure Cosmos DB for NoSQL change feed - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/handle-events-azure-functions-azure-cosmos-db-sql-api-change-feed/)

---

## Question 27

**Answer: C and E**

- C. `partitionKey`
- E. `id`

**Explanation:** The `ReadItemAsync` method of the container class of .NET SDK for Azure Cosmos DB has two mandatory parameters: `partitionKey` and `itemId`. The `consistencyLevel` parameter is part of the optional `requestOptions` parameter of the `ReadItemAsync`. The `eTag` and `sessionToken` parameters are part of the optional `requestOptions` parameter of the `ReadItemAsync` method.

**Resource:** [Explore Microsoft .NET SDK v3 for Azure Cosmos DB - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/work-with-cosmos-db/2-cosmos-db-dotnet-overview)

---

## Question 28

**Answer: C. Lease container**

**Explanation:** The lease container component serves as a storage mechanism to manage state across multiple change feed consumers. The delegate component is the code within the client application that implements business logic for each batch of changes. The compute instance is a client application instance that listens for changes from the change feed. The monitored container component is monitored for any insert or update operations. It does not serve as a storage mechanism to manage state across multiple change feed consumers.

**Resource:** [Understand change feed features in the SDK - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/consume-azure-cosmos-db-sql-api-change-feed-use-sdk/2-understand-features-sdk)

---

## Question 29

**Answer: B. Delegate**

**Explanation:** The delegate component can be used to define custom logic to process the changes that the change feed reads. The monitored container has the data from which the change feed is generated. The compute instance hosts the change feed processor to listen for changes. It can be represented by a VM, a Kubernetes pod, an Azure App Service instance, or an actual physical machine. The lease container acts as a state storage and coordinates the processing of the change feed across multiple workers.

**Resource:** [Understand change feed features in the SDK](https://learn.microsoft.com/training/modules/consume-azure-cosmos-db-sql-api-change-feed-use-sdk/2-understand-features-sdk)

---

## Question 30

**Answer: C. Use metadata headers defined with a PUT request**

**Explanation:** Metadata is the proper way to define this kind of data, allowing independent modification and supporting up to 8 KB in total size. The HTTP verb to define metadata is a PUT, and this is the correct format to define metadata values. The maximum size of a blob name is 1,024 characters. Also, this is not an optimal approach because metadata can be obtained and set independently, maintaining the same file name. Metadata is the proper way to define this kind of data, allowing independent modification and supporting up to 8 KB in total size. But the HTTP verb to define metadata is a PUT, not POST. The combination of locations and weather types can be potentially unlimited, and container names are limited to 63 characters.

**Resource:** [AZ-204: Develop solutions that use Blob storage - Training | Microsoft Learn](https://learn.microsoft.com/training/paths/develop-solutions-that-use-blob-storage/)

---

## Question 31

**Answer: D.**

```
byte[] data;
BlobClientOptions options = new BlobClientOptions();
options.Retry.MaxRetries = 10;
options.Retry.Delay = TimeSpan.FromSeconds(20);
BlobClient client = new BlobClient(new Uri("https://mystorageaccount.blob.core.windows.net/containers/blob.txt"), options);
Response<BlobDownloadResult> response = client.DownloadContent();
data = response.Value.Content.ToArray();
```

**Explanation:** The code segment that includes `options.Retry.MaxRetries = 10;` and `options.Retry.Delay = TimeSpan.FromSeconds(20);` defines the retry strategy and downloads the content to the variable data. The code segments that do not include these parameters do not define the retry strategy.

**Resource:** [Azure Fundamentals: Describe Azure architecture and services - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/paths/azure-fundamentals-describe-azure-architecture-services/)

---

## Question 32

**Answer: C. A container name**

**Explanation:** When creating a prefixMatch filter rule for an Azure storage lifecycle policy for block blobs, the first element of the prefix string must be a container name not a block blob index tag, block blob name, or storage account name.

**Resource:** [Discover Blob storage lifecycle policies - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/manage-azure-blob-storage-lifecycle/3-blob-storage-lifecycle-policies)

---

## Question 33

**Answer: D. A blob in the Cool tier in the same region**

**Explanation:** Blobs in the Archive tier can be rehydrated only to online tiers (that is, Cool or Hot). The destination can be any storage account in the same region.

**Resource:** [Rehydrate blob data from the archive tier - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/manage-azure-blob-storage-lifecycle/5-rehydrate-blob-data)

---

## Question 34

**Answer: B. Define a subscription with product scope**

**Explanation:** When creating a product, several APIs can be added to the product and a subscription can be associated with it. Access should not be granted to all APIs. Developer access should be granted regardless of the caller IP. A client certificate would require a policy to validate the certificate and specific logic to map the client to specific APIs.

**Resource:** [Secure APIs by using subscriptions - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/explore-api-management/6-secure-access-api-subscriptions)

---

## Question 35

**Answer: B. Policy**

**Explanation:** API publishers can change API behavior through configuration using policies. Policies are a collection of statements that run sequentially on the request or response of an API. A product has one or more APIs, a usage quota, and the terms of use and cannot be used to restrict the number of API calls. Subscriptions are the most common way for API consumers to access APIs published through an API Management instance. API is a representation of a back-end API and needs to be configured with a policy to implement a rate limit.

**Resource:** [How Azure API Management Works - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/introduction-to-azure-api-management/3-how-azure-api-management-works)

---

## Question 36

**Answer: A and D**

- A. Configure a validate-jwt policy to authenticate incoming requests
- D. Set up a rate limit by key policy to enforce call quotas

**Explanation:** Configuring a validate-jwt policy is necessary to authenticate users with OAuth 2.0. Setting up a rate limit by key policy helps enforce usage quotas. IP filtering does not address the authentication and quota requirements. Deploying an Azure Application Gateway is not required for these specific needs.

**Resources:**

- [Quickstart: Create a new Azure API Management instance by using the Azure CLI](https://learn.microsoft.com/en-us/azure/api-management/get-started-create-service-instance-cli)
- [Authentication and authorization to APIs in Azure API Management](https://learn.microsoft.com/en-us/azure/api-management/authentication-authorization-overview)

---

## Question 37

**Answer: C. `az eventhubs eventhub update --resource-group MyResourceGroupName --namespace-name MyNamespaceName --name MyEventHubName --partition-count 12`**

**Explanation:** The code segment that includes `az eventhubs eventhub update` adds partitions to an existing event hub. The code segment that includes `az eventhubs eventhub consumer-group update` updates the event hub consumer group. The code segment that includes `az eventhubs eventhub consumer-group create` will create an event hub consumer group. The code segment that includes `az eventhubs eventhub create --resource-group` segment will create an event hub with partitions, not change an existing one.

**Resource:** [Control Azure services with the CLI - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/control-azure-services-with-cli/)

---

## Question 38

**Answer: A, B, and E**

- A. Azure Blob storage
- B. Azure Data Lake Storage Gen1
- E. Azure Data Lake Storage Gen2

**Explanation:** Azure Event Hubs Capture can automatically deliver the streaming data in Event Hubs to Azure Blob storage. Azure Event Hubs Capture can automatically deliver the streaming data in Event Hubs to Azure Data Lake Storage Gen1. Azure Event Hubs Capture can automatically deliver the streaming data in Event Hubs to Azure Data Lake Storage Gen2. Azure Functions and Azure Stream Analytics cannot be used to capture events from Azure Event Hubs.

**Resource:** [Explore Azure Event Hubs - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/azure-event-hubs/)

---

## Question 39

**Answer: C. Message sessions**

**Explanation:** To provide FIFO guarantees in Service Bus, sessions must be configured. Message sessions enable exclusive, ordered handling of unbounded sequences of related messages. A dead-letter queue holds messages that cannot be delivered to any receiver. Message deferral makes it possible to defer retrieval of a message until a later time. Scheduled delivery allows submitting messages to a queue or topic for delayed processing. A dead-letter queue, message deferral, and scheduled delivery do not provide FIFO guarantees.

**Resource:** [Explore Azure Service Bus - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/discover-azure-message-queue/3-azure-service-bus-overview)

---

## Question 40

**Answer: C. Create a new topic with a default time to live of 15 minutes. Send the messages to this topic**

**Explanation:** To avoid affecting existing applications, the time to live of the existing topic must not be changed. A new topic needs to be created. Changing the topic's default time to live will affect other applications. A message-level time to live cannot be higher than the topic's time to live. To avoid affecting existing applications, the time to live of the existing topic or queue must not be changed.

**Resource:** [Exercise: Send and receive message from a Service Bus queue by using .NET. - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/discover-azure-message-queue/6-send-receive-messages-service-bus)

---

## Question 41

**Answer: A, B, and D**

- A. SQL
- B. Boolean
- D. Correlation

**Explanation:** A SqlFilter holds a SQL-like conditional expression that is evaluated in the broker against the arriving message's user-defined properties and system properties. The TrueFilter and FalseFilter either cause all arriving messages (true) or none of the arriving messages (false) to be selected for the subscription. A CorrelationFilter holds a set of conditions that are matched against one or more of an arriving message's user and system properties. Size Filter and Content are not valid options for Service Bus topic filtering.

**Resource:** [Implement message-based communication workflows with Azure Service Bus - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-message-workflows-with-service-bus/)

---

## Question 42

**Answer: B. Multicast request/reply**

**Explanation:** A publisher can send a message into a topic and multiple subscribers can become eligible to consume the message. A publisher can send a message into a queue and expect a reply from the message consumer, but multiple subscribers cannot consume the message. This session feature enables multiplexing of streams of related messages through a single queue but cannot be consumed by multiple subscribers. This session feature enables multiplexed replies, allowing several publishers to share a reply queue, but a message cannot be consumed by multiple subscribers.

**Resource:** [Explore Service Bus message payloads and serialization - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/discover-azure-message-queue/5-messages-payloads-serialization)

---

## Question 43

**Answer: B. PeekMessages**

**Explanation:** Messages can be peeked at in the queue without removing them from the queue by calling the PeekMessages method of the QueueClient class. The Peek method of the QueueClient class is used with Azure Service Bus, not Azure Queue Storage. The ReceiveMessages method of the QueueClient class removes them from the queue. The ReceiveMessageAsync method of the QueueClient class is used with Azure Service Bus, not Azure Queue Storage.

**Resource:** [Create and manage Azure Queue Storage and messages by using .NET - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/discover-azure-message-queue/8-queue-storage-code-examples)

---

## Question 44

**Answer: A. Azure Service Bus Premium tier**

**Explanation:** Service Bus detects duplicate messages. The Premium tier is required to send messages larger than 256 KB. Although Service Bus detects duplicate messages, the Standard tier only supports messages that are up to 256 KB in size. Azure Storage queues do not support duplicate message detection.

**Resource:** [Explore Azure Service Bus - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/discover-azure-message-queue/3-azure-service-bus-overview)

---

## Question 45

**Answer: C. Azure Service Bus dead-letter queue**

**Explanation:** Azure Service Bus dead-letter queue is designed to hold messages that cannot be delivered to any receiver or are not processed successfully, which is suitable for the company's requirement. Azure Storage queues with visibility timeout only hide messages temporarily and do not move them to separate storage. Azure Event Grid with advanced filtering is for event routing, not for handling failed message processing. Azure Queue Storage with message expiration simply deletes expired messages rather than moving them for analysis.

**Resources:**

- [Discover Azure message queues - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/discover-azure-message-queue)
- [Storage queues and Service Bus queues - compared and contrasted - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted)

---

## Question 46

**Answer: C and D**

- C. Azure Service Bus with duplicate detection
- D. Azure Service Bus with sessions enabled

**Explanation:** Azure Service Bus with sessions enabled allows for FIFO processing by using sessions to ensure that related messages are handled in the order they are received. Duplicate detection helps to ensure that the system does not process the same transaction more than once. Azure Queue Storage does not guarantee FIFO processing as it does not support sessions, and visibility timeout only hides the message temporarily from other consumers. Azure Event Grid is an event routing service and does not provide FIFO guarantees or message sessions.

**Resources:**

- [Discover Azure message queues - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/discover-azure-message-queue)
- [What is Azure Service Bus? - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview)

---

## Question 47

**Answer: C. Implement Application Insights web tests and alerts**

**Explanation:** Application Insights allows you to create web tests that simulate user interactions with your application and then set up alerts based on the results of these tests. Azure Monitor Resource Health alerts are used for infrastructure monitoring, not application performance. Azure Service Health provides information about Azure service issues and planned maintenance, not application performance. Azure Advisor provides best practice recommendations, not application performance alerts.

**Resource:** [Monitor app performance - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/monitor-app-performance/)

---

## Question 48

**Answer: D. Use Live Metrics in Application Insights to observe the activity of the deployed application in real-time**

**Explanation:** Option D is correct because Live Metrics provides real-time observation of the application's activity, allowing for immediate detection and response to performance issues. Option C is incorrect as nightly checks may not be sufficient for real-time data processing needs. Option A is incorrect because a single availability test does not provide comprehensive monitoring of all integrated services. Option B is incorrect as manual review of logs is not efficient for real-time monitoring and may delay the response to issues.

**Resources:**

- [Monitor app performance - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/monitor-app-performance)
- [Analyze metrics with Azure Monitor metrics explorer - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/analyze-metrics)

---

## Question 49

**Answer: A. Deploy multiple Application Insights instances for each region and use Azure Monitor to aggregate the data**

**Explanation:** Option A is correct because deploying multiple Application Insights instances for each region allows for localized monitoring, and using Azure Monitor to aggregate the data provides a centralized view of global performance. Option B is incorrect as a single instance may not scale effectively for global monitoring. Option D is incorrect because manual instrumentation and storage in Azure Blob Storage do not provide real-time monitoring and analysis capabilities. Option C is incorrect web tests and alerts are just part of a robust monitoring solution.

**Resources:**

- [Monitor app performance - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/monitor-app-performance)
- [Analyze metrics with Azure Monitor metrics explorer - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/analyze-metrics)

---

## Question 50

**Answer: A. Configure Application Insights to use preaggregated standard metrics for dashboarding and real-time alerting**

**Explanation:** Preaggregated standard metrics are not affected by telemetry sampling and provide accurate real-time data, which makes them suitable for dashboarding and alerting. Increasing the sampling rate or disabling sampling altogether would increase costs and may still not provide accurate metrics due to the volume of data. Creating a custom Kusto query would require manual effort and does not address the issue of sampling affecting the metrics.

**Resources:**

- [Metrics in Application Insights - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/app-insights-metrics)
- [Discover log-based metrics - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/monitor-app-performance/3-logs-based-metrics)