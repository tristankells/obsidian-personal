# Summary
- Know how to... 
	- Create application setting that are bound to deployment slots.
	-  Install SSL certificates for your app.
	- Enable diagnostics logging.
	- Create virtual directory-to-app mapping 
# Links
# Module assessment
> [!question] Question 1
> In which of the following app configuration settings categories would you set the stack and SDK version?
> - Application settings
> - Path mappings
> - General settings
> 
> > [!success]- Answer
> > General settings

> [!question] Question 2
> Which of the following types of application logging is supported on the Linux platform?
> - Web server logging
> - Failed request tracing
> - Deployment logging
> 
> > [!success]- Answer
> > Deployment logging
# Notes
- Application Settings
	- JSON Format
	- == Environment Variables
	- Uses
		- Override appsettings.json
			- Connection strings
	- Update == restart app
- General Settings
	- Host settings
		- Always on
		- Stack (Node, Java, .NET)
			- Version
	- Remote debugging
- Configuration path mappings
	- run app from custom paths
- Diagnostic logging
	- Types
		- Applications logs
		- Webserver logs / HTTP request data
		- Detail error messages
		- Failed request tracing
		- Deployment logging
	- Require storage
		- Blob
		- File system
		- File share
- Security certificates
	- Managed by Azure
	- Or privately managed
# Flashcards
Q: Azure Web App Applications Settings are used for setting what for your service?
A: Environment variables. 

Q: What are a couple settings you can set in General Setting for Azure Web App?
A: Stack, stack version, Always On, TLS version, Platform bitness, web sockets, HTTPS only, minimum TLS...

Q: Which 2 types of diagnostic logging is available on Linux?
A: Application logging & Deployment logging.

# 🛠 Practice Exercises
**Objective:** Learn how to configure and manage various settings for an Azure App Service, including application settings, general settings, and logging.

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