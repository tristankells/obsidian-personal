# Summary
- After this module, you'll...
	- Explain difference between Azure Functions, Azure Logic Apps and Webjobs
	- Describe Azure Functions hosting plan options.
	- Describe how Azure functions scall to meet business demand.
# Links
- [Explore Azure Functions - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/explore-azure-functions/)
# Module assessment
> [!question] Question 1 An organization wants to implement a serverless workflow to solve a business problem. One of the requirements is the solution needs to use a designer-first (declarative) development model. Which of the choices below meets the requirements?
> 
> - Azure Functions
> - Azure Logic Apps
> - WebJobs
> 
> > [!success]- Answer 
> > Azure Logic Apps

> [!question] Question 2 What is a key benefit of the Flex Consumption plan in Azure Functions hosting options?
> 
> - It provides fully predictable billing and manual scale instances.
> - It offers high scalability with compute choices, virtual networking, and pay-as-you-go billing.
> - It allows for the packaging of custom libraries with function code.
> 
> > [!success]- Answer 
> > It offers high scalability with compute choices, virtual networking, and pay-as-you-go billing.

> [!question] Question 3 What is the maximum number of instances for a function app on a Consumption plan in Windows?
> 
> - 300
> - 100
> - 200
> 
> > [!success]- Answer 
> > 200
# Notes
- Azure Functions
	- Built on top of Webjobs SDK.
	- Imperative
		- Code first
	- Triggers
		- Input
	- Bindings
		- Output
	- Plans 
		- Consumption
			- Pay as you go.
			- Limited to 5 mins execution time.
			- Windows only.
			- Automatic scaling.
			- Suffer cold starts.
		- Consumption Flex
			- This and beyond, limited to 30+ mins.
		- Premium
			- This and beyond, includes Linux Containers.
			- This and beyond, no cold starts.
			- Virtual network connectivity,
		- Dedicated
			- Set bill.
		- Container Apps
			- Kubernetes abstraction.
			- Required to ship with additional libraries.
- Azure Logic Apps
	- Declarative
		- Designer first
	- Library pre-built actions.
- Webjobs
	- Just use Functions...
		- Unless need file system trigger


# Flashcards

- What is the maximum number of instances for a Functions app on a Consumption plan in Windows?
	- 200
- What trigger does WebJobs have that Functions do not?
	- File system
- What two additional options do Logic Apps provide for management, compared to Functions?
	- Powershell & Azure Portal.
- What is the default and maximum execution for Functions on the **Consumption plan**?
	- 5 & 10 mins.
- What Functions plans support containers?
	- Premium, Dedicated and Container apps.
- What is the maximum number of instances for a Functions app on a Consumption plan in Linux?
	- 100.
# 🛠 Practice Exercises
**Objective:** Get hands-on experience with Azure Functions by creating, deploying, and monitoring a simple serverless function.

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