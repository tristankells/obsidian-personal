You manage an Azure App Service web app named **app1**. App1 is registered as a multi-tenant application in a Microsoft Entra ID tenant named **tenant1**.

You need to grant app1 the permission to access the Microsoft Graph API in tenant1.

Which service principal should you use?

Select only one answer.

legacy

system-assigned managed identity

application

**This answer is correct.**

user-assigned managed identity

This item tests the candidate’s knowledge of accessing user data from Microsoft Graph, which is part of implementing user authentication and authorization.

A Microsoft Entra ID application is defined by its one and only application object, which resides in the Microsoft Entra ID tenant where the application was registered (known as the application's home tenant). The application service principal is used to configure permission for app1 in tenant1 to access the Microsoft Graph API. The legacy service principal is a legacy app, which is an app created before app registrations were introduced or an app created through legacy experiences. Managed identities eliminate the need to manage credentials in code. A system-assigned managed identity is restricted to one per resource and is tied to the lifecycle of the resource. Managed identities for Azure resources eliminate the need to manage credentials in code. A user-assigned managed identity can be created and assigned to one or more instances of an Azure service. The legacy, system-assigned managed identity, and user-assigned managed identity cannot be used to assign permission for app1 in tenant1 to access the Microsoft Graph API.

[Explore the Microsoft identity platform - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/explore-microsoft-identity-platform/)

[Explore service principals - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/explore-microsoft-identity-platform/3-app-service-principals)

---
You plan to enable a user to create a managed identity for an Azure virtual machine (VM).

You need to ensure the following requirements are met:

- The user account must have sufficient permissions to create the managed identity.
- The principle of least privilege must be used.

Which permission role should you assign?

Select only one answer.

Virtual Machine Administrator Login

Virtual Machine Contributor

**This answer is correct.**

Global Administrator

Security Administrator

**This answer is incorrect.**

This item tests the candidate’s knowledge of the principle of least privilege, which is an essential part of implementing secure cloud solutions.

Virtual Machine Contributor is the least privileged built-in role required to create a managed identity for an Azure VM. Virtual Machine Administrator Login is not sufficient to create a managed identity for an Azure VM. Global Administrator and Security Administrator have excessive permissions to Microsoft Entra ID, which does not follow the principle of least privilege. Global Administrator and Security Administrator do not provide sufficient permissions to the Azure resources.

[Configure managed identities - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-managed-identities/4-configure-managed-identities)


---

A company plans to use Azure App Configuration for feature flags in an application.

The company has the following encryption requirements:

- customer-managed keys
- hardware security module (HSM)-protected keys

You need to recommend service tiers.

Which two tiers should you recommend? Each correct answer presents part of the solution.

Select all answers that apply.

Azure App Configuration Free tier

Azure App Configuration Standard tier

**This answer is correct.**

Azure Key Vault Standard tier

**This answer is incorrect.**

Azure Key Vault Premium tier

**This answer is correct.**

This item tests the candidate’s knowledge of the service tiers for Azure App Configuration and Azure Key Vault.

App Configuration Standard tier must be used for customer-managed keys to be used in App Configuration. Key Vault Premium tier is required to support HSM-protected keys. App Configuration Free tier does not allow the use of customer-managed keys. Key Vault Standard tier does not support HSM-protected keys.

[Secure app configuration data - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-azure-app-configuration/5-secure-app-configuration-data)

---

You have an Azure event hub.

You need to add partitions to the event hub.

Which code segment should you use?

Select only one answer.

`az eventhubs eventhub consumer-group update --resource-group MyResourceGroupName --namespace-name MyNamespaceName --eventhub-name MyEventHubName --set partitioncount=12`

`az eventhubs eventhub consumer-group create --resource-group MyResourceGroupName --namespace-name MyNamespaceName --eventhub-name MyEventHubName --set partitioncount=12`

**This answer is incorrect.**

`az eventhubs eventhub update --resource-group MyResourceGroupName --namespace-name MyNamespaceName --name MyEventHubName --partition-count 12`

**This answer is correct.**

`az eventhubs eventhub create --resource-group MyResourceGroupName --namespace-name MyNamespaceName --name MyEventHubName --partition-count 12`

This item tests the candidate’s knowledge of developing event-based solutions.

The code segment that includes `az eventhubs eventhub update` adds partitions to an existing event hub. The code segment that includes `az eventhubs eventhub consumer-group update` updates the event hub consumer group. The code segment that includes `az eventhubs eventhub consumer-group create` will create an event hub consumer group. The code segment that includes `az eventhubs eventhub create --resource-group` segment will create an event hub with partitions, not change an existing one

[Control Azure services with the CLI - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/control-azure-services-with-cli/)

---

You have an Azure Service Bus queue.

You need to ensure a publisher can send messages into a topic and multiple subscribers can become eligible to consume the messages.

Which message routing pattern should you use?

Select only one answer.

simple request/reply

multicast request/reply

**This answer is correct.**

multiplexing

multiplexed request/reply

This item tests the candidate’s knowledge of message routing in Azure Service Bus, which is part of developing message-based solutions.

A publisher can send a message into a topic and multiple subscribers can become eligible to consume the message. A publisher can send a message into a queue and expect a reply from the message consumer, but multiple subscribers cannot consume the message. This session feature enables multiplexing of streams of related messages through a single queue but cannot be consumed by multiple subscribers. This session feature enables multiplexed replies, allowing several publishers to share a reply queue, but a message cannot be consumed by multiple subscribers.

[Explore Service Bus message payloads and serialization - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/discover-azure-message-queue/5-messages-payloads-serialization)


---

You are developing a cloud native containerized background task application.

You need to choose the appropriate container deployment option based on the following requirements:

- Minimize cost
- Support service discovery and traffic splitting
- Enable event-driven application architecture
- Do not require access to native Kubernetes API

What should you use?

Select only one answer.

Azure Spring Apps

Azure Container Instances

**This answer is incorrect.**

Azure Container Apps

**This answer is correct.**

Azure Functions

This item tests the candidate’s knowledge of creating solutions by using Azure Container Apps. Azure Container Apps enables you to build serverless microservices based on containers. It is optimized for running general purpose containers and provides many application-specific concepts on top of containers. Azure Spring Apps is a fully managed service for Spring developers. It provides lifecycle management to run Spring Boot, Spring Cloud, or any other Spring applications on Azure. Azure Container Instances does not support scaling, load balancing, revisions, scale, or environments and does not meet the mentioned requirements. Azure Functions is a serverless Function as a Service (FaaS) solution. It can be used for running event-driven applications by using the functions programming model. However, it cannot be used to deploy a container image.

Learn link not available yet; scoping statement new for this OD. Noting that we need to update with the link when the content is live.

Noting that we need to update with the link when the content is live.

[Implement Azure Container Apps - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/implement-azure-container-apps/)

---
You need to read an Azure Cosmos DB change feed by using a push model.

Which two components can you use to achieve this goal? Each correct answer presents a complete solution.

Select all answers that apply.

Azure Functions with an Azure Cosmos DB trigger

**This answer is correct.**

Change feed processor library

**This answer is correct.**

Azure Functions with an Azure Event Grid trigger

Change feed pull model

**This answer is incorrect.**

This item tests the candidate’s knowledge of developing solutions that use Azure Cosmos DB storage.

Azure Functions with an Azure Cosmos DB trigger allows you to select the container to connect, and the Azure Function is triggered whenever there is a change in the container. The change feed processor library follows the observer pattern, where the processing function is called by the library. The change feed processor library will automatically check for changes and, if changes are found, push them to the client. Azure Functions with an Event Grid trigger will execute the function when an Event Grid event is dispatched. It has no relationship with an Azure Cosmos DB change feed. A change feed pull model will use a pull model rather than a push model.

[Consume an Azure Cosmos DB for NoSQL change feed using the SDK - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/consume-azure-cosmos-db-sql-api-change-feed-use-sdk/)

[Handle events with Azure Functions and Azure Cosmos DB for NoSQL change feed - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/handle-events-azure-functions-azure-cosmos-db-sql-api-change-feed/)

---
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
You are developing an application.

You need to set the standard HTTP properties of containers in Azure Blob Storage.

Which two HTTP properties can you set? Each correct answer presents part of the solution.

Select all answers that apply.

ETag

**This answer is correct.**

Last-Modified

**This answer is correct.**

Cache-Control

Origin

**This answer is incorrect.**

Range

This item tests the candidate’s knowledge of setting and retrieving properties and metadata. Metadata in Azure Storage objects is defined through headers starting with x-ms-meta-. Some standard HTTP properties are also available for both objects and containers. The only two HTTP properties that are available for containers are ETag and Last-Modified.

Last-Modified, Cache-Control, Origin and Range are properties only available for blobs.

[Set and retrieve properties and metadata for blob resources by using REST](https://learn.microsoft.com/training/modules/work-azure-blob-storage/5-set-retrieve-properties-metadata-rest)

---

You plan to develop an Azure App Service web app named **app1** by using a Windows custom container.

You need to load a TLS/SSL certificate in application code.

Which app setting should you configure?

Select only one answer.

`WEBSITE_LOAD_CERTIFICATES`

**This answer is correct.**

`WEBSITE_ROOT_CERTS_PATH`

`WEBSITE_CORS_ALLOWED_ORIGINS`

`WEBSITE_AUTH_TOKEN_CONTAINER_SASURL`

This item tests the candidate’s knowledge of configuring app settings, which is part of creating Azure App Service Web Apps.

The `WEBSITE_LOAD_CERTIFICATES` app setting makes the specified certificates accessible to Windows or Linux custom containers as files. The `WEBSITE_ROOT_CERTS_PATH` app setting is read-only and does not allow comma-separated thumbprint values to be mentioned to the certificates and then be loaded in the code. The `WEBSITE_AUTH_TOKEN_CONTAINER_SASURL` app setting is used to instruct the auth module to store and load all encrypted tokens to the specified blob storage container. This setting is used for Azure Storage and cannot be used to load certificates inside a Windows custom container.

[Configure web app settings - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-web-app-settings/)

---
You create an Azure web app locally. The web app consists of a ZIP package.

You need to deploy the web app by using the Azure CLI. The deployment must reduce the likelihood of locked files.

What should you do?

Select only one answer.

Run `az webapp deploy` specifying `–-clean true`.

**This answer is incorrect.**

Run `az webapp deploy` specifying `–-restart true`.

Run `az webapp deploy` to a staging slot with auto swap on.

**This answer is correct.**

Run `az webapp deploy` by using a high value for the `--timeout` parameter.

This item tests the candidate's knowledge of deploying Azure Web Apps using the Azure CLI.

Using a production and staging slot with auto swap enabled reduces the likelihood of locked files. If `–clean true` is used, the target folder is cleaned, but this has no effect on the likelihood of locked files. It is good to restart the app after deployment. This, however, is the default behavior of a ZIP deployment and has no effect on the reduced likelihood of locked files during deployment. The `--timeout` parameter has no effect on the likelihood of locked files.

[Deploy to App Service - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/introduction-to-azure-app-service/4-deploy-code-to-app-service?ns-enrollment-type=learningpath&ns-enrollment-id=learn.wwl.create-azure-app-service-web-apps)

---
You are a developing a serverless API using Azure Functions. The API is expected to handle a large number of HTTP requests and make outbound requests to a third-party service. The third-party service has a rate limit on the number of requests it can handle per minute.

You need to ensure that the Azure Function does not exceed the rate limit of the third-party service and manage resource utilization effectively.

Each correct answer presents part of the solution. Which two actions should you perform?

Select all answers that apply.

Enable 'dynamicThrottlesEnabled' property in the host.json file to reject requests with a 429 'Too Busy' response when system performance counters are over a high threshold.

**This answer is incorrect.**

Enable 'hsts' property in the host.json file to enforce HTTP Strict Transport Security (HSTS) behavior.

Set the 'maxConcurrentRequests' property in the host.json file to limit the number of parallel executions.

**This answer is correct.**

Set the 'maxOutstandingRequests' property in the host.json file to limit the number of outstanding requests at any given time.

**This answer is correct.**

Set the 'routePrefix' property in the host.json file to an empty string to remove the default prefix.

Setting the 'maxConcurrentRequests' property in the host.json file will limit the number of HTTP functions that are executed in parallel, which can help manage resource utilization and avoid exceeding the rate limit of the third-party service. The 'maxOutstandingRequests' property limits the number of outstanding requests that are held at any given time, including queued requests and in-progress executions, which can also help manage resource utilization. Enabling 'dynamicThrottlesEnabled' property would not help in this scenario as it rejects requests based on system performance counters, not based on the rate limit of a third-party service. The 'hsts' property is used to enforce HTTP Strict Transport Security (HSTS) behavior and is not related to managing resource utilization or rate limiting. The 'routePrefix' property is used to set the route prefix for all routes and does not affect resource utilization or rate limiting.

[Azure Functions HTTP triggers and bindings overview - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook?tabs=isolated-process%2Cfunctionsv2&pivots=programming-language-csharp)

---
You have an Azure subscription that contains an Azure Cosmos DB Core (SQL) API account. The account hosts two Azure Cosmos DB containers named Container1 and Container2.

You have an Azure Functions app named FunctionApp1.

You plan to create a function in FunctionApp1 that will process changes to Container1, and then write the results to Container2.

You need to ensure that the function reads the changes to Container1 immediately. The solution must minimize costs.

What should you do?

Select only one answer.

Configure FunctionApp1 to use the Consumption plan.

Configure FunctionApp1 to use the Premium plan.

Set the feedPollDelay parameter of the function to 0.

**This answer is correct.**

Set the feedPollDelay parameter of the function to -1.

The correct solution is to set the **feedPollDelay** parameter to **0**, because this controls how frequently the Azure Functions change feed processor polls for new changes in the Cosmos DB container. By default, there is a delay (typically 5 seconds) between polls to balance responsiveness and cost. Setting it to **0** ensures the function reads changes from Container1 immediately, which meets the requirement without needing to upgrade the hosting plan. Configuring the function to use the **Consumption** or **Premium** plan does not directly affect how quickly change feed events are read. Setting **feedPollDelay** to **-1** is invalid and would not achieve the desired result. Therefore, adjusting feedPollDelay to 0 is the most cost-effective solution.

[Quickstart: Respond to database changes in Azure Cosmos DB using Azure Functions](https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-cosmos-db-triggered-function)  
[Azure Cosmos DB trigger for Azure Functions 2.x and higher](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-trigger)

---
Question 27 of 50

You have a web service in Azure that uses an Azure SQL Database instance and is instrumented by using Application Insights.

You need to write a query to identify how long it takes for a specific web service call to retrieve data from the database.

Which type of data should you query in Application Insights?

Select only one answer.

customEvents

dependencies

**This answer is correct.**

performanceCounters

requests

**This answer is incorrect.**

The correct solution is to query **dependencies**, because Application Insights tracks external calls made by your service, including SQL Database queries, REST APIs, and storage operations. Dependency telemetry includes duration, success/failure, and target resource, making it ideal for measuring how long a web service call takes to retrieve data from the database. **customEvents** capture user-defined actions in the application but do not include database timings. **performanceCounters** provide system-level metrics such as CPU or memory usage, and **requests** represent incoming calls to the web service, not outbound database calls. Therefore, dependency data is the right source for identifying query durations to Azure SQL Database.

[Use Azure Application Insights](https://learn.microsoft.com/en-us/training/modules/configure-azure-app-services/10-use-application-insights)  
[Monitor Azure resources with Azure Monitor](https://learn.microsoft.com/en-us/azure/azure-monitor/platform/monitor-azure-resource)  
[Describe Azure Monitor](https://learn.microsoft.com/en-us/training/modules/describe-monitoring-tools-azure/4-describe-azure-monitor)  
[Monitor your networks using Azure Monitor](https://learn.microsoft.com/en-us/training/modules/design-implement-network-monitoring/2-monitor-networks-using-azure-monitor)

---
Question 34 of 50

You have an Azure event hub.

You need to add partitions to the event hub.

Which code segment should you use?

Select only one answer.

`az eventhubs eventhub consumer-group update --resource-group MyResourceGroupName --namespace-name MyNamespaceName --eventhub-name MyEventHubName --set partitioncount=12`

`az eventhubs eventhub consumer-group create --resource-group MyResourceGroupName --namespace-name MyNamespaceName --eventhub-name MyEventHubName --set partitioncount=12`

`az eventhubs eventhub update --resource-group MyResourceGroupName --namespace-name MyNamespaceName --name MyEventHubName --partition-count 12`

**This answer is correct.**

`az eventhubs eventhub create --resource-group MyResourceGroupName --namespace-name MyNamespaceName --name MyEventHubName --partition-count 12`

This item tests the candidate’s knowledge of developing event-based solutions.

The code segment that includes `az eventhubs eventhub update` adds partitions to an existing event hub. The code segment that includes `az eventhubs eventhub consumer-group update` updates the event hub consumer group. The code segment that includes `az eventhubs eventhub consumer-group create` will create an event hub consumer group. The code segment that includes `az eventhubs eventhub create --resource-group` segment will create an event hub with partitions, not change an existing one

[Control Azure services with the CLI - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/control-azure-services-with-cli/)

---
Question 39 of 50

A company is developing an IoT solution for smart buildings that collects telemetry data from various sensors. The data is sent to Azure for real-time analysis and storage.

You need to implement a solution that allows the ingestion of high volumes of events and provides reliable delivery to downstream processing services with minimal latency.

Which service should you use?

Select only one answer.

Azure Blob Storage

Azure Event Grid

**This answer is incorrect.**

Azure Event Hubs

**This answer is correct.**

Azure Service Bus

Azure Event Hubs is designed for high-throughput, real-time event streaming and is compatible with Apache Kafka, making it suitable for IoT scenarios. Azure Event Grid is more suited for event routing and serverless applications. Azure Service Bus is better for traditional enterprise messaging patterns, and Azure Blob Storage is not optimized for real-time event ingestion.

[Explore Azure Event Grid - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/azure-event-grid/2-event-grid-overview)  
[Discover Azure Event Hubs - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/azure-event-hubs/2-event-hubs-overview)  
[What is Azure Event Grid? - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/event-grid/overview)

---
Question 40 of 50

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

This item tests the candidate’s knowledge of implementing solutions that use Azure Service Bus.

A SqlFilter holds a SQL-like conditional expression that is evaluated in the broker against the arriving message’s user-defined properties and system properties. The TrueFilter and FalseFilter either cause all arriving messages (true) or none of the arriving messages (false) to be selected for the subscription. A CorrelationFilter holds a set of conditions that are matched against one or more of an arriving message's user and system properties. Size Filter and Content are not valid options for Service Bus topic filtering.

[Implement message-based communication workflows with Azure Service Bus - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-message-workflows-with-service-bus/)

---
Question 43 of 50

You plan to use Microsoft Graph to retrieve a list of users in a Microsoft Entra ID tenant.

You need to optimize query results.

Which two query options should you use? Each correct answer presents part of the solution.

Select all answers that apply.

`$filter`

**This answer is correct.**

`$count`

**This answer is incorrect.**

`$orderby`

`$select`

**This answer is correct.**

`$expand`

This item tests the candidate's knowledge of Microsoft Graph query options.

The `$filter` query option must be used to limit the results returned. The `$select` query option limits the attributes projected from the result set, making the query more efficient. The `$count` query option is meant to retrieve the total count of matching resources. `$expand` query option is used to retrieve related resources.

[Query Microsoft Graph by using REST - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/microsoft-graph/3-microsoft-graph-api)