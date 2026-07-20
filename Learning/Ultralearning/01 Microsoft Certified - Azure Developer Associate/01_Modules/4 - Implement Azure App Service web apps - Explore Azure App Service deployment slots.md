# Summary
- By the end of this module you will know...
	- The benefits of deployments slots.
	- How slot swapping works.
	- How to enable autoswap / perform a manually swap.
	- To route traffic manually and automatically

# Links
- [Explore Azure App Service Deployment Slots - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/understand-app-service-deployment-slots/)
- [GitHub - Azure-Samples/html-docs-hello-world: A simple HTML site for docs](https://github.com/Azure-Samples/html-docs-hello-world)
# Module assessment
> [!question] Question 1 By default, all client requests to the app's production URL (`http://<app_name>.azurewebsites.net`) are routed to the production slot. One can automatically route a portion of the traffic to another slot. What is the default routing rule applied to new deployment slots?
> 
> - 0%
> - 10%
> - 20%
> 
> > [!success]- Answer
> >  0%

> [!question] Question 2 Some configuration elements follow the content across a swap (not slot specific), whereas other configuration elements stay in the same slot after a swap (slot specific). Which of the following settings are swapped?
> 
> - Publishing endpoints
> - WebJobs content
> - WebJobs schedulers
> 
> > [!success]- Answer 
> > WebJobs content
# Notes
- Only Standard tier +
	- No cost, slots per plan
- Benefits
	- Staging environment
	- Pre-warming
	- Rollback
- Settings
	- Clone from existing
	- Independent repo
	- Warmup settings
		- WEBSITE_SWAP_WARMUP_PING_PATH
			- Warm up path after swap; `/ping`
		- WEBSITE_SWAP_WARMUP_PING_STATUSES
			- Valid HTTP responses; `200,202`
		- WEBSITE_WARMUP_PATH
			- Warm up path after restart; `/health`
	- Swapped Settings
		- Include
			- General settings
			- App setting...
		- Exclude
			- Private certificates
			- Publishing endpoints
- Process
	- Manual Swap
	- Auto-Swap
		- Windows only?
		- Push to code, automatic swap
	- Steps
		- 1. Apply target slot setting (swappable) setting to source slot.
			- swap w/ preview == stop for review
		- 2. Wait for source restarts
		- 3. HTTP call to `/` -> trigger cache.
		- 4. Custom warmup HTTP call.
			- Add custom endpoint to `applicationInitialization` 
		- 5. Swap routing rules, source becomes target.
		- Target slot always on

# Flashcards
- Name 3 examples of slot specific settings for Azure App Service deployment slots that are swapped to the new slot?
	- App settings, General settings, Connection strings, Handler mappings, Public certificates, WebJobs content, Hybrid connections, Azure Content Delivery Network, Service endpoints, Path mappings
- Name 3 examples of slot settings for Azure App Service deployment slots that are not swappable?
	- Publishing endpoints, Custom domain names, Nonpublic certificates and TLS/SSL settings, Scale settings, WebJobs schedulers, IP restrictions, Always On, Diagnostic log settings, Cross-origin resource sharing (CORS), Virtual network integration, Managed identities, Settings that end with the suffix `_EXTENSION_VERSION`
- What is the header cookie that indicates the deployment slot a client has been assigned to in Azure App Service?
	- ``x-ms-routing-name
# 🛠 Practice Exercises
**Objective:** Master the use of deployment slots in Azure App Service to implement blue-green deployments, A/B testing, and zero-downtime updates.
**Note:** Deployment slots are only available on Standard tier or higher, so this may incur costs.

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