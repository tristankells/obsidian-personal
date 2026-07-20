# Summary
- Describe Azure App Service key components and value.
- Explain how Azure App Service manages authentication and authorization.
- Identify methods to control inbound and outbound traffic to your web app.
- Deploy a containerized app to App Service.
# Links
- https://learn.microsoft.com/en-us/training/modules/introduction-to-azure-app-service
# Module assessment
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
> > To deploy an app to a staging environment and then swap staging and production slots, eliminating downtime
# Notes
- Azure Web App Service
- Auth
	- Authentication
		- Custom
		- Identity Providers
			- Meta, x, google
		- Allow unauthenticated
			- Handler in app code
				- Required for single page app
		- Configurable status code
			- 401 / 403
		- Logs w/ application logs
	- Authorization
		- Delegated to app?
- CI /CD
	- Integrations
		- Devops
		- Github
- App Service Environment
	- Single Customer
	- Isolated
	- Security
- Environments
	- Windows
	- Native Linux
	- Containers
		- Windows 
		- Linux
			- Limitations
				- File Storage Default Slow
				- Not on Shared pricing tier.
- Runtimes
	- Python
	- Ruby
	- .NET Core
	- PHP
	- Node
- Auto scale
- App Service Plan 
	- Defintion
		- OS
		- Region
		- VM
		- \# of VMs
		- Pricing plan
	- Types
		- Shared
			- Shared VMs
			- Plans
				- Free
				- Shared
		- Dedicated
			- Dedicated VMs
			- Plans
				- Basic
				- Standard
				- Premium
		- Isolated (Network Isolation)
			- Dedicated Azure Virtual Network
			- Plans
			- Isolated ``
			- IsolatedV2 
	- Controls
		- Scale out / up
	- New plan?
		- New region
		- Intensive workload
		- Independent scaling
- Deployment
	- Automatic
		- Providers
			- Github
			- Devops
			- Bitbuckets
	- Manual Deployments
		- Azure CLI
		- Git Endpoint
		- Zip deploy
		- FTP/S
	- Side Cars
		- Standalone Containers
		- Uses
			- Observability
			- Networking
	- Deployment Slots
		- Available on >= Standard 
		- Swap prod / qa
- Networking
	- Default internet access enabled
	- Controls
		- Inbound 
			- App-assigned address??
			- Access restrictions??
			- Service endpoints??
			- Private Endpoints??
		- Outbounds
			- Hybrid Connections??
			- Gateway-required virtual network in integration??
			- Virtual network integration??
# Flashcards
Q: List at least three of the environments supported by Azure Web App Service?
A: Windows, Linux, Windows Container, Linux Container. It also support docker compose and multi-container apps.

Q: List at least three of the runtimes supported by Linux on Azure Web App Service?
A: Node, PHP, dotnet, java, python, ruby

Q: On the Shared Azure App Service Plan customers ...
A: Share the same compute resources.

Q: On the Dedicated Azure App Service Plan customers ...
A: Have their own VMs.

Q: On the Isolated Azure App Service Plan customers ...
A: Have their own VMs and Azure Virtual Network.

Q: Who are the three supported providers for automated deployments on Azure Web App Service?
A: Devops, Github and Bitbucket

**Q: Which Azure App Service tiers support deployment slots?**
A: Standard, Premium, and Isolated tiers. The Basic and Free tiers do not support deployment slots.

**Q: Do deployment slots share the same App Service Plan?**
A: Yes. All slots for a web app run on the same App Service Plan and share its resources (CPU, memory).

Q: What is the main benefit of using deployment slots?
A: Zero-downtime deployments. You can warm up changes in a staging slot, then instantly swap it to production without any downtime

Q: What is a sidecar container?
A: A secondary container that runs alongside your main application container in the same pod/group, providing supporting functionality like logging, monitoring, or proxying.

Q: What resources do sidecar containers share with the main container?
A: Network namespace (communicate via localhost), storage volumes, and lifecycle (start/stop together).

Q: Give three common use cases for sidecar containers.
A:
Logging - Collecting and shipping application logs
Service mesh proxies - Handling network communication and security
Configuration management - Syncing config files from external sources

Q: With using provider SDK for authentication, what header will be populated with the token?
A: x-zumo-auth

Q: Name 3 identity providers for use with App Service Plan authentication?
A: Google, Facebook, Apple, Github, x

Q: What name 3 controls you have for inbound traffic to your application in an App Service Plan?
A: App-assigned address, Access restrictions, Service endpoints, Private endpoints	

Q: What name 2 controls you have for outbound traffic to your application in an App Service Plan?
A: Hybrid Connections, Gateway-required virtual network integration, Virtual network integration

Q: Which of the following App Service plan categories provides the maximum scale-out capabilities?
A: Isolated

Q: What determines the set of compute resources for a web app to run in Azure App Service?
A: The App Service Plan
# 🛠 Practice Exercises
**Objective:** Gain practical experience with core features of Azure App Service, including CI/CD, deployment slots, containerization, and security.

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
- [ ] **6. Quickstart Follow-Along:**
    - [ ] Complete the guided quickstart for deploying from a local filesystem to get another perspective on deployment: [Build and deploy to Azure Container Apps](https://learn.microsoft.com/en-us/azure/container-apps/quickstart-code-to-cloud?tabs=bash%2Ccsharp). (Note: This links to Container Apps, which is a related but different service. It's still a valuable exercise).
