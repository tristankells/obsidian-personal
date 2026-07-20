
## [[1 - Implement Azure App Service web apps - Explore Azure App Service]]

### Azure Training Practical Exercises

- [ ] **6. Quickstart Follow-Along:**
    - [ ] Complete the guided quickstart for deploying from a local filesystem to get another perspective on deployment: [Build and deploy to Azure Container Apps](https://learn.microsoft.com/en-us/azure/container-apps/quickstart-code-to-cloud?tabs=bash%2Ccsharp). (Note: This links to Container Apps, which is a related but different service. It's still a valuable exercise).

### Custom Practical Exercises

- [ ] **1. Automated Deployment from GitHub:**
    - [ ] **Goal:** Set up a continuous deployment pipeline from a GitHub repository to an Azure App Service.
    - [ ] Create a simple web app (e.g., Node.js, Python, or a static HTML site) and push it to a GitHub repository.
    - [ ] Create an Azure App Service.
    - [ ] In the App Service's "Deployment Center," connect it to your GitHub repository and configure it to automatically build and deploy when you push changes to the main branch.
    - [ ] Make a change to your code, push it to GitHub, and watch the deployment happen automatically.
- [ ] **2. Staging and Production with Deployment Slots:**
    - [ ] **Goal:** Implement a safe deployment strategy using staging and production slots. (Requires Standard tier or higher).
    - [ ] Create a "staging" deployment slot for your App Service.
    - [ ] Configure your CI/CD pipeline to deploy to the "staging" slot instead of production.
    - [ ] After a successful deployment to staging, perform a manual swap to move the new code to production.
- [ ] **3. Containerized Deployment:**
    - [ ] **Goal:** Deploy a containerized version of your web app to App Service.
    - [ ] Dockerize your web app by creating a `Dockerfile`.
    - [ ] Push the Docker image to a container registry (like Azure Container Registry or Docker Hub).
    - [ ] Create a new App Service configured to run a container.
    - [ ] Point the App Service to your container image and configure it to automatically pull the latest version on new deployments.
    - [ ] **Bonus:** Set up a CI/CD pipeline that builds the Docker image, pushes it to the registry, and then triggers the App Service to update.
- [ ] **4. Built-in Authentication:**
    - [ ] **Goal:** Secure your App Service with a federated identity provider without changing your app's code.
    - [ ] In the App Service "Authentication" blade, enable authentication.
    - [ ] Add an identity provider (e.g., Microsoft Entra ID or GitHub).
    - [ ] Configure it to require authentication for all requests.
    - [ ] Access your app and verify that you are redirected to a login page.
- [ ] **5. Network Security:**
    - [ ] **Goal:** Restrict access to your App Service.
    - [ ] In the "Networking" > "Access restrictions" section, add a rule that denies all traffic.
    - [ ] Add a second rule with a higher priority that allows access only from your current IP address.
    - [ ] Verify that you can still access the app, but it would be inaccessible from other networks.

## [[2 - Implement Azure App Service web apps - Configure web app settings]]

### Custom Practical Exercises

- [ ] **1. Externalize Configuration with Application Settings:**
    - [ ] **Goal:** Move a sensitive setting from your application's code or configuration file to Azure App Service Application Settings.
    - [ ] If your "Envelopes" app has a database connection string hard-coded or in a local `appsettings.json`, create a new Application Setting in your App Service.
    - [ ] Name it `ConnectionStrings:DefaultConnection` (or a similar appropriate name for your app's language).
    - [ ] Set its value to your actual database connection string.
    - [ ] Modify your application code to read the connection string from environment variables.
    - [ ] Deploy and verify that the app successfully connects to the database using the setting from Azure.
- [ ] **2. Optimize Cost with "Always On":**
    - [ ] **Goal:** Understand the purpose and cost implication of the "Always On" setting.
    - [ ] Find the "Always On" setting in your App Service's General Settings.
    - [ ] If your App Service plan is Basic or higher, this setting is available. For a non-production or low-traffic app, turning it **off** can save money because the app will go idle after a period of inactivity.
    - [ ] Turn it off and observe the "cold start" time after the app has been idle.
- [ ] **3. Remote Debugging:**
    - [ ] **Goal:** Attach a remote debugger from Visual Studio to a live App Service.
    - [ ] In your App Service's General Settings, enable Remote Debugging for your version of Visual Studio.
    - [ ] In Visual Studio, open your project, go to the "Debug" menu, and select "Attach to Process."
    - [ ] Find your App Service instance and attach the debugger to the `w3wp.exe` process.
    - [ ] Set a breakpoint and access your application to hit the breakpoint, allowing you to inspect live code execution in Azure.
- [ ] **4. Diagnostic Logging:**
    - [ ] **Goal:** Enable and view application and web server logs to diagnose issues.
    - [ ] In the "App Service logs" settings, enable "Application Logging" (to the filesystem).
    - [ ] Add some log statements to your application code (e.g., `console.log` in Node.js, `ILogger` in .NET).
    - [ ] Deploy the changes.
    - [ ] Use the "Log stream" feature to view the logs in real-time as you interact with your application. This is crucial for debugging issues in a live environment.

## [[3 - Implement Azure Web Apps - Scale apps in Azure App Service]]

### Custom Practical Exercises

- [ ] **1. Metric-Based Scaling:**
    - [ ] **Goal:** Configure an App Service to scale out when CPU usage is high and scale back in when it's low.
    - [ ] Deploy a simple web app to an App Service Plan (Standard tier or above).
    - [ ] In the App Service, navigate to the "Scale out (App Service plan)" settings.
    - [ ] Create a new autoscale rule based on a metric.
    - [ ] **Scale-out rule:** If "CPU Percentage" is greater than 70% for 10 minutes, increase the instance count by 1.
    - [ ] **Scale-in rule:** If "CPU Percentage" is less than 30% for 10 minutes, decrease the instance count by 1.
    - [ ] Set the minimum and maximum instance counts (e.g., min: 1, max: 4).
    - [ ] **(Optional)** Use a load testing tool (like Azure Load Testing or a simple script) to generate traffic and trigger the scale-out rule. Monitor the "Run history" to see the scaling events.
- [ ] **2. Schedule-Based Scaling:**
    - [ ] **Goal:** Configure the App Service to have more instances during peak business hours and fewer instances overnight and on weekends.
    - [ ] In the autoscale settings, create a new scale condition with a specific schedule.
    - [ ] **Weekday Schedule:** For Monday to Friday, from 9:00 AM to 5:00 PM, set the instance count to a minimum of 2.
    - [ ] **Default Schedule:** For all other times, let the instance count default to 1.
    - [ ] This demonstrates how to prepare for predictable traffic patterns without relying on metrics.
- [ ] **3. Avoid "Flapping":**
    - [ ] **Goal:** Understand and prevent rapid scaling in and out.
    - [ ] Review your metric-based rules. Notice that the scale-out threshold (70%) and scale-in threshold (30%) are far apart.
    - [ ] Consider what would happen if the thresholds were very close (e.g., scale out at 70%, scale in at 65%). The system could "flap" by constantly adding and removing instances. This exercise is to recognize the importance of having a significant margin between scale-out and scale-in rules.

## [[4 - Implement Azure App Service web apps - Explore Azure App Service deployment slots]]

### Custom Practical Exercises

- [ ] **1. Create a Staging Slot:**
    - [ ] **Goal:** Set up a non-production slot to test changes safely.
    - [ ] Deploy a simple web app to the production slot of an App Service.
    - [ ] Use the Azure CLI (`az webapp deployment slot create`) to create a new slot named "staging".
    - [ ] In the Azure portal, verify that the new slot has been created and has its own URL.
- [ ] **2. Deploy to the Staging Slot and Warm Up:**
    - [ ] **Goal:** Deploy new code to the staging slot and ensure it's ready before it receives production traffic.
    - [ ] Make a visible change to your web app's code (e.g., change a title from "v1" to "v2").
    - [ ] Deploy the updated code to the "staging" slot using `az webapp deploy`.
    - [ ] Access the staging slot's URL directly (`<app-name>-staging.azurewebsites.net`) to verify the "v2" changes are live. This also "warms up" the slot.
- [ ] **3. Perform a Manual Swap:**
    - [ ] **Goal:** Promote the code from the staging slot to the production slot with zero downtime.
    - [ ] Use the Azure CLI (`az webapp deployment slot swap`) to swap the "staging" and "production" slots.
    - [ ] Immediately after the swap, access the production URL. It should now show the "v2" content.
    - [ ] Access the staging URL. It should now show the original "v1" content, providing an instant rollback path.
- [ ] **4. A/B Testing with Traffic Routing:**
    - [ ] **Goal:** Route a percentage of production traffic to the staging slot to test a new feature with a subset of users.
    - [ ] Deploy a new feature or change to the "staging" slot.
    - [ ] In the App Service "Deployment slots" settings in the portal, adjust the traffic percentage for the staging slot from 0% to 20%.
    - [ ] Now, 20% of users visiting the main production URL will be randomly routed to the new version in the staging slot. This is a powerful way to test new features in a controlled manner.
- [ ] **5. Slot-Specific Settings:**
    - [ ] **Goal:** Understand how to keep certain settings (like database connection strings) tied to a specific slot.
    - [ ] In the "staging" slot's configuration, create a new Application Setting called `DatabaseConnectionString` with a value like "staging-db-connection".
    - [ ] Mark this setting as a "deployment slot setting".
    - [ ] Perform a swap.
    - [ ] After the swap, check the application settings for both the production and staging slots. The `DatabaseConnectionString` should have remained in the staging slot, demonstrating that sensitive or environment-specific settings don't get swapped into production.

## [[5 - Explore Azure Functions]]

### Custom Practical Exercises

- [ ] **1. Create and Deploy a "Hello World" Function:**
    - [ ] **Goal:** Understand the basic workflow of creating and deploying a function.
    - [ ] Use the Azure Functions extension in Visual Studio Code to create a new project.
    - [ ] Choose an HTTP trigger and a language of your choice (e.g., C#, Python, or JavaScript).
    - [ ] Run the function locally to test it.
    - [ ] Deploy the function to a new Function App in Azure.
    - [ ] Test the deployed function by accessing its public URL.
- [ ] **2. Implement a Real-World Scenario with Triggers and Bindings:**
    - [ ] **Goal:** Create a function that automatically processes data, simulating a real-world task.
    - [ ] **Scenario:** An Azure Function that creates a backup of your "envelopes" data.
    - [ ] **Trigger:** Use a **Timer Trigger** to run the function on a schedule (e.g., every night at 1 AM).
    - [ ] **Input Binding (Optional):** If your data is in Azure Cosmos DB or Table Storage, use an input binding to fetch the data to be backed up.
    - [ ] **Output Binding:** Use an **Output Binding** to save the backup data. A good choice would be to write the data as a JSON file to an Azure Blob Storage container. You could also explore bindings for third-party services like Google Drive if available or by using their SDKs directly.
- [ ] **3. Centralized Monitoring:**
    - [ ] **Goal:** Learn how to monitor function executions and diagnose issues.
    - [ ] After your function has run a few times (either via HTTP calls or the timer), navigate to the Function App in the Azure portal.
    - [ ] Use the **Monitor** tab to view a log of past executions. Check for successes and failures.
    - [ ] Integrate your Function App with **Application Insights** (often done by default) to explore more detailed telemetry, such as performance metrics, dependencies, and exceptions.
- [ ] **4. Explore Different Deployment Methods:**
    - [ ] **Goal:** Understand the various ways to deploy code to a Function App.
    - [ ] **Visual Studio / VS Code:** You've already done this, but recognize it as the primary "inner loop" development method.
    - [ ] **Azure CLI:** Use the `az functionapp deployment source config-zip` command to deploy your function from a .zip file. This is common for CI/CD pipelines.
    - [ ] **(Optional) GitHub Actions:** Create a simple GitHub Actions workflow that automatically deploys your function whenever you push changes to your repository's main branch.

## [[6 - Develop Azure Functions]]

### Custom Practical Exercises

- [ ] **1. Local Development with VS Code:**
    - [ ] **Goal:** Create, run, and debug an Azure Function entirely on your local machine.
    - [ ] Use the VS Code command palette (`F1` or `Ctrl+Shift+P`) and select `Azure Functions: Create New Project...`.
    - [ ] Choose an HTTP trigger and your preferred language.
    - [ ] Set a breakpoint in your function's code.
    - [ ] Press `F5` to start the local Functions host and debugger.
    - [ ] Access the local endpoint provided in the terminal to hit your breakpoint and inspect the request object.
- [ ] **2. Deploy and Test in Azure:**
    - [ ] **Goal:** Deploy your local function to the cloud and test it.
    - [ ] Use the VS Code Azure Functions extension to deploy your project to a new Function App in Azure.
    - [ ] Once deployed, find the function's public URL in the Azure portal or the VS Code extension.
    - [ ] Test the live endpoint to ensure it's working correctly in the cloud.
- [ ] **3. Use a Time-Based Trigger:**
    - [ ] **Goal:** Create a function that runs on a schedule.
    - [ ] Add a new function to your project.
    - [ ] This time, select the **Timer Trigger**.
    - [ ] Configure it to run every 5 minutes using the NCRONTAB expression `0 */5 * * * *`.
    - [ ] Add a log statement inside the function (e.g., "Timer function executed!").
    - [ ] Deploy the updated Function App.
    - [ ] Monitor the function's logs in the Azure portal (or via Application Insights Live Metrics) to see it execute every 5 minutes.
- [ ] **4. Explore Custom Bindings (Conceptual or Implemented):**
    - [ ] **Goal:** Understand how to connect Functions to services that don't have built-in bindings.
    - [ ] **Research:** Look for community-provided custom bindings for a service like Google Sheets or another third-party API you're interested in.
    - [ ] **Implementation (if a binding is found):**
        - Follow the instructions to install and configure the custom binding.
        - Create a function that uses an output binding to write a new row to a Google Sheet every time an HTTP trigger is called.
    - [ ] **SDK Fallback (if no binding is found):**
        - If a custom binding isn't available, use the official Google Sheets SDK (or another service's SDK) within your function code to connect and write data. This demonstrates that even without a binding, you can connect to any service.

## [[7 - Implement containerized solutions - Manage container images in Azure Container Registry]]

### Azure Training Practical Exercises

- [ ] **2. Follow the Microsoft Learn Exercise (if cost-effective):**
    - [ ] Complete the guided exercise: [Build and run a container image with Azure Container Registry Tasks](https://learn.microsoft.com/en-us/training/modules/publish-container-image-to-azure-container-registry/6-build-run-image-azure-container-registry). This will cover the fundamental steps.

### Custom Practical Exercises

- [ ] **1. Cost Analysis:**
    - [ ] Investigate the pricing tiers for Azure Container Registry (Basic, Standard, Premium).
    - [ ] Determine if there is a free tier or a free amount of storage/builds included.
- [ ] **3. Manual ACR Workflow:**
    - [ ] **Create an ACR Resource:**
        - Use the Azure CLI (`az acr create`) to provision a new container registry.
    - [ ] **Build and Push a Docker Image:**
        - Create a simple Dockerfile for a basic web app (e.g., a "Hello World" Node.js or Python app).
        - Build the Docker image locally using `docker build`.
        - Log in to your ACR instance using `az acr login`.
        - Tag the local image for your ACR (`docker tag`).
        - Push the image to your ACR (`docker push`).
    - [ ] **Verify the Image:**
        - Check the Azure portal to see the pushed image in your registry's repository.
        - Use `az acr repository list` and `az acr repository show-manifests` to verify via the CLI.
    - [ ] **Run the Image (Optional):**
        - Run the container image directly from ACR using Azure Container Instances (ACI) to test it.
- [ ] **4. Explore ACR Tasks for Automation:**
    - [ ] **Quick Task:**
        - Use `az acr build` to perform a one-time build and push of your Dockerfile directly in Azure, without needing Docker Desktop locally.
    - [ ] **Scheduled Task:**
        - Create an ACR Task that automatically builds and pushes your image on a set schedule (e.g., daily at midnight) using `az acr task create`.
    - [ ] **Multi-Step Task:**
        - Define a `acr-task.yaml` file to create a more complex workflow.
        - For example, a task that first builds a development image, runs a test container, and then, if successful, builds and pushes a production-tagged image.

## [[8 - Implement containerized solutions  Run container images in Azure Container Instances]]

### Azure Training Practical Exercises

- [ ] **2. Single Container Deployment with Azure CLI:**
    - [ ] Follow the official Microsoft Learn exercise to get a baseline understanding: [Deploy a container to Azure Container Instances](https://learn.microsoft.com/en-us/training/modules/create-run-container-images-azure-container-instances/3-run-azure-container-instances-cloud-shell).

### Custom Practical Exercises

- [ ] **1. Cost and Tier Analysis:**
    - [ ] Research the pricing model for Azure Container Instances. Is it purely consumption-based?
    - [ ] Determine if there's a free tier or a certain amount of free usage per month.
- [ ] **3. Multi-Container Deployment (Sidecar Pattern):**
    - [ ] **Goal:** Deploy the "Envelopes" budget app (or a similar two-part app) as a multi-container group in ACI. One container for the frontend, one for the backend.
    - [ ] **Deploy using YAML:**
        - Create a `deploy-aci.yaml` file.
        - Define two containers in the `properties.containers` section.
        - Configure the necessary ports and environment variables for each.
        - Deploy it using `az container create --file deploy-aci.yaml`.
    - [ ] **Deploy using ARM Template:**
        - Create an Azure Resource Manager template (`template.json`).
        - Define the container group and its containers within the template.
        - This is more complex but good practice for integrating with other Azure resources. Deploy it using `az deployment group create`.
- [ ] **4. Configuration and Data Persistence:**
    - [ ] **Passing Environment Variables:**
        - When deploying a container, use the `--environment-variables` flag in the `az container create` command to pass configuration settings (e.g., `API_URL=...`).
    - [ ] **Mounting Persistent Storage:**
        - **Cost Research:** First, investigate the cost of Azure Files, as it's a common way to provide persistent storage to ACI. Check for a free tier.
        - **Create an Azure File Share:** Use `az storage share create`.
        - **Mount the Share:** When creating a container instance, use the `--azure-file-volume-` parameters to mount the file share as a volume inside your container. This is ideal for persisting database files, logs, or user uploads.

## [[9 -  Implement containerized solutions - Implement Azure Container Apps]]

### Azure Training Practical Exercises

- [ ] **1. Basic Deployment:**
    - [ ] Follow the official Microsoft Learn exercise to deploy your first container app: [Deploy a container to Azure Container Apps with the Azure CLI](https://learn.microsoft.com/en-us/training/modules/implement-azure-container-apps/3-exercise-deploy-app).

### Custom Practical Exercises

- [ ] **2. Explore Dapr Integration:**
    - [ ] **Goal:** Build a simple application that uses Dapr for state management or pub/sub messaging.
    - [ ] **State Management:** Create a simple counter app where the count is persisted using the Dapr state management API.
    - [ ] **Pub/Sub:** Create two container apps—a "publisher" and a "subscriber"—that communicate through the Dapr pub/sub API.
- [ ] **3. Multi-Container App with Sidecar:**
    - [ ] **Goal:** Deploy an application that uses the sidecar pattern (e.g., a main application container and a logging or monitoring sidecar).
    - [ ] Create a Container App with two containers. The main container could be a simple API, and the sidecar could be a logging agent that tails a log file from a shared volume.
- [ ] **4. Built-in Authentication:**
    - [ ] **Goal:** Secure a container app without writing any authentication code.
    - [ ] Deploy a simple web app.
    - [ ] Use the Azure CLI (`az containerapp auth`) or the Azure portal to enable authentication with a federated identity provider like Microsoft Entra ID or GitHub.
    - [ ] Try to access the app and verify that you are redirected to the login page.
- [ ] **5. Secrets Management:**
    - [ ] **Goal:** Pass a secret to a container app securely.
    - [ ] Create a secret using `az containerapp secret set`.
    - [ ] In your container app definition, create an environment variable that references the secret using the `secretref` syntax.
    - [ ] Access the environment variable from your application code to confirm the secret was passed securely.
- [ ] **6. Revisions and Traffic Splitting:**
    - [ ] **Goal:** Practice a blue-green deployment.
    - [ ] Deploy an initial version (revision) of your container app.
    - [ ] Make a small change to your application (e.g., change a "v1" text to "v2").
    - [ ] Deploy a new revision of the app without directing any traffic to it yet.
    - [ ] Manually split the traffic, sending a small percentage (e.g., 10%) to the new revision to test it.
    - [ ] Once verified, shift 100% of the traffic to the new revision.
