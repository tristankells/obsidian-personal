## [[15 - Implement user authentication and authorization Explore the Microsoft identity platform]]

### Custom Practical Exercises

- [ ] **1. Secure the "Envelopes" API:**
    - [ ] **Goal:** Implement single-tenant authentication for your "Envelopes" API.
    - [ ] Register your application in Microsoft Entra ID.
    - [ ] Configure your API to require authentication using the Microsoft identity platform.
    - [ ] Test that unauthenticated requests are rejected and that authenticated requests are allowed.

## [[16 - Implement user authentication and authorization  -Implement authentication by using the Microsoft Authentication Library]]

### Azure Training Practical Exercises

- [ ] **1. Follow the Guided Exercise:**
    - [ ] **Goal:** Learn the fundamentals of MSAL.NET.
    - [ ] Complete the official Microsoft Learn exercise: [Implement interactive authentication with MSAL.NET](https://learn.microsoft.com/en-us/training/modules/implement-authentication-by-using-microsoft-authentication-library/4-interactive-authentication-msal).

### Custom Practical Exercises

- [ ] **2. Token Caching and Silent Acquisition:**
    - [ ] **Goal:** Improve the user experience by silently acquiring tokens from the cache.
    - [ ] After a successful interactive login, ensure the token is cached.
    - [ ] On subsequent application starts, use `AcquireTokenSilent` to get a token without prompting the user.
    - [ ] Implement a `try/catch` block to fall back to `AcquireTokenInteractive` if silent acquisition fails.
- [ ] **3. Explore Different Authentication Flows (Conceptual):**
    - [ ] **Goal:** Understand other common authentication flows.
    - [ ] **Device Code Flow:** Research how the device code flow works and when it's used (e.g., CLI apps).
    - [ ] **Integrated Windows Authentication (IWA):** If you are on a domain-joined machine, research how IWA provides a seamless sign-in experience.

## [[17 - Implement user authentication and authorization - Implement shared access signatures]]

### Custom Practical Exercises

- [ ] **1. Generate a Service SAS:**
    - [ ] **Goal:** Create a SAS token for temporary, limited access to a blob.
    - [ ] Create a storage account and upload a file to a blob container.
    - [ ] Generate a Service SAS for the blob with "Read" permissions and a 1-hour expiry.
    - [ ] Verify you can access the blob with the SAS URL, but cannot perform other operations.
- [ ] **2. Generate a User Delegation SAS:**
    - [ ] **Goal:** Create a more secure SAS token using Microsoft Entra ID credentials.
    - [ ] Assign your user the "Storage Blob Data Contributor" role on the storage account.
    - [ ] Use Azure CLI to get a user delegation key.
    - [ ] Create a user delegation SAS for a container with "Write" and "List" permissions.
    - [ ] Use `azcopy` with the SAS to upload a file, verifying the permissions.
- [ ] **3. Implement and Use a Stored Access Policy:**
    - [ ] **Goal:** Centrally manage and revoke access for SAS tokens.
    - [ ] Define a stored access policy on a blob container named `read-policy` with read access for 24 hours.
    - [ ] Generate a Service SAS linked to this policy.
    - [ ] Verify the SAS works.
    - [ ] Revoke the SAS by deleting or modifying the stored access policy and verify that access is now denied.

## [[18 - Implement user authentication and authorization -Explore Microsoft Graph]]

### Azure Training Practical Exercises

- [ ] **1. Set up a .NET Application for Microsoft Graph:**
    - [ ] **Goal:** Learn how to authenticate and retrieve basic user data with the Microsoft Graph SDK.
    - [ ] Follow the official Microsoft Learn exercise: [Retrieve user profile information with the Microsoft Graph SDK](https://learn.microsoft.com/en-us/training/modules/microsoft-graph/5a-exercise-microsoft-graph-user-profile).

### Custom Practical Exercises

- [ ] **2. Extend the Application:**
    - [ ] **Goal:** Retrieve more detailed information using the Graph SDK.
    - [ ] **List User's Files:** Modify the application to list the first 10 files in the user's OneDrive for Business root directory.
    - [ ] **Read User's Calendar:** Add functionality to display the user's upcoming appointments for the next 7 days.
    - [ ] **Send an Email:** Implement a feature to send an email from the signed-in user's account to themselves.

## [[19 - Implement secure Azure solutions - Implement Azure Key Vault]]

### Azure Training Practical Exercises

- [ ] **1. Basic Secret Management:**
    - [ ] **Goal:** Learn the fundamentals of creating and retrieving secrets from Key Vault.
    - [ ] Follow the official Microsoft Learn exercise: [Create and retrieve secrets from Azure Key Vault](https://learn.microsoft.com/en-us/training/modules/implement-azure-key-vault/5-set-retrieve-secret-azure-key-vault).

### Custom Practical Exercises

- [ ] **2. Integrate Key Vault with an Azure App Service:**
    - [ ] **Goal:** Access a Key Vault secret from a web app without credentials in code, using a managed identity.
    - [ ] Enable the system-assigned managed identity for an App Service.
    - [ ] Grant the managed identity "Get" and "List" permissions for secrets in your Key Vault.
    - [ ] Create a secret in Key Vault (e.g., a database connection string).
    - [ ] In the App Service configuration, reference the secret using the `@Microsoft.KeyVault(SecretUri=...)` syntax.
    - [ ] Deploy a web app that reads the secret from its configuration and displays it.
- [ ] **3. Secret Rotation and Versioning:**
    - [ ] **Goal:** Practice updating a secret and managing its version.
    - [ ] Create a new version of an existing secret in Key Vault.
    - [ ] Update the Key Vault reference in your App Service to point to the new version (or to always get the latest version).
    - [ ] Restart the App Service and confirm it retrieves the updated secret.

## [[20 - Implement secure Azure solutions - Implement managed identities]]

### Custom Practical Exercises

- [ ] **1. System-Assigned Managed Identity:**
    - [ ] **Goal:** Use a system-assigned identity for a VM to access a Storage Account.
    - [ ] Create a VM and enable its system-assigned managed identity.
    - [ ] Assign the "Storage Blob Data Reader" role to the VM's identity on a Storage Account.
    - [ ] From the VM, use the Azure CLI with its managed identity to list blobs, proving access without stored credentials.
- [ ] **2. User-Assigned Managed Identity:**
    - [ ] **Goal:** Share a single user-assigned identity across multiple resources.
    - [ ] Create a user-assigned managed identity.
    - [ ] Assign this identity to two different Azure App Services.
    - [ ] Grant the identity the "Key Vault Secrets User" role on a Key Vault.
    - [ ] From both App Services, authenticate using the user-assigned identity and retrieve a secret from the Key Vault.

## [[21 - Implement secure Azure solutions - Implement Azure App Configuration]]

### Azure Training Practical Exercises

- [ ] **1. Retrieve Configuration Settings:**
    - [ ] **Goal:** Learn how to use Azure App Configuration to manage and retrieve application settings.
    - [ ] Follow the official Microsoft Learn exercise: [Retrieve configuration settings from Azure App Configuration](https://learn.microsoft.com/en-us/training/modules/implement-azure-app-configuration/5a-retrieve-configuration-settings).