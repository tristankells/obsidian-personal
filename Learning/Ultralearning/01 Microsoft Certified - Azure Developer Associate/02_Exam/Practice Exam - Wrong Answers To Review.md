> [!question] You manage an Azure App Service web app named **app1**. App1 is registered as a multi-tenant application in a Microsoft Entra ID tenant named **tenant1**.
> 
> You need to grant app1 the permission to access the Microsoft Graph API in tenant1.
> 
> Which service principal should you use?
> 
> Select only one answer.
> 
> - legacy
> - system-assigned managed identity
> - application
> - user-assigned managed identity
> 
> > [!success]- Answer
> > application
> > 
> > This item tests the candidate’s knowledge of accessing user data from Microsoft Graph, which is part of implementing user authentication and authorization.
> > 
> > A Microsoft Entra ID application is defined by its one and only application object, which resides in the Microsoft Entra ID tenant where the application was registered (known as the application's home tenant). The application service principal is used to configure permission for app1 in tenant1 to access the Microsoft Graph API. The legacy service principal is a legacy app, which is an app created before app registrations were introduced or an app created through legacy experiences. Managed identities eliminate the need to manage credentials in code. A system-assigned managed identity is restricted to one per resource and is tied to the lifecycle of the resource. Managed identities for Azure resources eliminate the need to manage credentials in code. A user-assigned managed identity can be created and assigned to one or more instances of an Azure service. The legacy, system-assigned managed identity, and user-assigned managed identity cannot be used to assign permission for app1 in tenant1 to access the Microsoft Graph API.
> > 
> > [Explore the Microsoft identity platform - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/explore-microsoft-identity-platform/)
> > 
> > [Explore service principals - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/explore-microsoft-identity-platform/3-app-service-principals)

> [!question] You plan to enable a user to create a managed identity for an Azure virtual machine (VM).
> 
> You need to ensure the following requirements are met:
> 
> - The user account must have sufficient permissions to create the managed identity.
> - The principle of least privilege must be used.
> 
> Which permission role should you assign?
> 
> Select only one answer.
> 
> - Virtual Machine Administrator Login
> - Virtual Machine Contributor
> - Global Administrator
> - Security Administrator
> 
> > [!success]- Answer
> > Virtual Machine Contributor
> > 
> > This item tests the candidate’s knowledge of the principle of least privilege, which is an essential part of implementing secure cloud solutions.
> > 
> > Virtual Machine Contributor is the least privileged built-in role required to create a managed identity for an Azure VM. Virtual Machine Administrator Login is not sufficient to create a managed identity for an Azure VM. Global Administrator and Security Administrator have excessive permissions to Microsoft Entra ID, which does not follow the principle of least privilege. Global Administrator and Security Administrator do not provide sufficient permissions to the Azure resources.
> > 
> > [Configure managed identities - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-managed-identities/4-configure-managed-identities)

> [!question] A company plans to use Azure App Configuration for feature flags in an application.
> 
> The company has the following encryption requirements:
> 
> - customer-managed keys
> - hardware security module (HSM)-protected keys
> 
> You need to recommend service tiers.
> 
> Which two tiers should you recommend? Each correct answer presents part of the solution.
> 
> Select all answers that apply.
> 
> - Azure App Configuration Free tier
> - Azure App Configuration Standard tier
> - Azure Key Vault Standard tier
> - Azure Key Vault Premium tier
> 
> > [!success]- Answer
> > Azure App Configuration Standard tier
> > Azure Key Vault Premium tier
> > 
> > This item tests the candidate’s knowledge of the service tiers for Azure App Configuration and Azure Key Vault.
> > 
> > App Configuration Standard tier must be used for customer-managed keys to be used in App Configuration. Key Vault Premium tier is required to support HSM-protected keys. App Configuration Free tier does not allow the use of customer-managed keys. Key Vault Standard tier does not support HSM-protected keys.
> > 
> > [Secure app configuration data - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-azure-app-configuration/5-secure-app-configuration-data)

> [!question] You have an Azure event hub.
> 
> You need to add partitions to the event hub.
> 
> Which code segment should you use?
> 
> Select only one answer.
> 
> - `az eventhubs eventhub consumer-group update --resource-group MyResourceGroupName --namespace-name MyNamespaceName --eventhub-name MyEventHubName --set partitioncount=12`
> - `az eventhubs eventhub consumer-group create --resource-group MyResourceGroupName --namespace-name MyNamespaceName --eventhub-name MyEventHubName --set partitioncount=12`
> - `az eventhubs eventhub update --resource-group MyResourceGroupName --namespace-name MyNamespaceName --name MyEventHubName --partition-count 12`
> - `az eventhubs eventhub create --resource-group MyResourceGroupName --namespace-name MyNamespaceName --name MyEventHubName --partition-count 12`
> 
> > [!success]- Answer
> > `az eventhubs eventhub update --resource-group MyResourceGroupName --namespace-name MyNamespaceName --name MyEventHubName --partition-count 12`
> > 
> > This item tests the candidate’s knowledge of developing event-based solutions.
> > 
> > The code segment that includes `az eventhubs eventhub update` adds partitions to an existing event hub. The code segment that includes `az eventhubs eventhub consumer-group update` updates the event hub consumer group. The code segment that includes `az eventhubs eventhub consumer-group create` will create an event hub consumer group. The code segment that includes `az eventhubs eventhub create --resource-group` segment will create an event hub with partitions, not change an existing one
> > 
> > [Control Azure services with the CLI - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/control-azure-services-with-cli/)

> [!question] You have an Azure Service Bus queue.
> 
> You need to ensure a publisher can send messages into a topic and multiple subscribers can become eligible to consume the messages.
> 
> Which message routing pattern should you use?
> 
> Select only one answer.
> 
> - simple request/reply
> - multicast request/reply
> - multiplexing
> - multiplexed request/reply
> 
> > [!success]- Answer
> > multicast request/reply
> > 
> > This item tests the candidate’s knowledge of message routing in Azure Service Bus, which is part of developing message-based solutions.
> > 
> > A publisher can send a message into a topic and multiple subscribers can become eligible to consume the message. A publisher can send a message into a queue and expect a reply from the message consumer, but multiple subscribers cannot consume the message. This session feature enables multiplexing of streams of related messages through a single queue but cannot be consumed by multiple subscribers. This session feature enables multiplexed replies, allowing several publishers to share a reply queue, but a message cannot be consumed by multiple subscribers.
> > 
> > [Explore Service Bus message payloads and serialization - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/discover-azure-message-queue/5-messages-payloads-serialization)

> [!question] You are developing a cloud native containerized background task application.
> 
> You need to choose the appropriate container deployment option based on the following requirements:
> 
> - Minimize cost
> - Support service discovery and traffic splitting
> - Enable event-driven application architecture
> - Do not require access to native Kubernetes API
> 
> What should you use?
> 
> Select only one answer.
> 
> - Azure Spring Apps
> - Azure Container Instances
> - Azure Container Apps
> - Azure Functions
> 
> > [!success]- Answer
> > Azure Container Apps
> > 
> > This item tests the candidate’s knowledge of creating solutions by using Azure Container Apps. Azure Container Apps enables you to build serverless microservices based on containers. It is optimized for running general purpose containers and provides many application-specific concepts on top of containers. Azure Spring Apps is a fully managed service for Spring developers. It provides lifecycle management to run Spring Boot, Spring Cloud, or any other Spring applications on Azure. Azure Container Instances does not support scaling, load balancing, revisions, scale, or environments and does not meet the mentioned requirements. Azure Functions is a serverless Function as a Service (FaaS) solution. It can be used for running event-driven applications by using the functions programming model. However, it cannot be used to deploy a container image.
> > 
> > Learn link not available yet; scoping statement new for this OD. Noting that we need to update with the link when the content is live.
> > 
> > Noting that we need to update with the link when the content is live.
> > 
> > [Implement Azure Container Apps - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/implement-azure-container-apps/)

> [!question] You need to read an Azure Cosmos DB change feed by using a push model.
> 
> Which two components can you use to achieve this goal? Each correct answer presents a complete solution.
> 
> Select all answers that apply.
> 
> - Azure Functions with an Azure Cosmos DB trigger
> - Change feed processor library
> - Azure Functions with an Azure Event Grid trigger
> - Change feed pull model
> 
> > [!success]- Answer
> > Azure Functions with an Azure Cosmos DB trigger
> > Change feed processor library
> > 
> > This item tests the candidate’s knowledge of developing solutions that use Azure Cosmos DB storage.
> > 
> > Azure Functions with an Azure Cosmos DB trigger allows you to select the container to connect, and the Azure Function is triggered whenever there is a change in the container. The change feed processor library follows the observer pattern, where the processing function is called by the library. The change feed processor library will automatically check for changes and, if changes are found, push them to the client. Azure Functions with an Event Grid trigger will execute the function when an Event Grid event is dispatched. It has no relationship with an Azure Cosmos DB change feed. A change feed pull model will use a pull model rather than a push model.
> > 
> > [Consume an Azure Cosmos DB for NoSQL change feed using the SDK - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/consume-azure-cosmos-db-sql-api-change-feed-use-sdk/)
> > 
> > [Handle events with Azure Functions and Azure Cosmos DB for NoSQL change feed - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/handle-events-azure-functions-azure-cosmos-db-sql-api-change-feed/)

> [!question] You have blobs in Azure Blob storage. The blobs store pictures.
> 
> You need to record the location and weather condition information from when the pictures were taken. You must ensure you can use up to 2,000 characters when recording the information.
> 
> What should you do?
> 
> Select only one answer.
> 
> - Append a suffix to the blob name by using the location and weather. Add a delimiter between them.
> - Use metadata headers defined with a POST request.
> - Use metadata headers defined with a PUT request.
> - Create one container for each location. Inside each container, define the blob name as the weather type and a random suffix.
> 
> > [!success]- Answer
> > Use metadata headers defined with a PUT request.
> > 
> > This item tests the candidate's knowledge about structuring data for blob storage.
> > 
> > Metadata is the proper way to define this kind of data, allowing independent modification and supporting up to 8 KB in total size. The HTTP verb to define metadata is a PUT, and this is the correct format to define metadata values. The maximum size of a blob name is 1,024 characters. Also, this is not an optimal approach because metadata can be obtained and set independently, maintaining the same file name. Metadata is the proper way to define this kind of data, allowing independent modification and supporting up to 8 KB in total size. But the HTTP verb to define metadata is a PUT, not POST. The combination of locations and weather types can be potentially unlimited, and container names are limited to 63 characters.
> > 
> > [AZ-204: Develop solutions that use Blob storage - Training | Microsoft Learn](https://learn.microsoft.com/training/paths/develop-solutions-that-use-blob-storage/)

> [!question] You are developing an application.
> 
> You need to set the standard HTTP properties of containers in Azure Blob Storage.
> 
> Which two HTTP properties can you set? Each correct answer presents part of the solution.
> 
> Select all answers that apply.
> 
> - ETag
> - Last-Modified
> - Cache-Control
> - Origin
> - Range
> 
> > [!success]- Answer
> > ETag
> > Last-Modified
> > 
> > This item tests the candidate’s knowledge of setting and retrieving properties and metadata. Metadata in Azure Storage objects is defined through headers starting with x-ms-meta-. Some standard HTTP properties are also available for both objects and containers. The only two HTTP properties that are available for containers are ETag and Last-Modified.
> > 
> > Last-Modified, Cache-Control, Origin and Range are properties only available for blobs.
> > 
> > [Set and retrieve properties and metadata for blob resources by using REST](https://learn.microsoft.com/training/modules/work-azure-blob-storage/5-set-retrieve-properties-metadata-rest)

> [!question] You plan to develop an Azure App Service web app named **app1** by using a Windows custom container.
> 
> You need to load a TLS/SSL certificate in application code.
> 
> Which app setting should you configure?
> 
> Select only one answer.
> 
> - `WEBSITE_LOAD_CERTIFICATES`
> - `WEBSITE_ROOT_CERTS_PATH`
> - `WEBSITE_CORS_ALLOWED_ORIGINS`
> - `WEBSITE_AUTH_TOKEN_CONTAINER_SASURL`
> 
> > [!success]- Answer
> > `WEBSITE_LOAD_CERTIFICATES`
> > 
> > This item tests the candidate’s knowledge of configuring app settings, which is part of creating Azure App Service Web Apps.
> > 
> > The `WEBSITE_LOAD_CERTIFICATES` app setting makes the specified certificates accessible to Windows or Linux custom containers as files. The `WEBSITE_ROOT_CERTS_PATH` app setting is read-only and does not allow comma-separated thumbprint values to be mentioned to the certificates and then be loaded in the code. The `WEBSITE_AUTH_TOKEN_CONTAINER_SASURL` app setting is used to instruct the auth module to store and load all encrypted tokens to the specified blob storage container. This setting is used for Azure Storage and cannot be used to load certificates inside a Windows custom container.
> > 
> > [Configure web app settings - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-web-app-settings/)

> [!question] You create an Azure web app locally. The web app consists of a ZIP package.
> 
> You need to deploy the web app by using the Azure CLI. The deployment must reduce the likelihood of locked files.
> 
> What should you do?
> 
> Select only one answer.
> 
> - Run `az webapp deploy` specifying `–-clean true`.
> - Run `az webapp deploy` specifying `–-restart true`.
> - Run `az webapp deploy` to a staging slot with auto swap on.
> - Run `az webapp deploy` by using a high value for the `--timeout` parameter.
> 
> > [!success]- Answer
> > Run `az webapp deploy` to a staging slot with auto swap on.
> > 
> > This item tests the candidate's knowledge of deploying Azure Web Apps using the Azure CLI.
> > 
> > Using a production and staging slot with auto swap enabled reduces the likelihood of locked files. If `–clean true` is used, the target folder is cleaned, but this has no effect on the likelihood of locked files. It is good to restart the app after deployment. This, however, is the default behavior of a ZIP deployment and has no effect on the reduced likelihood of locked files during deployment. The `--timeout` parameter has no effect on the likelihood of locked files.
> > 
> > [Deploy to App Service - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/introduction-to-azure-app-service/4-deploy-code-to-app-service?ns-enrollment-type=learningpath&ns-enrollment-id=learn.wwl.create-azure-app-service-web-apps)

> [!question] You are a developing a serverless API using Azure Functions. The API is expected to handle a large number of HTTP requests and make outbound requests to a third-party service. The third-party service has a rate limit on the number of requests it can handle per minute.
> 
> You need to ensure that the Azure Function does not exceed the rate limit of the third-party service and manage resource utilization effectively.
> 
> Each correct answer presents part of the solution. Which two actions should you perform?
> 
> Select all answers that apply.
> 
> - Enable 'dynamicThrottlesEnabled' property in the host.json file to reject requests with a 429 'Too Busy' response when system performance counters are over a high threshold.
> - Enable 'hsts' property in the host.json file to enforce HTTP Strict Transport Security (HSTS) behavior.
> - Set the 'maxConcurrentRequests' property in the host.json file to limit the number of parallel executions.
> - Set the 'maxOutstandingRequests' property in the host.json file to limit the number of outstanding requests at any given time.
> - Set the 'routePrefix' property in the host.json file to an empty string to remove the default prefix.
> 
> > [!success]- Answer
> > Set the 'maxConcurrentRequests' property in the host.json file to limit the number of parallel executions.
> > Set the 'maxOutstandingRequests' property in the host.json file to limit the number of outstanding requests at any given time.
> > 
> > Setting the 'maxConcurrentRequests' property in the host.json file will limit the number of HTTP functions that are executed in parallel, which can help manage resource utilization and avoid exceeding the rate limit of the third-party service. The 'maxOutstandingRequests' property limits the number of outstanding requests that are held at any given time, including queued requests and in-progress executions, which can also help manage resource utilization. Enabling 'dynamicThrottlesEnabled' property would not help in this scenario as it rejects requests based on system performance counters, not based on the rate limit of a third-party service. The 'hsts' property is used to enforce HTTP Strict Transport Security (HSTS) behavior and is not related to managing resource utilization or rate limiting. The 'routePrefix' property is used to set the route prefix for all routes and does not affect resource utilization or rate limiting.
> > 
> > [Azure Functions HTTP triggers and bindings overview - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook?tabs=isolated-process%2Cfunctionsv2&pivots=programming-language-csharp)

> [!question] You have an Azure subscription that contains an Azure Cosmos DB Core (SQL) API account. The account hosts two Azure Cosmos DB containers named Container1 and Container2.
> 
> You have an Azure Functions app named FunctionApp1.
> 
> You plan to create a function in FunctionApp1 that will process changes to Container1, and then write the results to Container2.
> 
> You need to ensure that the function reads the changes to Container1 immediately. The solution must minimize costs.
> 
> What should you do?
> 
> Select only one answer.
> 
> - Configure FunctionApp1 to use the Consumption plan.
> - Configure FunctionApp1 to use the Premium plan.
> - Set the feedPollDelay parameter of the function to 0.
> - Set the feedPollDelay parameter of the function to -1.
> 
> > [!success]- Answer
> > Set the feedPollDelay parameter of the function to 0.
> > 
> > The correct solution is to set the **feedPollDelay** parameter to **0**, because this controls how frequently the Azure Functions change feed processor polls for new changes in the Cosmos DB container. By default, there is a delay (typically 5 seconds) between polls to balance responsiveness and cost. Setting it to **0** ensures the function reads changes from Container1 immediately, which meets the requirement without needing to upgrade the hosting plan. Configuring the function to use the **Consumption** or **Premium** plan does not directly affect how quickly change feed events are read. Setting **feedPollDelay** to **-1** is invalid and would not achieve the desired result. Therefore, adjusting feedPollDelay to 0 is the most cost-effective solution.
> > 
> > [Quickstart: Respond to database changes in Azure Cosmos DB using Azure Functions](https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-cosmos-db-triggered-function)
> > [Azure Cosmos DB trigger for Azure Functions 2.x and higher](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-trigger)

> [!question] You have a web service in Azure that uses an Azure SQL Database instance and is instrumented by using Application Insights.
> 
> You need to write a query to identify how long it takes for a specific web service call to retrieve data from the database.
> 
> Which type of data should you query in Application Insights?
> 
> Select only one answer.
> 
> - customEvents
> - dependencies
> - performanceCounters
> - requests
> 
> > [!success]- Answer
> > dependencies
> > 
> > The correct solution is to query **dependencies**, because Application Insights tracks external calls made by your service, including SQL Database queries, REST APIs, and storage operations. Dependency telemetry includes duration, success/failure, and target resource, making it ideal for measuring how long a web service call takes to retrieve data from the database. **customEvents** capture user-defined actions in the application but do not include database timings. **performanceCounters** provide system-level metrics such as CPU or memory usage, and **requests** represent incoming calls to the web service, not outbound database calls. Therefore, dependency data is the right source for identifying query durations to Azure SQL Database.
> > 
> > [Use Azure Application Insights](https://learn.microsoft.com/en-us/training/modules/configure-azure-app-services/10-use-application-insights)
> > [Monitor Azure resources with Azure Monitor](https://learn.microsoft.com/en-us/azure/azure-monitor/platform/monitor-azure-resource)
> > [Describe Azure Monitor](https://learn.microsoft.com/en-us/training/modules/describe-monitoring-tools-azure/4-describe-azure-monitor)
> > [Monitor your networks using Azure Monitor](https://learn.microsoft.com/en-us/training/modules/design-implement-network-monitoring/2-monitor-networks-using-azure-monitor)

> [!question] A company is developing an IoT solution for smart buildings that collects telemetry data from various sensors. The data is sent to Azure for real-time analysis and storage.
> 
> You need to implement a solution that allows the ingestion of high volumes of events and provides reliable delivery to downstream processing services with minimal latency.
> 
> Which service should you use?
> 
> Select only one answer.
> 
> - Azure Blob Storage
> - Azure Event Grid
> - Azure Event Hubs
> - Azure Service Bus
> 
> > [!success]- Answer
> > Azure Event Hubs
> > 
> > Azure Event Hubs is designed for high-throughput, real-time event streaming and is compatible with Apache Kafka, making it suitable for IoT scenarios. Azure Event Grid is more suited for event routing and serverless applications. Azure Service Bus is better for traditional enterprise messaging patterns, and Azure Blob Storage is not optimized for real-time event ingestion.
> > 
> > [Explore Azure Event Grid - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/azure-event-grid/2-event-grid-overview)
> > [Discover Azure Event Hubs - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/azure-event-hubs/2-event-hubs-overview)
> > [What is Azure Event Grid? - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/event-grid/overview)

> [!question] You need to write a filter condition for an Azure Service Bus topic.
> 
> Which three filters can you use? Each correct answer presents a complete solution.
> 
> Select all answers that apply.
> 
> - SQL
> - Boolean
> - Size
> - Correlation
> - Content
> 
> > [!success]- Answer
> > SQL
> > Boolean
> > Correlation
> > 
> > This item tests the candidate’s knowledge of implementing solutions that use Azure Service Bus.
> > 
> > A SqlFilter holds a SQL-like conditional expression that is evaluated in the broker against the arriving message’s user-defined properties and system properties. The TrueFilter and FalseFilter either cause all arriving messages (true) or none of the arriving messages (false) to be selected for the subscription. A CorrelationFilter holds a set of conditions that are matched against one or more of an arriving message's user and system properties. Size Filter and Content are not valid options for Service Bus topic filtering.
> > 
> > [Implement message-based communication workflows with Azure Service Bus - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-message-workflows-with-service-bus/)

> [!question] You plan to use Microsoft Graph to retrieve a list of users in a Microsoft Entra ID tenant.
> 
> You need to optimize query results.
> 
> Which two query options should you use? Each correct answer presents part of the solution.
> 
> Select all answers that apply.
> 
> - `$filter`
> - `$count`
> - `$orderby`
> - `$select`
> - `$expand`
> 
> > [!success]- Answer
> > `$filter`
> > `$select`
> > 
> > This item tests the candidate's knowledge of Microsoft Graph query options.
> > 
> > The `$filter` query option must be used to limit the results returned. The `$select` query option limits the attributes projected from the result set, making the query more efficient. The `$count` query option is meant to retrieve the total count of matching resources. `$expand` query option is used to retrieve related resources.
> > 
> > [Query Microsoft Graph by using REST - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/microsoft-graph/3-microsoft-graph-api)

> [!question] You need to implement an Azure Storage lifecycle policy for append blobs.
> 
> Which rule action should you use?
> 
> Select only one answer.
> 
> - delete
> - enableAutoTierToHotFromCool
> - tierToArchive
> - tierToCool
> 
> > [!success]- Answer
> > delete
> > 
> > This item tests the candidate’s knowledge of configuring Azure Storage lifecycle policy for blobs, which is an essential part of developing solutions for blob storage.
> > 
> > The delete rule action supports both block blobs and append blobs. The enableAutoTierToHotFromCool, tierToArchive, and tierToCool rule actions only supports block blobs.
> > 
> > [Discover Blob storage lifecycle policies - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/manage-azure-blob-storage-lifecycle/3-blob-storage-lifecycle-policies)

> [!question] You have blobs in an Azure storage account.
> 
> You need to implement a stored access policy that will apply to a shared access signature generated for the blobs.
> 
> To which type of storage resource should you associate the policy?
> 
> Select only one answer.
> 
> - the storage account
> - the blob service of the storage account
> - the container that is hosting blobs
> - each individual blob
> 
> > [!success]- Answer
> > the container that is hosting blobs
> > 
> > This item tests the candidate’s knowledge of configuring stored access policy, which is part of implementing authorization.
> > 
> > The container that is hosting blobs is used for associating the corresponding stored access policies. The storage account can be associated with shared access signatures keys but not stored access policies. The blob service of the storage account can be associated with shared access signatures keys but not stored access policies. Each individual blob can be associated with shared access signatures keys but not stored access policies.
> > 
> > [Define a stored access policy](https://learn.microsoft.com/en-us/rest/api/storageservices/define-stored-access-policy)

> [!question] You develop an App Service app hosted on Windows Platform. Users report that the app is failing.
> 
> You need to begin troubleshooting the app by inspecting a copy of the page that is returned when the HTTP return code is greater than 400.
> 
> Which type of log should you review?
> 
> Select only one answer.
> 
> - application
> - web server
> - detailed error
> - deployment
> 
> > [!success]- Answer
> > detailed error
> > 
> > This item tests the candidate’s knowledge of using logs to troubleshoot web apps. The detailed error log contains copies of the error pages, produced in response to HTTP codes greater than 400, that would have been sent to clients. These pages are not sent due to security reasons. The web server log shows information about the raw HTTP request, such as method, bytes, and client user agent. The application log is application specific, logging information that your application code or components that are used by your application writes. The deployment log stores information to diagnose the reasons for a failed deployment.
> > 
> > [Enable diagnostic logging - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-web-app-settings/5-enable-diagnostic-logging)

> [!question] A company plans to implement a Microsoft Defender for Cloud solution.
> 
> The company has the following requirements:
> 
> - Notifies when DNS domains are not deleted when a new Azure Functions app is deleted.
> - Use native alerting.
> - Minimize costs.
> 
> You need to select a hosting plan.
> 
> Which hosting plan should you use?
> 
> Select only one answer.
> 
> - Consumption
> - Standard
> - Premium
> - Free
> 
> > [!success]- Answer
> > Standard
> > 
> > This item tests the candidate's knowledge about securing Azure Functions.
> > 
> > The Standard plan supports both custom domains and Microsoft Defender for Cloud, which can automatically alert on dangling DNS domains. The Consumption plan is incorrect because it does not support Microsoft Defender for Cloud. This can automatically alert on dangling DNS domains. The Premium plan supports custom domains and Microsoft Defender for Cloud, which can automatically alert on dangling DNS domains. This, however, is not the lowest cost option. The Free plan does not support custom domains, although it does support Microsoft Defender for Cloud, which can automatically alert on dangling DNS domains.
> > 
> > [Overview of Defender for App Service to protect your Azure App Service web apps and APIs - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-app-service-introduction "Overview of Defender for App Service to protect your Azure App Service web apps and APIs - Training | Microsoft Learn")

> [!question] You create a batch routine by using a timer trigger in Azure Functions.
> 
> You need to configure the batch routine to execute every 15 minutes, from Monday through Friday.
> 
> Which code segment should you use?
> 
> Select only one answer.
> 
> - [Function(nameof(TimerTriggerCSharp))]  
> [FixedDelayRetry(5, "00:00:10")]  
> public static void Run([TimerTrigger("0 */15 * * * 1-5")] TimerInfo myTimer,  
>   FunctionContext context)  
> {  
>   var log = context.GetLogger(nameof(TimerFunction));  
>   if (myTimer.IsPastDue)  
>   {  
>     log.LogInformation("Timer is running late!");  
>   }  
>   log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");  
> }
> - [Function(nameof(TimerTriggerCSharp))]  
> [FixedDelayRetry(5, "00:00:10")]  
> public static void Run([TimerTrigger("*/15 * * * 0-4")] TimerInfo myTimer,  
>   FunctionContext context)  
> {  
>   var log = context.GetLogger(nameof(TimerFunction));  
>   if (myTimer.IsPastDue)  
>   {  
>     log.LogInformation("Timer is running late!");  
>   }  
>   log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");  
> }
> - [Function(nameof(TimerTriggerCSharp))]  
> [FixedDelayRetry(5, "00:00:10")]  
> public static void Run([TimerTrigger("0 15 * * * ")] TimerInfo myTimer,  
>   FunctionContext context)  
> {  
>   var log = context.GetLogger(nameof(TimerFunction));  
>   if (myTimer.IsPastDue)  
>   {  
>     log.LogInformation("Timer is running late!");  
>   }  
>   log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");  
> }
> - [Function(nameof(TimerTriggerCSharp))]  
> [FixedDelayRetry(5, "00:00:10")]  
> public static void Run([TimerTrigger("* 15 * * 1-5")] TimerInfo myTimer,  
>   FunctionContext context)  
> {  
>   var log = context.GetLogger(nameof(TimerFunction));  
>   if (myTimer.IsPastDue)  
>   {  
>     log.LogInformation("Timer is running late!");  
>   }  
>   log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");  
> }
> 
> > [!success]- Answer
> > [Function(nameof(TimerTriggerCSharp))]  
> [FixedDelayRetry(5, "00:00:10")]  
> public static void Run([TimerTrigger("0 */15 * * * 1-5")] TimerInfo myTimer,  
>   FunctionContext context)  
> {  
>   var log = context.GetLogger(nameof(TimerFunction));  
>   if (myTimer.IsPastDue)  
>   {  
>     log.LogInformation("Timer is running late!");  
>   }  
>   log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");  
> }
> > 
> > This item tests the candidate’s knowledge of working with timer triggers in Azure Functions.
> > 
> > The code segment that includes `Run([TimerTrigger("0 */15 * * * 1-5")` executes the function every 15 minutes from Monday to Friday. The code segment that includes `Run([TimerTrigger("*/15 * * * 0-4")` is missing the second part, and it is not using the proper range for days of the week. The code segment that includes `Run([TimerTrigger("0 15 * * * ")` executes only once at 15:00 (3 PM). The code segment that includes `Run([TimerTrigger("* 15 * * 1-5")` is missing the seconds attribute and the step (‘/’) part for the minutes.
> > 
> > https://learn.microsoft.com/training/modules/execute-azure-function-with-triggers/
> > 
> > [Timer trigger for Azure Functions - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-timer?tabs=python-v2%2Cisolated-process%2Cnodejs-v4&pivots=programming-language-csharp)

> [!question] You have an Azure App Service web app.
> 
> You enable Application Insights for the app.
> 
> You need to view detailed information about each user who signs in to the app, including what the user does while signed in.
> 
> Which type of telemetry data should you filter by using Application Insights?
> 
> Select only one answer.
> 
> - dependencies
> - events
> - requests
> - traces
> 
> > [!success]- Answer
> > events
> > 
> > The correct solution is to filter by **events**, because Application Insights events are custom telemetry designed to track user actions and behaviors inside the app, such as button clicks, page navigation, or other activities performed while signed in. **Requests** represent incoming HTTP calls to the app and provide details about performance and response codes, but they don’t capture what a user does within the app. **Dependencies** track calls to external resources like databases or APIs, and **traces** log diagnostic information from the application. To understand **per-user activity** inside the application, events are the appropriate telemetry type.
> > 
> > [Summary](https://learn.microsoft.com/en-us/training/modules/route-system-feedback/5-summary)  
> > [Implement Application Insights](https://learn.microsoft.com/en-us/training/modules/implement-tools-track-usage-flow/7-implement-application-insights)  
> > [Use Azure Application Insights](https://learn.microsoft.com/en-us/training/modules/configure-azure-app-services/10-use-application-insights)  
> > [Monitor Azure resources with Azure Monitor](https://learn.microsoft.com/en-us/azure/azure-monitor/platform/monitor-azure-resource)

> [!question] You manage a Microsoft Entra ID registered application named **app1**. 
> 
> App1 calls a web API, which then calls Microsoft Graph.
> 
> You need to ensure the signed-in user identity is delegated through the request chain.
> 
> Which authentication flow should you use?
> 
> Select only one answer.
> 
> - Authorization code
> - On-Behalf-Of
> - Client credentials
> - Implicit
> 
> > [!success]- Answer
> > On-Behalf-Of
> > 
> > This item tests the candidate’s knowledge of accessing user data from Microsoft Graph, which is part of implementing user authentication and authorization.
> > 
> > OAuth 2.0 On-Behalf-Of flow (OBO) is used when an application invokes a service or web API, which in turn needs to call another service or web API. The idea is to propagate the delegated user identity and permissions through the request chain. The OAuth 2.0 authorization code grant can be used in apps that are installed on a device to gain access to protected resources, such as web APIs. The OAuth 2.0 client credentials grant flow permits a web service (confidential client) to use its own credentials, instead of impersonating a user, to authenticate when calling another web service. Implicit is a redirection-based flow. The client must be capable of interacting with the resource owner's user-agent (typically a web browser). Authorization code, On-Behalf-Of, and implicit cannot be used to delegate user permission and identity.
> > 
> >[Implement authentication by using the Microsoft Aut](https://learn.microsoft.com/training/modules/implement-authentication-by-using-microsoft-authentication-library/)

> [!question] A company implements a multi-region Azure Cosmos DB account.
> You need to configure the default consistency level for the account. The consistency level must ensure that update operations made as a batch within a transaction are always visible together.
> 
> Which consistency level should you use?
> 
> Select only one answer.
> 
> - Bounded Staleness
> - Session
> - Consistent Prefix
> - Eventual
> 
> > [!success]- Answer
> > On-Behalf-Of
> > 
> > This item tests the candidate’s knowledge of accessing user data from Microsoft Graph, which is part of implementing user authentication and authorization.
> > 
> > OAuth 2.0 On-Behalf-Of flow (OBO) is used when an application invokes a service or web API, which in turn needs to call another service or web API. The idea is to propagate the delegated user identity and permissions through the request chain. The OAuth 2.0 authorization code grant can be used in apps that are installed on a device to gain access to protected resources, such as web APIs. The OAuth 2.0 client credentials grant flow permits a web service (confidential client) to use its own credentials, instead of impersonating a user, to authenticate when calling another web service. Implicit is a redirection-based flow. The client must be capable of interacting with the resource owner's user-agent (typically a web browser). Authorization code, On-Behalf-Of, and implicit cannot be used to delegate user permission and identity.
> > 
> >[Implement authentication by using the Microsoft Aut](https://learn.microsoft.com/training/modules/implement-authentication-by-using-microsoft-authentication-library/)
> >

