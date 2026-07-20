---

tags: [azure, cloud, certification, AZ-204]
created: 2025-12-08
---
# 📝 Summary
**What is this module about?**  
After completing this module, you'll be able to:
- Explain the differences between the two types of managed identities
- Describe the flows for user- and system-assigned managed identities
- Configure managed identities
- Acquire access tokens by using REST and code
---
# 🔗 Links
**Useful resources and official docs:**  
- [Introduction - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/implement-managed-identities/1-introduction)
---
# ✅ Module Assessment
**Key questions and answers from the module assessment:**  
> [!question] Question 1 Which of the following managed identity characteristics is indicative of user-assigned identities?
> 
> - Shared lifecycle with an Azure resource
> - Independent life-cycle
> - Can only be associated with a single Azure resource
> 
> > [!success]- Answer 
> > Independent life-cycle

> [!question] Question 2 A client app requests managed identities for an access token for a given resource. Which of the following options is the basis for the token?
> 
> - Oauth 2.0
> - Service principal
> - Virtual machine
> 
> > [!success]- Answer 
> > Service principal
---
# 🧠 Flashcards
**Important terms and definitions for quick recall:**  
## Card 1: System-Assigned vs User-Assigned Identity Lifecycle

**Q: What is the key difference between system-assigned and user-assigned managed identities regarding their lifecycle and deletion?**

**A:** System-assigned identities share the lifecycle with their Azure resource (deleted when resource is deleted), while user-assigned identities have an independent lifecycle and must be explicitly deleted.

**Context:** This is the most fundamental operational difference. Example: Deleting a VM with a system-assigned identity automatically deletes the identity, but deleting a VM with a user-assigned identity leaves that identity intact for use by other resources.

---

## Card 2: User-Assigned Managed Identity Use Case

**Q: According to Azure best practices, when should you use a user-assigned managed identity instead of a system-assigned one?**

**A:** When multiple resources need to share a single identity, or when permissions should stay consistent across resources that are recycled frequently.

**Context:** Example: Multiple VMs that need to access the same resource, or workloads requiring preauthorization to a secure resource as part of provisioning. User-assigned identities can be associated with more than one Azure resource.

---

## Card 3: Managed Identity Purpose

**Q: What problem do managed identities solve for developers accessing Azure services that support Microsoft Entra authentication?**

**A:** They eliminate the need to manage credentials (secrets, certificates, and keys) by providing an automatically managed identity that applications use to obtain Microsoft Entra tokens.

**Context:** Before managed identities, developers had to securely store credentials in Azure Key Vault and manage their rotation. Managed identities remove this burden entirely while maintaining secure authentication.

---
**Q: What is the endpoint URL that code running on an Azure VM uses to request an access token from a managed identity, and what is the key access restriction?**

**A:** `http://169.254.169.254/metadata/identity/oauth2/token` - accessible only from within the virtual machine.

**Context:** This endpoint is used by both system-assigned and user-assigned managed identities (step 5 in both flows). The VM's code requests a token here, which triggers Microsoft Entra ID to return a JWT access token that can be used to authenticate to Azure services.

---
## Card 1: System-Assigned Identity Azure CLI Command

**Q: What Azure CLI parameter enables a system-assigned managed identity when creating a new VM with `az vm create`?**

**A:** `--assign-identity` (optionally with `--role` and `--scope` to specify permissions).

**Context:** Example: `az vm create --resource-group myResourceGroup --name myVM --assign-identity --role contributor --scope mySubscription`. For existing VMs, use `az vm identity assign` command instead.

---

## Card 2: User-Assigned Identity Two-Step Process

**Q: What are the two required steps to enable a user-assigned managed identity on an Azure VM, and which Azure CLI commands accomplish them?**

**A:** (1) Create the identity using `az identity create`, then (2) Assign it to the VM using `az vm create --assign-identity <IDENTITY_NAME>` or `az vm identity assign --identities <IDENTITY_NAME>`.

**Context:** Unlike system-assigned identities (which are created automatically when enabled), user-assigned identities must be created as standalone resources first. Requires Virtual Machine Contributor and Managed Identity Operator role assignments.

## Card 1: DefaultAzureCredential Authentication Order

**Q: What are the first three authentication mechanisms that DefaultAzureCredential attempts, in order, before moving to other methods?**

**A:** (1) Environment variables, (2) Managed Identity (if deployed to Azure host with it enabled), (3) Visual Studio (if developer authenticated via VS).

**Context:** DefaultAzureCredential attempts multiple mechanisms in sequence, stopping when one succeeds. After these three, it tries Azure CLI, Azure PowerShell, and optionally interactive browser. This allows the same code to work in both development and production environments without changes.

---

## Card 2: User-Assigned Identity with DefaultAzureCredential

**Q: In Azure Identity SDK, how do you configure DefaultAzureCredential to authenticate with a specific user-assigned managed identity instead of a system-assigned one?**

**A:** Pass `DefaultAzureCredentialOptions` with the `ManagedIdentityClientId` property set to the user-assigned identity's client ID.

**Context:** Example: `new DefaultAzureCredential(new DefaultAzureCredentialOptions { ManagedIdentityClientId = userAssignedClientId })`. Without this configuration, DefaultAzureCredential uses system-assigned managed identity when deployed to Azure.


---
# 🛠 Practice Exercises
**Objective:** Understand the difference between system-assigned and user-assigned managed identities and learn how to create and use them to securely access Azure resources.

- [ ] **1. System-Assigned Managed Identity:**
    - [ ] **Goal:** Create an Azure VM and enable a system-assigned identity to allow it to access a Storage Account.
    - [ ] Create an Azure Storage Account.
    - [ ] Create an Azure Virtual Machine (VM).
    - [ ] Enable the system-assigned managed identity on the VM.
    - [ ] Assign the "Storage Blob Data Reader" role to the VM's identity on the Storage Account.
    - [ ] Connect to the VM and use the Azure CLI or PowerShell with its managed identity to list blobs in the storage account, proving it has access without any stored credentials.
- [ ] **2. User-Assigned Managed Identity:**
    - [ ] **Goal:** Create a single user-assigned identity and share it across multiple Azure resources.
    - [ ] Create a user-assigned managed identity resource using `az identity create`.
    - [ ] Create two Azure App Service instances (or VMs).
    - [ ] Assign the *same* user-assigned identity to both App Service instances.
    - [ ] Grant this identity access to an Azure Key Vault (e.g., the "Key Vault Secrets User" role).
    - [ ] From both App Service instances (using their web-based console or by deploying a simple app), write code to authenticate using the user-assigned identity and retrieve a secret from the Key Vault. This demonstrates a shared, reusable identity. 

---
# 📚 Additional Notes
**Any extra insights, tips, or gotchas:** 