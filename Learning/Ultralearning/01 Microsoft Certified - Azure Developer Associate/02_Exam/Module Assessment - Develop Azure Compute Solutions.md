
## [[1 - Implement Azure App Service web apps - Explore Azure App Service]]

> [!question] Question 1
> Which of the following App Service plan categories provides the maximum scale-out capabilities?
> - Dedicated compute
> - Isolated
> - Shared compute
> 
> > [!success]- Answer
> > Isolated

> [!question] Question 2
> Which of the following networking features of App Service can be used to control outbound network traffic?
> - App-assigned address
> - Hybrid Connections
> - Service endpoints
> 
> > [!success]- Answer
> > Hybrid Connections

> [!question] Question 3
> What is the purpose of the Azure App Service Environment feature?
> - It provides a shared infrastructure for running App Service apps.
> - It allows for the deployment and running of containerized web apps on Windows and Linux.
> - It provides a fully isolated and dedicated environment for running App Service apps with improved security at high scale.
> 
> > [!success]- Answer
> > It provides a fully isolated and dedicated environment for running App Service apps with improved security at high scale.

> [!question] Question 4
> What determines the set of compute resources for a web app to run in Azure App Service?
> - The geographical region where the app is deployed
> - The pricing tier of the app
> - The App Service plan
> 
> > [!success]- Answer
> > The App Service plan

> [!question] Question 5
> What is the purpose of using deployment slots in Azure App Service?
> - To deploy an app to a staging environment and then swap staging and production slots, eliminating downtime
> - To increase the storage capacity of the application
> - To add up to nine sidecar containers for each sidecar-enabled custom container app
> 
> > [!success]- Answer
> > To deploy an an app to a staging environment and then swap staging and production slots, eliminating downtime

## [[2 - Implement Azure App Service web apps - Configure web app settings]]

> [!question] Question 1
> What is the purpose of the "General settings" section in the Azure App Service configuration?
> - To configure custom domain names and SSL certificates for the web app
> - To manage the application's connection strings and app settings
> - To configure platform settings such as runtime stack, bitness, and WebSocket support
> 
> > [!success]- Answer
> > To configure platform settings such as runtime stack, bitness, and WebSocket support

> [!question] Question 2
> What is the function of the "Path mappings" configuration in Azure App Service?
> - To configure custom startup commands for the web app
> - To map virtual directory paths to physical directory paths
> - To manage the application's diagnostic logging settings
> 
> > [!success]- Answer
> > To map virtual directory paths to physical directory paths

> [!question] Question 3
> What is the purpose of the "Always On" setting in Azure App Service?
> - To ensure that the web app is always running, even if there is no traffic
> - To automatically scale the web app based on demand
> - To enable remote debugging for the web app
> 
> > [!success]- Answer
> > To ensure that the web app is always running, even if there is no traffic

## [[3 - Implement Azure Web Apps - Scale apps in Azure App Service]]

> [!question] Question 1
> What are the two ways to scale an App Service plan?
> - Scale up and scale out
> - Scale in and scale down
> - Scale left and scale right
> 
> > [!success]- Answer
> > Scale up and scale out

> [!question] Question 2
> What is the difference between scaling up and scaling out?
> - Scaling up adds more VM instances, while scaling out increases the resources of the existing VM instances.
> - Scaling up increases the resources of the existing VM instances, while scaling out adds more VM instances.
> - Scaling up and scaling out are the same thing.
> 
> > [!success]- Answer
> > Scaling up increases the resources of the existing VM instances, while scaling out adds more VM instances.

> [!question] Question 3
> What is autoscale in Azure App Service?
> - A feature that allows you to manually scale your App Service plan.
> - A feature that automatically scales your App Service plan based on a set of rules and schedules.
> - A feature that allows you to scale your App Service plan to a different region.
> 
> > [!success]- Answer
> > A feature that automatically scales your App Service plan based on a set of rules and schedules.

## [[4 - Implement Azure App Service web apps - Explore Azure App Service deployment slots]]

> [!question] Question 1
> What is the primary benefit of using deployment slots in Azure App Service?
> - They allow you to run different versions of your app simultaneously for A/B testing.
> - They provide a way to deploy new versions of your app with zero downtime.
> - They enable you to scale your app to different geographical regions.
> 
> > [!success]- Answer
> > They provide a way to deploy new versions of your app with zero downtime.

> [!question] Question 2
> When you swap two deployment slots, what happens to the app's settings?
> - All settings are swapped along with the app content.
> - Only the app content is swapped; settings remain with the slot.
> - Some settings are swapped, while others (slot-specific settings) remain with the slot.
> 
> > [!success]- Answer
> > Some settings are swapped, while others (slot-specific settings) remain with the slot.

> [!question] Question 3
> What is a "swap with preview"?
> - It's a type of swap that allows you to preview the changes in the production slot before completing the swap.
> - It's a feature that automatically rolls back a swap if errors are detected.
> - It's a swap that only deploys a small percentage of traffic to the new version.
> 
> > [!success]- Answer
> > It's a type of swap that allows you to preview the changes in the production slot before completing the swap.

## [[5 - Explore Azure Functions]]

> [!question] Question 1
> What is a trigger in Azure Functions?
> - A trigger is the event that starts a function.
> - A trigger is a connection to a data source.
> - A trigger is a way to schedule a function to run at a specific time.
> 
> > [!success]- Answer
> > A trigger is the event that starts a function.

> [!question] Question 2
> What is a binding in Azure Functions?
> - A binding is a declarative way to connect data and services to your function.
> - A binding is a way to secure your function.
> - A binding is a way to monitor your function's execution.
> 
> > [!success]- Answer
> > A binding is a declarative way to connect data and services to your function.

> [!question] Question 3
> What are the three hosting plans for Azure Functions?
> - Consumption, Premium, and App Service Plan
> - Basic, Standard, and Premium
> - Free, Shared, and Dedicated
> 
> > [!success]- Answer
> > Consumption, Premium, and App Service Plan

## [[6 - Develop Azure Functions]]

> [!question] Question 1
> How do you create a new Azure Function in Visual Studio Code?
> - By using the Azure Functions extension and selecting "Create New Project".
> - By creating a new file with a `.func` extension.
> - By using the `func new` command in the terminal.
> 
> > [!success]- Answer
> > By using the Azure Functions extension and selecting "Create New Project".

> [!question] Question 2
> What is the purpose of the `function.json` file?
> - It contains the code for the function.
> - It defines the function's trigger, bindings, and other configuration settings.
> - It stores the application settings for the function app.
> 
> > [!success]- Answer
> > It defines the function's trigger, bindings, and other configuration settings.

> [!question] Question 3
> What is the difference between an input binding and an output binding?
> - An input binding sends data to the function, while an output binding receives data from the function.
> - An input binding reads data from a data source, while an output binding writes data to a data source.
> - There is no difference between input and output bindings.
> 
> > [!success]- Answer
> > An input binding reads data from a data source, while an output binding writes data to a data source.

## [[7 - Implement containerized solutions - Manage container images in Azure Container Registry]]

> [!question] Question 1
> What is the primary purpose of Azure Container Registry (ACR)?
> - To run containerized applications.
> - To build and store container images.
> - To orchestrate container deployments.
> 
> > [!success]- Answer
> > To build and store container images.

> [!question] Question 2
> What is a webhook in Azure Container Registry?
> - A feature that allows you to automate tasks when an image is pushed to the registry.
> - A way to secure access to the registry.
> - A tool for scanning images for vulnerabilities.
> 
> > [!success]- Answer
> > A feature that allows you to automate tasks when an image is pushed to the registry.

> [!question] Question 3
> What is the benefit of using ACR Tasks?
> - It allows you to build container images in the cloud, without needing Docker on your local machine.
> - It provides a way to run containers on a schedule.
> - It automatically deploys images to Azure Kubernetes Service (AKS).
> 
> > [!success]- Answer
> > It allows you to build container images in the cloud, without needing Docker on your local machine.

## [[8 - Implement containerized solutions  Run container images in Azure Container Instances]]

> [!question] Question 1
> What is the main advantage of using Azure Container Instances (ACI)?
> - It provides a full-fledged container orchestration platform.
> - It allows you to run containers without managing any underlying infrastructure.
> - It is the most cost-effective way to run containers in Azure.
> 
> > [!success]- Answer
> > It allows you to run containers without managing any underlying infrastructure.

> [!question] Question 2
> How can you provide a publicly accessible DNS name for a container group in ACI?
> - By configuring a public IP address for the container group.
> - By creating a CNAME record in your DNS zone.
> - By using a custom domain name.
> 
> > [!success]- Answer
> > By configuring a public IP address for the container group.

> [!question] Question 3
> What is a sidecar container in the context of ACI?
> - A container that runs alongside the main container in a container group.
> - A container that is used for monitoring and logging.
> - A container that is used to build the main container image.
> 
> > [!success]- Answer
> > A container that runs alongside the main container in a container group.

## [[9 -  Implement containerized solutions - Implement Azure Container Apps]]

> [!question] Question 1
> What is a key feature of Azure Container Apps that distinguishes it from Azure Container Instances (ACI)?
> - It is built on top of Kubernetes, providing more advanced features like scaling, load balancing, and service discovery.
> - It is a serverless container offering, where you only pay for the resources your container consumes.
> - It is designed for single, long-running containers.
> 
> > [!success]- Answer
> > It is built on top of Kubernetes, providing more advanced features like scaling, load balancing, and service discovery.

> [!question] Question 2
> What is a "revision" in Azure Container Apps?
> - A snapshot of a container app's configuration and code.
> - A way to roll back to a previous version of a container app.
> - Both of the above.
> 
> > [!success]- Answer
> > Both of the above.

> [!question] Question 3
> What is Dapr, and how is it integrated with Azure Container Apps?
> - Dapr is a portable, event-driven runtime that simplifies building microservices. It is natively integrated into Container Apps, providing features like service-to-service invocation and state management.
> - Dapr is a container orchestration platform.
> - Dapr is a monitoring and logging tool for containerized applications.
> 
> > [!success]- Answer
> > Dapr is a portable, event-driven runtime that simplifies building microservices. It is natively integrated into Container Apps, providing features like service-to-service invocation and state management.
