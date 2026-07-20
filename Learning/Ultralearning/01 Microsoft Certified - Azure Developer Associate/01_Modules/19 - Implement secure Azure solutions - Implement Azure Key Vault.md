---

tags: [azure, cloud, certification, AZ-204]
created: 2025-12-08
---
# 📝 Summary
**What is this module about?**  
After completing this module, you'll be able to:
- Describe the benefits of using Azure Key Vault
- Explain how to authenticate to Azure Key Vault
- Create and retrieve secrets from Azure Key Vault
---
# 🔗 Links
**Useful resources and official docs:**  
- [Explore Azure Key Vault - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/implement-azure-key-vault/2-key-vault-overview)
---
# ✅ Module Assessment
**Key questions and answers from the module assessment:**  
> [!question] Question 1 Which of the below methods of authenticating to Azure Key Vault is recommended for most scenarios?
> 
> - Service principal and certificate
> - Service principal and secret
> - Managed identities
> 
> > [!success]- Answer 
> > Managed identities

> [!question] Question 2 Azure Key Vault protects data when it's traveling between Azure Key Vault and clients. What protocol does it use for encryption?
> 
> - Secure Sockets Layer
> - Transport Layer Security
> - Presentation Layer
> 
> > [!success]- Answer 
> > Transport Layer Security
---
# 🧠 Flashcards
**Important terms and definitions for quick recall:**  
## Card: Core Problems Azure Key Vault Solves

**Q: What major security and management problems does Azure Key Vault solve for cloud applications?**  
**A:** It centralizes and protects secrets, manages encryption keys, and automates SSL/TLS certificate lifecycle tasks.

**Context:** Key Vault addresses secrets management, key management, and certificate management—removing the need to embed secrets in code or operate in-house HSM infrastructure.

---

## Card: Key Benefits of Using Azure Key Vault

**Q: What are the primary benefits of using Azure Key Vault for enterprise applications?**  
**A:**

1. Centralized secret storage
    
2. Secure access via Entra ID + RBAC or access policies
    
3. Full logging and monitoring options
    
4. Simplified administration and automated certificate lifecycle
    
5. High availability via regional and cross-region replication
    

**Context:** Key Vault improves security posture, simplifies secret lifecycle management, and reduces operational overhead by using Azure’s managed capabilities.

---
## Card 1: Recommended Key Vault Authentication Method

**Q: According to Azure Key Vault best practices, what is the recommended authentication method and why is it preferred over service principals?**

**A:** Managed identities for Azure resources - because Azure automatically rotates the service principal client secret, eliminating the need for manual secret rotation.

**Context:** Three authentication options exist (managed identities, service principal + certificate, service principal + secret), but managed identities are the best practice since they solve the secret rotation problem automatically.

---

## Card 2: Key Vault Organization Pattern

**Q: What is Azure's recommended organizational pattern for Key Vaults across different application environments?**

**A:** One vault per application per environment (separate vaults for Development, Pre-Production, and Production).

**Context:** This pattern prevents secrets from being shared across environments and limits breach impact. Example: MyApp would have three vaults: MyApp-Dev, MyApp-PreProd, MyApp-Prod.

## Card 1: Key Vault Security Principal Types

**Q: In Microsoft Entra ID authentication for Azure Key Vault, what are the three types of security principals that can request access to Azure resources?**

**A:** Users (real people with accounts), Groups (collections of users with shared permissions), and Service Principals (represent apps or services, not people).

**Context:** Security principals are authenticated by Microsoft Entra ID before accessing Key Vault. Think of service principals as "user accounts for applications."

---

## Card 2: Managed Identity Recommendation

**Q: When obtaining a service principal for Key Vault application authentication, what specific type of managed identity does Azure recommend?**

**A:** System-assigned managed identity.

**Context:** Managed identities are preferred over manual app registration because Azure creates and manages the service principal automatically, allowing apps to securely access Azure services without storing credentials. Works with App Service, Azure Functions, and Virtual Machines.

---
# 🛠 Practice Exercises
**Objective:** Learn how to securely store and access application secrets using Azure Key Vault.

- [ ] **1. Basic Secret Management:**
    - [ ] Follow the official Microsoft Learn exercise to get comfortable with the basics: [Create and retrieve secrets from Azure Key Vault](https://learn.microsoft.com/en-us/training/modules/implement-azure-key-vault/5-set-retrieve-secret-azure-key-vault). This will cover:
        - Creating a Key Vault.
        - Adding a secret using the Azure portal.
        - Retrieving that secret in an application using the Azure SDK.
- [ ] **2. Integrate Key Vault with an Azure App Service:**
    - [ ] **Goal:** Access a Key Vault secret from a web application without any credentials in the code, using a managed identity.
    - [ ] Create an Azure App Service instance.
    - [ ] Enable the system-assigned managed identity for the App Service.
    - [ ] In your Key Vault, create an access policy that grants the App Service's managed identity "Get" and "List" permissions for secrets.
    - [ ] Create a secret in your Key Vault (e.g., a database connection string).
    - [ ] In the App Service's configuration, create an application setting that uses a Key Vault reference to point to your secret (e.g., `@Microsoft.KeyVault(SecretUri=...)`).
    - [ ] Deploy a simple web app that reads this application setting and displays its value, proving it can access the secret.
- [ ] **3. Secret Rotation and Versioning:**
    - [ ] **Goal:** Practice updating a secret and see how versioning works.
    - [ ] In your Key Vault, create a new version of the secret you created earlier with a different value.
    - [ ] Notice that your App Service is still using the old version of the secret because its reference points to a specific version.
    - [ ] Update the Key Vault reference in the App Service to point to the new version of the secret (or remove the version from the URI to always get the latest).
    - [ ] Restart the App Service and confirm that it now retrieves the updated secret value.
---
# 📚 Additional Notes
**Any extra insights, tips, or gotchas:** 