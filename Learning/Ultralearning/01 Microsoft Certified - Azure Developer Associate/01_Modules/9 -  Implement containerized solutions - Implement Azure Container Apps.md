# Summary
- By the end of this module, you will be able to ...caca
	- Describe the benefits of Azure Container Instances and how resources are grouped.
	- Deploy a container instance in Azure by using the Azure CLI
	- Start and stop containers using policies.
	- Set environment variables in your container instances.
	- Mount files share to a container instance.
# Links
- [Implement Azure Container Apps - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/implement-azure-container-apps/)
# Module assessment
> [!question] Question 1 Which of the following options is true about the built-in authentication feature in Azure Container Apps?
> 
> - It can only be configured to restrict access to authenticated users.
> - It allows for out-of-the-box authentication with federated identity providers.
> - It requires the use of a specific language or SDK.
> 
> > [!success]- Answer 
> > It allows for out-of-the-box authentication with federated identity providers.

> [!question] Question 2 What is a revision in Azure Container Apps?
> 
> - A dynamic snapshot of a container app version.
> - A version of a container app that is actively being used.
> - An immutable snapshot of a container app version.
> 
> > [!success]- Answer 
> > An immutable snapshot of a container app version.
# Notes
- Azure Container Service Apps
	- Build on Azure Kubernetes Service
- Benefits
	- Mount file share
	- Support split traffic / blue green deployments.
	- Use existing registries
	- Managed https enabled ingress
	- Service Discovery
	- Dapr support
		- Unified API for microservice architecture.
		- BIG TOPIC
	- Azure Log Analytics
	- Keda based scale trigger
		- CPU and Memory
		- ++ external events
	- Independent scaling, versioning and upgrades.
	- Auth
		- In built
			- Sidecar container
		- Federated Identity
			- Google
			- X
			- Microsoft
			- etc...
- Limitations
	- No root access
	- Only linux
- Azure Container Apps Environment
	- Environment for groups of Containers Apps.
	- Shared compute resources
	- Same virtual network
- Configuration
	- ARM
	- Multicontainer Container Apps
		- Side Car
	- Container Registry
		- Public
		- Private
	- Revisions
		- Automatic on revision scope changes
		- != application scope changes
			- Includes secrets
	- Secrets
		- Inject via CLI
		- Reference in environment variables
			- `secretref:SECRETNAME`
		- No azure key vault integrations


# Flashcards
-  Besides from memory and cpu, name two other scale triggers available in Azure Container Apps
	- HTTP traffic,
	- KEDA Scalers
	- Event-driven processsing.
- In Azure Container Apps, the top level is ..., which can contain multiple ..., which might container multiple ... which each contain a ... which defines the actually number of running ....
	- Azure Container App Environment -> Azure Container App -> Revision -> Replica -> Container
- To use a private registry Azure Container Apps, you must define what three fields in a ARM template.
	- server, username, passwordSecretRef
- If for some reason you need HTTP traffic on you app running in Azure Container Apps, what do you need to do?
	- Enable `allowInsecure` on the ingress configuration. 
- Name the two parameters and their values, if you wanted to pass a secure password to the `password` environment variables of an Azure Container App created via `az containerapp create`. 
	- `-- secrets "password=$SECUREPASSWORD"`
	- `--env-vars "password=secretref:password"`
# 🛠 Practice Exercises
**Objective:** Learn to deploy, manage, and scale applications using Azure Container Apps, and explore its advanced features like Dapr, multi-container apps, and revisions.

- [ ] **1. Basic Deployment:**
    - [ ] Follow the official Microsoft Learn exercise to deploy your first container app: [Deploy a container to Azure Container Apps with the Azure CLI](https://learn.microsoft.com/en-us/training/modules/implement-azure-container-apps/3-exercise-deploy-app).
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