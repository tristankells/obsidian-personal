# Summary
After completing you will be able to:
- Explain the key components of a function and how they are structured
- Create triggers and bindings to control when a function runs and where the output is directed
- Connect a function to services in Azure
- Create a function by using Visual Studio Code and the Azure Functions Core Tools
# Links
[Develop Azure Functions - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/develop-azure-functions/)
[Develop and run Azure Functions locally | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-local?pivots=programming-language-csharp)
# Module assessment
> [!question] Question 1 Which of the following choices is required for a function to run?
> 
> - Binding
> - Trigger
> - Both triggers and bindings
> 
> > [!success]- Answer 
> > Trigger

> [!question] Question 2 Which of the following choices supports both the `in` and `out` direction settings?
> 
> - Bindings
> - Trigger
> - Connection value
> 
> > [!success]- Answer
> >  Bindings
# Note
- Functions App
	- Collections of functions.
	- Same... 
		- Programming language / runtime.
		- Pricing plan
		- Deployment method
	- Run locally
		- `local.settings.json` instead of Application Settings.
		- Triggers
			- Connect to Azure services
			- Storage based
				- Azurite emulator
- Bindings
	- Trigger == special input binding
		- Requires exactly 1
	- In / out bindings
		- Not required
		- Multiple allowed.
	- `functions.json` or defined through attributes / decoration.
- Auth
	- Connections Strings or
	- Managed Identity

# Flashcards
- What 3 things do Functions that are part of the same Functions app share?
	- Programming language, pricing plan & deployment method.
- In Azure functions, when would you have to use `function.json`?
	- When you using any language besides Java and C#, as they don't support attributes/decorations.
- When developing Azure functions locally, applications settings are defined in what file?
	- `local.settings.json`
# 🛠 Practice Exercises
**Objective:** Deepen your understanding of the Azure Functions development workflow, from local development and debugging to deployment and using different types of bindings.

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