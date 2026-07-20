# Summary
- After this module, you'll be able to:
	- Explain the features and benefits of Azure Container Registry.
	- Use ACR Tasks to automate builds and deployments.
	- Explain the elements in a Dockerfile.
	- Build and run an image in the ACR by using Azure CLI.
# Links
[Manage Container Images in Azure Container Registry - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/publish-container-image-to-azure-container-registry/)
# Module assessment
> [!question] Question 1 Which of the following Azure Container Registry options support geo-replication to manage a single registry across multiple regions?
> 
> - Basic
>     
> - Standard
>     
> - Premium
>     
> 
> > [!success]- Answer  
> > Premium

---

> [!question] Question 2 Which Azure container registry tiers benefit from encryption-at-rest?
> 
> - Basic, Standard, and Premium
>     
> - Basic and Standard only
>     
> - Premium only
>     
> 
> > [!success]- Answer  
> > Basic, Standard, and Premium
# Notes
- Azure Container Registry
	- Use Cases
		- Scalable orchestration systems
			- Docker swarm
			- k8
			- DC/OS
				- Data Center Operating System
		- Azure Services
			- Azure Kubernetes Service
			- Azure App Service
			- Batch
				- Batch job service
			- Service Fabric
				- Microsoft's [container orchestrator](https://learn.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-resource-manager-introduction)
	- Store images artifacts
	- Use in build / deployment pipelines
	- Benefits
		- Automatable build process with triggers.
	- Supports docker images
		- Windows 
		- Linux
	- - Pricing Plans
	- Basic
		- Same features as higher plans
		- Lowest storage / throughput
		- All plans include encryption-at-rest
	- Standard 
		- Increased throughput and storage.
	- Premium
		- Geo-replication / Zone redundancy
		- Secure Signing
		- Private Endpoints
- Azure Container Registry Tasks
	- Default: Linux
	- Types 
		- Quick Task
			- Offload dev build to Azure.
			- `docker build; docker push`
			- On demand.
		- Trigger
			- On change
				- Source code change
				- Base image change
			- On schedule 
		- Multi-Step Task
			- yaml definition
			- Example
				- Image build -> Image Deploy -> Test Image Build -> Test Image Deploy -> On success helm update...
- - Dockerfile
	- List of instructions to include in image.
		- `FROM` the base image to build yours from 
		- `WORKDIR` change the working directory.
		- `COPY` copy files from one location to working directory.
		- `EXPOSE` the private port for the host to call. Not accessible outside the host.
		- `CMD` the file command to run once to start the container.
	- Docker image
		- Sharable unit of software, that includes all of the it's dependencies. 
	- Docker container
# Flashcards
- What 3 additional feature are include in the premium plan for Azure Container Registry?
	- Geo-replication, content trust for image tag signing and private endpoints to restrict access to the registry
- What are three available triggers for for Azure Container Registry tasks?
	- Source Code, Base Image and Schedule
- Name 4 other Azure Service that can pull images from Azure Container Registry directly?
	- App Service, Azure Kubernetes Service, Batch and Service Fabric.
- What does the `FROM` command do in a dockerfile?
	- Specifies the base image to build from. Should be the beginning of every dockerfile.
- Name the three types of Azure Container Registry Tasks?
	- Quick Task, Trigger Task and Multi Step Tasks.
# 🛠 Practice Exercises
**Objective:** Gain hands-on experience with Azure Container Registry (ACR) by creating a registry, building and pushing a Docker image, and exploring ACR Tasks for automation.

- [ ] **1. Cost Analysis:**
    - [ ] Investigate the pricing tiers for Azure Container Registry (Basic, Standard, Premium).
    - [ ] Determine if there is a free tier or a free amount of storage/builds included.
- [ ] **2. Follow the Microsoft Learn Exercise (if cost-effective):**
    - [ ] Complete the guided exercise: [Build and run a container image with Azure Container Registry Tasks](https://learn.microsoft.com/en-us/training/modules/publish-container-image-to-azure-container-registry/6-build-run-image-azure-container-registry). This will cover the fundamental steps.
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