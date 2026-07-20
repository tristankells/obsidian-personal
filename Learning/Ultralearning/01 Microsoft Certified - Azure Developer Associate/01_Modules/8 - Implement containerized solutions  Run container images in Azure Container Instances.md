# Summary
After  this module, you'll be able to:
- Describe the benefits of Azure Container Instances
- Deploy a container instance in Azure by using the Azure CLI
- Start and stop containers using policies
- Set environment variables in your container instances
- Mount file shares in your container instances
# Links
- [Introduction - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/create-run-container-images-azure-container-instances/1-introduction)
# Module assessment
> [!question] Question 1 Which of the following methods is recommended when deploying a multi-container group that includes only containers?
> 
> - Azure Resource Management template
>     
> - YAML file
>     
> - az container create command
>     
> 
> > [!success]- Answer  
> > YAML file

---

> [!question] Question 2 What is the purpose of a restart policy in Azure Container Instances?
> 
> - To charge customers more for compute resources used while the container is running.
>     
> - To ensure that containers are never restarted, even if the process fails.
>     
> - To specify when and how containers should be restarted, based on the desired behavior.
>     
> 
> > [!success]- Answer  
> > To specify when and how containers should be restarted, based on the desired behavior.

---

> [!question] Question 3 If you want to mount multiple volumes, what options are at your disposal for deployment?
> 
> - YAML file only
>     
> - Azure Resource Manager template and YAML file
>     
> - Azure Resource Manager template and PowerShell
>     
> 
> > [!success]- Answer  
> > Azure Resource Manager template and YAML file
# Notes
- Benefits
	- Run on the same host
	- Multi container support
	- Public container access
	- Mount storage
	- Fast startup
	- Linux and Windows
- Container Groups
	- Collections of container
		- Share...
			- lifecycle, 
			- resources 
			- local network 
			- IP Address
			- storage volumes.
		- = k8 pod
	- Single or multi-container...
		- Using Azure Resource Manager (ARM) templates
			- Recommend with additional Azure services.
		- Or YAML
			- Best for only containers.
		- Only on Linux
- Restart Policies
	- Specified through CLI.
	- Always
		- Default
		- For running services 
	- Never
		- For one time containers
	- OnFailure
		- Retry mechanism for one time
- Environment Variables
	- Pass in via CLI
		- `--environment-variables`
	- SecureValues
		- Pass values via secret file.
- Volume storage
	- To mount multiple volume needs ARM or YAML
	- Azure File Share only on linux.
	- Mount to group

# Flashcards
- Azure Container Instances support the following 4 volume mounts...
	- Azure file share, 
	- Secret
	- Empty directory
	- Cloned git repo.
- Containers part of the same Azure Container Instances Container Group share...
	- Lifecycle
	- Resources (Memory and CPU)
	- Storage Volumes
	- Local Network
- What are the two recommended ways to deploy multi-container group in Azure Container Instances
	- Resource Manager template
	- YAML file
- What are the restart policies in Azure Container Instances? Which is the default?
	- Always (Default), Never, OnFailure
- What is the command line argument for passing environment variables to Azure Container Instances?
	- `--environment-variables`
- If you want to mount multiple volumes to a container group, what two deployments methods can you use?
	- Resource Manager template OR YAML file.
# 🛠 Practice Exercises
**Objective:** Understand and use Azure Container Instances (ACI) to run single and multi-container applications, manage their configuration, and persist data.

- [ ] **1. Cost and Tier Analysis:**
    - [ ] Research the pricing model for Azure Container Instances. Is it purely consumption-based?
    - [ ] Determine if there's a free tier or a certain amount of free usage per month.
- [ ] **2. Single Container Deployment with Azure CLI:**
    - [ ] Follow the official Microsoft Learn exercise to get a baseline understanding: [Deploy a container to Azure Container Instances](https://learn.microsoft.com/en-us/training/modules/create-run-container-images-azure-container-instances/3-run-azure-container-instances-cloud-shell).
    - [ ] Manually deploy a simple public container image (e.g., `mcr.microsoft.com/azuredocs/aci-helloworld`) using the `az container create` command.
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