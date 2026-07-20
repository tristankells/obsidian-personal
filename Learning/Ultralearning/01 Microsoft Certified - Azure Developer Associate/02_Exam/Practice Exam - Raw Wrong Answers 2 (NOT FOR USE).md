Question 7 of 50

You need to implement an Azure Storage lifecycle policy for append blobs.

Which rule action should you use?

Select only one answer.

delete

**This answer is correct.**

enableAutoTierToHotFromCool

**This answer is incorrect.**

tierToArchive

tierToCool

This item tests the candidate’s knowledge of configuring Azure Storage lifecycle policy for blobs, which is an essential part of developing solutions for blob storage.

The delete rule action supports both block blobs and append blobs. The enableAutoTierToHotFromCool, tierToArchive, and tierToCool rule actions only supports block blobs.

[Discover Blob storage lifecycle policies - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/manage-azure-blob-storage-lifecycle/3-blob-storage-lifecycle-policies)

---
Question 9 of 50

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
You develop an App Service app hosted on Windows Platform. Users report that the app is failing.

You need to begin troubleshooting the app by inspecting a copy of the page that is returned when the HTTP return code is greater than 400.

Which type of log should you review?

Select only one answer.

application

web server

detailed error

**This answer is correct.**

deployment

This item tests the candidate’s knowledge of using logs to troubleshoot web apps. The detailed error log contains copies of the error pages, produced in response to HTTP codes greater than 400, that would have been sent to clients. These pages are not sent due to security reasons. The web server log shows information about the raw HTTP request, such as method, bytes, and client user agent. The application log is application specific, logging information that your application code or components that are used by your application writes. The deployment log stores information to diagnose the reasons for a failed deployment.

[Enable diagnostic logging - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/configure-web-app-settings/5-enable-diagnostic-logging)

---
Question 43 of 50

A company plans to implement a Microsoft Defender for Cloud solution.

The company has the following requirements:

- Notifies when DNS domains are not deleted when a new Azure Functions app is deleted.
- Use native alerting.
- Minimize costs.

You need to select a hosting plan.

Which hosting plan should you use?

Select only one answer.

Consumption

Standard

**This answer is correct.**

Premium

Free

This item tests the candidate's knowledge about securing Azure Functions.

The Standard plan supports both custom domains and Microsoft Defender for Cloud, which can automatically alert on dangling DNS domains. The Consumption plan is incorrect because it does not support Microsoft Defender for Cloud. This can automatically alert on dangling DNS domains. The Premium plan supports custom domains and Microsoft Defender for Cloud, which can automatically alert on dangling DNS domains. This, however, is not the lowest cost option. The Free plan does not support custom domains, although it does support Microsoft Defender for Cloud, which can automatically alert on dangling DNS domains.

[Overview of Defender for App Service to protect your Azure App Service web apps and APIs - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-app-service-introduction "Overview of Defender for App Service to protect your Azure App Service web apps and APIs - Training | Microsoft Learn")

---
Question 44 of 50

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

**This answer is incorrect.**

This item tests the candidate’s knowledge of working with timer triggers in Azure Functions.

The code segment that includes `Run([TimerTrigger("0 */15 * * * 1-5")` executes the function every 15 minutes from Monday to Friday. The code segment that includes `Run([TimerTrigger("*/15 * * * 0-4")` is missing the second part, and it is not using the proper range for days of the week. The code segment that includes `Run([TimerTrigger("0 15 * * * ")` executes only once at 15:00 (3 PM). The code segment that includes `Run([TimerTrigger("* 15 * * 1-5")` is missing the seconds attribute and the step (‘/’) part for the minutes.

https://learn.microsoft.com/training/modules/execute-azure-function-with-triggers/

[Timer trigger for Azure Functions - Training | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-timer?tabs=python-v2%2Cisolated-process%2Cnodejs-v4&pivots=programming-language-csharp)

---
Question 50 of 50

You have an Azure App Service web app.

You enable Application Insights for the app.

You need to view detailed information about each user who signs in to the app, including what the user does while signed in.

Which type of telemetry data should you filter by using Application Insights?

Select only one answer.

dependencies

events

**This answer is correct.**

requests

traces

**This answer is incorrect.**

The correct solution is to filter by **events**, because Application Insights events are custom telemetry designed to track user actions and behaviors inside the app, such as button clicks, page navigation, or other activities performed while signed in. **Requests** represent incoming HTTP calls to the app and provide details about performance and response codes, but they don’t capture what a user does within the app. **Dependencies** track calls to external resources like databases or APIs, and **traces** log diagnostic information from the application. To understand **per-user activity** inside the application, events are the appropriate telemetry type.

[Summary](https://learn.microsoft.com/en-us/training/modules/route-system-feedback/5-summary)  
[Implement Application Insights](https://learn.microsoft.com/en-us/training/modules/implement-tools-track-usage-flow/7-implement-application-insights)  
[Use Azure Application Insights](https://learn.microsoft.com/en-us/training/modules/configure-azure-app-services/10-use-application-insights)  
[Monitor Azure resources with Azure Monitor](https://learn.microsoft.com/en-us/azure/azure-monitor/platform/monitor-azure-resource)