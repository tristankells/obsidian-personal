---
title: "15 - Implement user authentication and authorization - Explore the Microsoft identity platform"
tags: [azure, cloud, certification, AZ-204]
created: 2025-12-02
---
# 📝 Summary
**What is this module about?**  
After completing this module, you'll be able to:
- Identify the components of the Microsoft identity platform.
- Describe the three types of service principals and how they relate to application objects.
- Explain how permissions and user consent operate, and how conditional access impacts your application.

---
# 🔗 Links
**Useful resources and official docs:**  
- [Explore the Microsoft Identity Platform - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/explore-microsoft-identity-platform/)

---
# ✅ Module Assessment
**Key questions and answers from the module assessment:**  
> [!question] Question 1 Which of the types of permissions supported by the Microsoft identity platform is used by apps that have a signed-in user present?
> 
> - Delegated permissions
> - App-only access permissions
> - Both delegated and app-only access permissions
> 
> > [!success]- Answer 
> > Delegated permissions

> [!question] Question 2 Which of the following app scenarios require code to handle Conditional Access challenges?
> 
> - Apps performing the device-code flow
> - Apps performing the on-behalf-of flow
> - Apps performing the Integrated Windows authentication flow
> 
> > [!success]- Answer 
> > Apps performing the on-behalf-of flow

---
# 🧠 Flashcards
**Important terms and definitions for quick recall:**  
## Card 1: Microsoft Identity Platform Components

**Q: What are the five main components that make up the Microsoft identity platform?**

**A:**

1. OAuth 2.0/OpenID Connect authentication service
2. Open-source libraries (MSAL and standards-compliant libraries)
3. Microsoft identity platform endpoint
4. Application management portal (in Azure portal)
5. Application configuration API and PowerShell

**Context:** Microsoft identity platform architecture - these components work together to enable developers to build applications with authentication and authorization. The platform handles modern security features like passwordless authentication and Conditional Access automatically.

## Card 1: Application Registration - Tenant Access Types

**Q: In Microsoft Entra ID application registration, what are the two tenant access options you can choose, and what is the difference between them?**

**A:**

1. **Single tenant:** Only accessible in your tenant
2. **Multi-tenant:** Accessible in other tenants

**Context:** Microsoft Entra ID app registration - this choice determines whether your application can authenticate users only from your organization or from multiple organizations. The choice affects how service principals are created across tenants.

---

## Card 2: Application Object vs Service Principal - Relationship

**Q: What is the relationship between an application object and service principal objects in Microsoft Entra ID?**

**A:** The application object is the **global** representation (template/blueprint) used across all tenants with a **one-to-many** relationship to service principals. Service principals are **local** representations created in each specific tenant where the application is used.

**Context:** Microsoft Entra ID identity configuration - the application object resides only in the home tenant where the app was registered. A single-tenant app has one service principal; a multi-tenant app has a service principal in each consenting tenant.

---

## Card 3: Service Principal Types in Microsoft Entra ID

**Q: What are the three types of service principals in Microsoft Entra ID?**

**A:**

1. **Application:** Local representation of a global app object in a tenant
2. **Managed identity:** Represents a managed identity for connecting to resources
3. **Legacy:** Represents apps created before app registrations or through legacy experiences

**Context:** Microsoft Entra ID security principals - service principals define access policies and permissions for applications in a tenant, enabling authentication and authorization. Managed identity service principals can't be updated directly.


## Card 1: OAuth 2.0 Permission Sets - Scopes Definition

**Q: In the Microsoft identity platform's OAuth 2.0 implementation, what are permission sets called, and how is a permission represented?**

**A:** Permission sets are called **scopes** (also referred to as permissions), and each permission is represented as a **string value** (e.g., `https://graph.microsoft.com/Calendars.Read`).

**Context:** OAuth 2.0 in Microsoft identity platform - scopes allow resource functionality to be divided into smaller chunks so apps only request needed permissions. The string format appends the permission value to the resource's identifier or application ID URI.

---

## Card 2: Microsoft Identity Platform - Permission Types

**Q: What are the two types of permissions supported by the Microsoft identity platform, and what is the key difference between them?**

**A:**

1. **Delegated access:** Used by apps with a signed-in user present (user or admin consents; app acts on behalf of user)
2. **App-only access:** Used by apps running without a signed-in user, like background services/daemons (only admin can consent)

**Context:** Microsoft identity platform authorization model - the permission type determines whether a user must be signed in and who can grant consent. App-only access requires administrator consent due to higher privilege level.

---

## Card 3: Static vs. Incremental User Consent

**Q: What is the main advantage of incremental (dynamic) user consent over static user consent in the Microsoft identity platform?**

**A:** Incremental consent allows apps to request a **minimum set of permissions upfront** and **request more over time** as users access more features, rather than requesting all permissions at first sign-in (which can discourage users with long permission lists).

**Context:** Microsoft identity platform consent types - incremental consent uses the `scope` parameter at token request time without predefining in app registration. However, it only applies to delegated permissions, not app-only access, and creates challenges for admin consent scenarios.

---
**Q: In what specific scenarios does a Microsoft Entra ID Conditional Access policy require code changes in an application (rather than working automatically)?**

**A:** When an app **indirectly or silently requests a token** for a service. Specific scenarios include:

- Apps performing the on-behalf-of flow
- Apps accessing multiple services/resources
- Single-page apps using MSAL.js
- Web apps calling a resource

**Context:** Microsoft Entra ID Conditional Access - in most cases, Conditional Access works without code changes (like simple interactive sign-in with MFA). Code changes are needed for challenge handling when tokens are requested non-interactively, such as a middle-tier service requesting downstream API access where a claims "challenge" must be passed back to the app.

---
# 🛠 Practice Exercises
**Hands-on tasks or labs:**  
- Setup authentication for your single tenant envelopes service.

---
# 📚 Additional Notes
**Any extra insights, tips, or gotchas:** 