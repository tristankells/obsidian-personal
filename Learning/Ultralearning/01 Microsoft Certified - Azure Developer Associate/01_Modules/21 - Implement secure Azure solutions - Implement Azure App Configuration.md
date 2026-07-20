---

tags: [azure, cloud, certification, AZ-204]
created: 2025-12-08
---
# 📝 Summary
**What is this module about?**  
After completing this module, you'll be able to:
- Explain the benefits of using Azure App Configuration
- Describe how Azure App Configuration stores information
- Implement feature management
- Securely access your app configuration information
- Retrieve configuration settings from Azure App Configuration

---
# 🔗 Links
**Useful resources and official docs:**  
- [Explore the Azure App Configuration service - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/implement-azure-app-configuration/2-app-configuration-overview)
---
# ✅ Module Assessment
**Key questions and answers from the module assessment:**  
> [!question] Question 1 What is the purpose of labels in Azure App Configuration?
> 
> - Labels are used to differentiate key-values with the same key in App Configuration.
> - Labels are used to encrypt key-values in App Configuration.
> - Labels are used to limit the size of key-values in App Configuration.
> 
> > [!success]- Answer 
> > Labels are used to differentiate key-values with the same key in App Configuration.

> [!question] Question 2 What is the role of a feature manager in managing application features?
> 
> - A feature manager is a rule for evaluating the state of a feature flag.
> - A feature manager is a variable with a binary state of on or off.
> - A feature manager is an application package that handles the lifecycle of all the feature flags in an application.
> 
> > [!success]- Answer 
> > A feature manager is an application package that handles the lifecycle of all the feature flags in an application.

> [!question] Question 3 What is the purpose of using customer-managed keys in Azure App Configuration?
> 
> - To enable authentication with Microsoft Entra ID
> - To permanently store the unwrapped encryption key
> - To encrypt sensitive information at rest
> 
> > [!success]- Answer 
> > To encrypt sensitive information at rest
---
# 🧠 Flashcards
**Important terms and definitions for quick recall:**
**Q: How does Azure App Configuration complement Azure Key Vault, and what is the key distinction in what each service stores?**

**A:** App Configuration stores **application settings** and feature flags (configuration data), while Key Vault stores application secrets. App Configuration complements Key Vault rather than replacing it.

**Context:** They work together: use Key Vault for sensitive secrets (API keys, passwords, certificates) and App Configuration for non-secret settings (connection strings, feature flags, hierarchical configuration). App Configuration can even reference Key Vault secrets, combining both services.

## Card 1: App Configuration Label Purpose

**Q: In Azure App Configuration, what is the purpose of labels and what is a common use case for them?**

**A:** Labels differentiate key-values with the same key name. Common use: specify multiple environments for the same key (e.g., AppName:DbEndpoint with labels Test, Staging, Production creates three separate configurations).

**Context:** Without a label, reference using `\0` (URL encoded as %00). Labels can also be used for versioning by storing application version numbers or Git commit IDs, since App Configuration doesn't auto-version key values.

---

## Card 2: App Configuration Key Naming Constraints

**Q: What are the three reserved characters that cannot be used in Azure App Configuration key names without escaping, and what is the combined size limit for a key-value pair?**

**A:** Reserved characters: `*`, `,`, and `\` (must escape as `\{Reserved Character}`). Combined size limit: 10,000 characters for the entire key-value pair including key, value, and attributes.

**Context:** Keys are case-sensitive unicode strings (app1 ≠ App1). Hierarchical naming with delimiters like `/` or `:` is recommended for readability and management (e.g., AppName:Service1:ApiEndpoint).

---
## Card 1: Feature Flag Filter Evaluation Logic

**Q: When a feature flag in Azure App Configuration has multiple filters, how does the system determine if the feature should be enabled?**

**A:** The filter list is traversed in order until one filter determines the feature should be enabled - then the flag turns on and remaining filters are skipped. If no filter enables it, the flag is off.

**Context:** Filters represent rules like user groups, device types, geographic locations, or time windows. Example: FeatureC with a Percentage filter at 50% enables the feature for half of users. This short-circuit evaluation improves performance.

---

## Card 2: Feature Management Core Components

**Q: What are the two essential components required for an effective feature management implementation, and how do they interact?**

**A:** (1) An application that uses feature flags, and (2) a separate repository that stores the feature flags and their current states (Azure App Configuration serves this role).

**Context:** This separation allows changing feature availability without code deployment or application restart. The feature manager in the application retrieves flag states from the repository and controls whether code blocks execute based on filters.

---
## Card 1: Customer-Managed Key Requirements

**Q: What are the three Azure resources required to enable customer-managed key capability for Azure App Configuration?**

**A:** (1) Standard tier App Configuration instance, (2) Azure Key Vault with soft-delete and purge-protection enabled, (3) RSA or RSA-HSM key in Key Vault that's not expired, enabled, and has wrap/unwrap capabilities.

**Context:** After configuring these resources, you must also: assign a managed identity to the App Configuration instance and grant it GET, WRAP, and UNWRAP permissions in Key Vault's access policy. App Configuration refreshes the unwrapped encryption key hourly.

---

## Card 2: Private Endpoint Security Benefits

**Q: What are the three main security benefits of using private endpoints for Azure App Configuration?**

**A:** (1) Block all public endpoint connections via firewall, (2) prevent data from escaping the virtual network, (3) enable secure on-premises access through VPN/ExpressRoute with private-peering.

**Context:** Private endpoints use an IP address from the virtual network address space. Traffic traverses the Microsoft backbone network via private link, eliminating public internet exposure. Clients on the VNet securely access App Configuration data.
# 🛠 Practice Exercises
**Hands-on tasks or labs:**  
- [ ] [Exercise - Retrieve configuration settings from Azure App Configuration - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/implement-azure-app-configuration/5a-retrieve-configuration-settings)

---
# 📚 Additional Notes
**Any extra insights, tips, or gotchas:** 