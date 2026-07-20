# Azure Exam Practice Questions

## Question 2

You plan to use a shared access signature to protect access to services within a general-purpose v2 storage account.

You need to identify the type of service that you can protect by using the user delegation shared access signature.

Which service should you identify?

A. Blob  
B. File  
C. Queue  
D. Table

---

## Question 3

You have blobs in an Azure storage account.

You need to implement a stored access policy that will apply to shared access signatures generated for the blobs.

To which type of storage resource should you associate the policy?

A. The storage account  
B. The blob service of the storage account  
C. The container that is hosting blobs  
D. Each individual blob

---

## Question 4

You manage a Microsoft Entra ID registered application named **app1**. App1 calls a web API, which then calls Microsoft Graph.

You need to ensure the signed-in user identity is delegated through the request chain.

Which authentication flow should you use?

A. Authorization code  
B. On-Behalf-Of  
C. Client credentials  
D. Implicit

---

## Question 5

You develop a multitenant web application named **App1**. You plan to register App1 with multiple Microsoft Entra ID tenants.

You need to identify the relationship between the application objects and security principals associated with App1.

Which relationship should you identify?

A. App1 will have multiple application objects and multiple service principals  
B. App1 will have multiple application objects and a single service principal  
C. App1 will have a single application object and multiple service principals  
D. App1 will have a single application object and a single service principal

---

## Question 6

You plan to generate a shared access signature (SAS) token for read access to a blob in a storage account.

You need to secure the token from being compromised.

What should you use?

A. Primary account key  
B. Secondary account key  
C. Microsoft Entra ID credentials assigned the Contributor role  
D. Microsoft Entra ID credentials assigned the Reader role

---

## Question 7

You need to generate a shared access signature token that grants the Read permission to a blob container.

Which code segment should you use?

A.

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

B.

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

C.

```
BlobSasBuilder sasBuilder = new BlobSasBuilder()
{
    BlobContainerName = containerClient.Name,
    Resource = "c"
};
sasBuilder.ExpiresOn = DateTimeOffset.UtcNow.AddHours(1);
sasBuilder.SetPermissions(BlobContainerSasPermissions.Create);
Uri sasUri = containerClient.GenerateSasUri(sasBuilder);
```

D.

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

---

## Question 8

You manage an Azure App Service Functions app named **app1** and a storage account named **account1**.

You have the following requirements:

- App1 should access account1 without managing credentials
- The service principal associated with app1 cannot be explicitly deleted

You need to configure a security principal for app1.

Which security principal should you use?

A. Application  
B. System-assigned managed identity  
C. User-assigned managed identity  
D. Legacy

---

## Question 9

You have 10 applications running in Azure App Service.

You need to ensure the applications have access to items stored in Azure App Configuration by using a common configuration. Passwords or keys must not be used.

Which solution should you use?

A. System-assigned managed identities  
B. User-assigned managed identity  
C. Service principal with permissions to Azure App Configuration  
D. Developer's credentials in code

---

## Question 10

You plan to create a key namespace hierarchy in Azure App Configuration.

You need to separate individual key names.

Which character should you use?

A. :  
B. *  
C. ,  
D. \

---

## Question 11

A container group in Azure Container Instances has multiple containers.

The containers must restart when the process executed in the container group terminates due to an error.

You need to define the restart policy for the container group.

Which Azure CLI command should you use?

A.

```
az container restart \
    --name mycontainer \
    --resource-group myResourceGroup \
    --no-wait
```

B.

```
az container create \
    --resource-group myResourceGroup \
    --name mycontainer \
    --image mycontainerimage \
    --restart-policy Always
```

C.

```
az container create \
    --resource-group myResourceGroup \
    --name mycontainer \
    --image mycontainerimage \
    --restart-policy Never
```

D.

```
az container create \
    --resource-group myResourceGroup \
    --name mycontainer \
    --image mycontainerimage \
    --restart-policy OnFailure
```

---

## Question 12

Your company is developing a new web application that will be deployed as a containerized solution on Azure. The application is expected to have fluctuating workloads and needs to be highly available.

You need to create a solution that allows the application to scale based on demand and recover from failures automatically.

Each correct answer presents part of the solution. Which two actions should you perform? (Choose two.)

A. Deploy the containerized application to Azure Container Apps  
B. Store the application's images in Azure Blob Storage  
C. Deploy the containerized application to Azure Container Instance  
D. Publish the application's image to Azure Container Registry

---

## Question 13

Your company is developing an application that includes a backend web API service. The development team has decided to use Azure Container Apps to host the API. They have a Dockerfile in the root of their repository that defines the containerized app.

You need to deploy the container app using the Dockerfile.

What should you do?

A. Use the `az containerapp env create` command with the `--name` parameter  
B. Use the `az containerapp create` command with the `--image` parameter  
C. Use the `az containerapp create` command with the `--containername` parameter  
D. Use the `az containerapp up` command with the `--source .` parameter

---

## Question 14

You develop a web application hosted on the Web Apps feature of Microsoft Azure App Service.

You need to enable and configure Azure Web Service Local Cache with 1.5 GB.

Which two code segments should you use? Each correct answer presents part of the solution.

A. `"WEBSITE_LOCAL_CACHE_OPTION": "Always"`  
B. `"WEBSITE_LOCAL_CACHE_SIZEINMB": "1500"`  
C. `"WEBSITE_LOCAL_CACHE_OPTION": "Enable"`  
D. `"WEBSITE_LOCAL_CACHE_SIZEINMB": "1.5"`

---

## Question 15

You plan to develop an Azure App Service web app named **app1** by using a Windows custom container.

You need to load a TLS/SSL certificate in application code.

Which app setting should you configure?

A. `WEBSITE_LOAD_CERTIFICATES`  
B. `WEBSITE_ROOT_CERTS_PATH`  
C. `WEBSITE_CORS_ALLOWED_ORIGINS`  
D. `WEBSITE_AUTH_TOKEN_CONTAINER_SASURL`

---

## Question 16

You manage a multi-instance deployment of an Azure App Service web app named **app1**.

You need to ensure a client application is routed to the same instance for the life of the session.

Which platform setting should you use?

A. WebSocket  
B. Always on  
C. HTTP version  
D. ARR Affinity

---

## Question 17

You are developing a Linux web app on Azure App Service.

You need to deploy the web app to the production environment based on the following requirements:

- App changes must be validated in an environment identical to the production environment before moving the app to the production environment
- Downtime must be eliminated when the app is deployed to the production environment

What should you use?

A. Deployment slots  
B. Auto-scaling  
C. Hybrid connection  
D. App cloning

---

## Question 18

A company has an App Service web app that requires a TLS/SSL certificate. The certificate will be used in other App Service apps. The certificate must be automatically renewed with the least management overhead.

You need to add the certificate.

What should you do?

A. Create a free App Service managed certificate  
B. Purchase an App Service certificate  
C. Upload a certificate from a third party  
D. Import a certificate from a Key Vault

---

## Question 19

You plan to create an Azure Functions app named **app1**.

You need to ensure that app1 will satisfy the following requirements:

- Supports automatic scaling
- Has event-based scaling behavior
- Provides a serverless pricing model

Which hosting plan should you use?

A. App Service  
B. App Service Environment  
C. Consumption  
D. Functions Premium

---

## Question 20

You have an Azure Key Vault named **MyVault**.

You need to change the Azure App Service settings by using a key vault reference to access a secret named **MyConnection** from MyVault.

Which code segment should you use?

A. `@Microsoft.KeyVault(Secret=MyConnection;VaultName=MyVault)`  
B. `@Microsoft.KeyVault(SecretName=MyConnection;VaultName=MyVault)`  
C. `@Microsoft.KeyVault(Secret=MyConnection;Vault=MyVault)`  
D. `@Microsoft.KeyVault(SecretName=MyConnection;Vault=MyVault)`

---

## Question 21

You plan to create a C# script-based Azure Functions app.

You need to configure the trigger and bindings for the functions of the Azure Functions app.

What should you do?

A. Create a function.json file for each function  
B. Create a host.json file for the Azure Functions app  
C. Decorate methods of each function with C# attributes  
D. Decorate parameters of each function with C# attributes

---

## Question 22

A company plans to create an Azure Functions app.

You need to recommend a solution that meets the following requirements:

- Executes multiple functions concurrently
- Performs aggregation on the results from the functions
- Avoids cold starts
- Minimizes costs

Which two components should you recommend? Each correct answer presents part of the solution

A. The Consumption plan  
B. The Premium plan  
C. Fan-out/fan-in pattern  
D. Function chaining pattern

---

## Question 23

You create a batch routine by using a timer trigger in Azure Functions.

You need to configure the batch routine to execute every 15 minutes, from Monday through Friday.

Which code segment should you use?

A. `[TimerTrigger("0 */15 * * * 1-5")]`  
B. `[TimerTrigger("*/15 * * * 0-4")]`  
C. `[TimerTrigger("0 15 * * * ")]`  
D. `[TimerTrigger("* 15 * * 1-5")]`

---

## Question 24

You are developing an Azure Functions app that will be deployed to a Consumption plan. The app consumes data from a database server that has limited throughput.

You need to use the `functionAppScaleLimit` property to control the number of instances of the app that will be created.

Which value should you use for the property setting?

A. 0  
B. 10  
C. null

---

## Question 25

You are a developing a serverless API using Azure Functions. The API is expected to handle a large number of HTTP requests and make outbound requests to a third-party service. The third-party service has a rate limit on the number of requests it can handle per minute.

You need to ensure that the Azure Function does not exceed the rate limit of the third-party service and manage resource utilization effectively.

Each correct answer presents part of the solution. Which two actions should you perform?

A. Enable 'dynamicThrottlesEnabled' property in the host.json file to reject requests with a 429 'Too Busy' response when system performance counters are over a high threshold  
B. Enable 'hsts' property in the host.json file to enforce HTTP Strict Transport Security (HSTS) behavior  
C. Set the 'maxConcurrentRequests' property in the host.json file to limit the number of parallel executions  
D. Set the 'maxOutstandingRequests' property in the host.json file to limit the number of outstanding requests at any given time  
E. Set the 'routePrefix' property in the host.json file to an empty string to remove the default prefix

---

## Question 26

You need to read an Azure Cosmos DB change feed by using a push model.

Which two components can you use to achieve this goal? Each correct answer presents a complete solution.

A. Azure Functions with an Azure Cosmos DB trigger  
B. Change feed processor library  
C. Azure Functions with an Azure Event Grid trigger  
D. Change feed pull model

---

## Question 27

You manage an Azure Cosmos DB container named **container1**.

You need to use the `ReadItemAsync` method to read an item from the Azure Cosmos service.

Which two parameters should you provide? Each correct answer presents part of the solution.

A. `consistencyLevel`  
B. `eTag`  
C. `partitionKey`  
D. `sessionToken`  
E. `id`

---

## Question 28

You plan to implement a storage mechanism for managing state across multiple change feed consumers.

You need to configure the change feed processor in the .NET SDK for Azure Cosmos DB for NoSQL API.

Which component should you use?

A. Delegate  
B. Compute instance  
C. Lease container  
D. Monitored container

---

## Question 29

You manage the deployment of an Azure Cosmos DB account.

You must define custom logic by using the .NET SDK change feed processor to process changes that the change feed reads.

You need to select the appropriate change feed processor component.

Which component should you use?

A. Monitored container  
B. Delegate  
C. Compute instance  
D. Lease container

---

## Question 30

You have blobs in Azure Blob storage. The blobs store pictures.

You need to record the location and weather condition information from when the pictures were taken. You must ensure you can use up to 2,000 characters when recording the information.

What should you do?

A. Append a suffix to the blob name by using the location and weather. Add a delimiter between them  
B. Use metadata headers defined with a POST request  
C. Use metadata headers defined with a PUT request  
D. Create one container for each location. Inside each container, define the blob name as the weather type and a random suffix

---

## Question 31

You need to download blob content to a byte array by using an operation that automatically recovers from transient failures.

Which code statement should you use?

A.

```
byte[] data;
BlobClient client = new BlobClient(new Uri("https://mystorageaccount.blob.core.windows.net/containers/blob.txt"), null);
Response<BlobDownloadResult> response = client.DownloadContent(data);
```

B.

```
BlobRequestOptions optionsWithRetryPolicy = new BlobRequestOptions();
byte[]destinationArray = blob.DownloadContent(index: 0, accessCondition: null, options: optionsWithRetryPolicy);
```

C.

```
byte[] data;
BlobClient client = new BlobClient(new Uri("https://mystorageaccount.blob.core.windows.net/containers/blob.txt"), null);
Response<BlobDownloadResult> response = client.DownloadContent();
data = response.Value.Content.ToArray();
```

D.

```
byte[] data;
BlobClientOptions options = new BlobClientOptions();
options.Retry.MaxRetries = 10;
options.Retry.Delay = TimeSpan.FromSeconds(20);
BlobClient client = new BlobClient(new Uri("https://mystorageaccount.blob.core.windows.net/containers/blob.txt"), options);
Response<BlobDownloadResult> response = client.DownloadContent();
data = response.Value.Content.ToArray();
```

---

## Question 32

You have an Azure storage lifecycle policy for block blobs.

You need to create a prefixMatch filter rule that will contain an array of strings for prefixes to be matched.

What should be the first element of the prefix string?

A. A block blob index tag  
B. A block blob name  
C. A container name  
D. A storage account name

---

## Question 33

You need to rehydrate a blob stored in the Archive tier by changing the access tier.

Which destination blob should you use?

A. A blob in the Archive tier in the same region  
B. A blob in the Archive tier in a different region  
C. A blob in the Cool tier in a different region  
D. A blob in the Cool tier in the same region

---

## Question 34

A company uses Azure API Management to expose some of its services.

Each developer consuming APIs must use a single key to obtain access to various APIs without requiring approval from the API publisher.

You need to recommend a solution.

Which solution should you recommend?

A. Define a subscription with all APIs scope  
B. Define a subscription with product scope  
C. Restrict access based on caller IPs  
D. Restrict APIs based on client certificate

---

## Question 35

You manage an Azure API Management instance.

You need to limit the maximum number of API calls allowed from a single source for a specific time interval.

What should you configure?

A. Product  
B. Policy  
C. Subscription  
D. API

---

## Question 36

A company is using Azure API Management to expose their APIs to external partners. The company wants to ensure that the APIs are accessible only to users authenticated with OAuth 2.0, and that usage quotas are enforced to prevent abuse.

You need to configure the API Management instance to meet the security and usage requirements.

Which two actions should you perform?

A. Configure a validate-jwt policy to authenticate incoming requests  
B. Deploy an Azure Application Gateway in front of the API Management instance  
C. Implement IP filtering by defining access restriction policies  
D. Set up a rate limit by key policy to enforce call quotas

---

## Question 37

You have an Azure event hub.

You need to add partitions to the event hub.

Which code segment should you use?

A. `az eventhubs eventhub consumer-group update --resource-group MyResourceGroupName --namespace-name MyNamespaceName --eventhub-name MyEventHubName --set partitioncount=12`  
B. `az eventhubs eventhub consumer-group create --resource-group MyResourceGroupName --namespace-name MyNamespaceName --eventhub-name MyEventHubName --set partitioncount=12`  
C. `az eventhubs eventhub update --resource-group MyResourceGroupName --namespace-name MyNamespaceName --name MyEventHubName --partition-count 12`  
D. `az eventhubs eventhub create --resource-group MyResourceGroupName --namespace-name MyNamespaceName --name MyEventHubName --partition-count 12`

---

## Question 38

You need to capture events streaming from Azure Event Hubs.

To which three locations can you capture data? Each correct answer presents a complete solution.

A. Azure Blob storage  
B. Azure Data Lake Storage Gen1  
C. Azure Functions  
D. Azure Stream Analytics  
E. Azure Data Lake Storage Gen2

---

## Question 39

You have an Azure Service Bus instance.

You need to provide first-in, first-out (FIFO) guarantee for message processing.

What should you configure?

A. Dead-letter queue  
B. Message deferral  
C. Message sessions  
D. Scheduled delivery

---

## Question 40

You create an Azure Service Bus topic with a default message time to live of 10 minutes.

You need to send messages to this topic with a time to live of 15 minutes. The solution must not affect other applications that are using the topic.

What should you recommend?

A. Change the topic's default time to live to 15 minutes  
B. Change the specific message's time to live to 15 minutes  
C. Create a new topic with a default time to live of 15 minutes. Send the messages to this topic  
D. Update the time to live for the queue containing the topic

---

## Question 41

You need to write a filter condition for an Azure Service Bus topic.

Which three filters can you use? Each correct answer presents a complete solution.

A. SQL  
B. Boolean  
C. Size  
D. Correlation  
E. Content

---

## Question 42

You have an Azure Service Bus queue.

You need to ensure a publisher can send messages into a topic and multiple subscribers can become eligible to consume the messages.

Which message routing pattern should you use?

A. Simple request/reply  
B. Multicast request/reply  
C. Multiplexing  
D. Multiplexed request/reply

---

## Question 43

You are developing a .NET project that will manage messages in Azure Storage queues.

You need to verify the presence of messages in a queue without removing them from the queue.

Which method should you use?

A. Peek  
B. PeekMessages  
C. ReceiveMessages  
D. ReceiveMessageAsync

---

## Question 44

You have an application that requires message queuing.

You need to recommend a solution that meets the following requirements:

- Automatic duplicate message detection
- Ability to send 2 MB messages

Which message queuing solution should you recommend?

A. Azure Service Bus Premium tier  
B. Azure Service Bus Standard tier  
C. Azure Storage queues with locally redundant storage (LRS)  
D. Azure Storage queues with zone-redundant storage (ZRS)

---

## Question 45

A logistics company requires a messaging system that can automatically handle messages that cannot be processed after several attempts, moving them to a separate storage for later analysis.

You need to choose a queue service that supports automatic handling of non-processable messages.

What should you use?

A. Azure Event Grid with advanced filtering  
B. Azure Queue Storage with message expiration  
C. Azure Service Bus dead-letter queue  
D. Azure Storage queues with visibility timeout

---

## Question 46

A financial services company is implementing a system to process transactions that are received as messages. The system must ensure that transactions are processed only once, and in the exact order they are received to maintain data integrity.

You need to design a messaging solution that guarantees first-in-first-out (FIFO) message delivery and processing.

Which two services should you use?

A. Azure Event Grid with advanced filtering  
B. Azure Queue Storage with visibility timeout  
C. Azure Service Bus with duplicate detection  
D. Azure Service Bus with sessions enabled

---

## Question 47

You have an Azure web app that occasionally experiences high response times.

You need to be notified when the response time exceeds a certain threshold.

What should you do?

A. Configure Azure Advisor alerts  
B. Create a Resource Health alert in Azure Monitor  
C. Implement Application Insights web tests and alerts  
D. Use Azure Service Health to monitor the status of Azure services

---

## Question 48

Your team is developing a new feature for an existing Azure-based application that relies heavily on real-time data processing. The feature involves integrating multiple Azure services and third-party APIs.

You need to create a strategy to ensure that the integration of these services does not introduce any performance issues or failures. You need to design the monitoring solution to detect and address potential issues

What should you do?

A. Create a single availability test in Application Insights to monitor the endpoint of the new feature  
B. Deploy a custom logging solution to capture and review logs manually at the end of each day  
C. Schedule nightly runs of Azure Automation runbooks to check the health of each service individually  
D. Use Live Metrics in Application Insights to observe the activity of the deployed application in real-time

---

## Question 49

An e-commerce platform is planning to expand its services globally. The platform is hosted on Azure and utilizes various Azure services and third-party integrations.

You need to design and create a robust monitoring solution that can scale with the expansion and provide insights into the performance of the platform across different regions.

What should you do?

A. Deploy multiple Application Insights instances for each region and use Azure Monitor to aggregate the data  
B. Implement a single Application Insights instance with default settings to monitor the entire platform  
C. Create web tests and alerts for each region within a single Application Insights instance  
D. Use manual instrumentation to log user activities and store them in Azure Blob Storage for later analysis

---

## Question 50

A development team is using Application Insights to monitor their web application deployed on Azure. They have noticed discrepancies in the reported metrics due to high telemetry volume.

You need to ensure that the reported metrics accurately reflect the application's performance without being affected by telemetry sampling.

What should you implement to achieve this goal?

A. Configure Application Insights to use preaggregated standard metrics for dashboarding and real-time alerting  
B. Create a custom Kusto query in Application Insights to manually aggregate log-based metrics  
C. Disable all telemetry sampling in Application Insights to ensure all events are collected  
D. Increase the sampling rate in Application Insights to collect more data points for log-based metrics