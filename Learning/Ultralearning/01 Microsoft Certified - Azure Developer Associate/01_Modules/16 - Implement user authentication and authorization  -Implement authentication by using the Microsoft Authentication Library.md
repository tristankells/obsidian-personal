---

tags: [azure, cloud, certification, AZ-204]
created: 2025-12-03
---
# 📝 Summary
**What is this module about?**  
After completing this module, you'll be able to:
- Explain the benefits of using MSAL and the application types and scenarios it supports
- Instantiate both public and confidential client apps from code
- Register an app with the Microsoft identity platform
- Create an app that retrieves a token with the MSAL.NET SDK
---
# 🔗 Links
**Useful resources and official docs:**  
- [Implement Authentication by Using the Microsoft Authentication Library - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/implement-authentication-by-using-microsoft-authentication-library/)

---
# ✅ Module Assessment
**Key questions and answers from the module assessment:**  
> [!question] Question 1 Which of the following MSAL libraries supports single-page web apps?
> 
> - MSAL Node
> - MSAL.js
> - MSAL.NET
> 
> > [!success]- Answer 
> > MSAL.js

> [!question] Question 2 What is the purpose of using `PublicClientApplicationBuilder` class in MSAL.NET?
> 
> - The class creates a new Azure account.
> - To configure and instantiate a public client application that can acquire tokens and authenticate users against the Microsoft identity platform.
> - Adds a new API permission to the registered app.
> 
> > [!success]- Answer 
> > To configure and instantiate a public client application that can acquire tokens and authenticate users against the Microsoft identity platform.

---
# 🧠 Flashcards
**Important terms and definitions for quick recall:**  
## Card 1: Public vs. Confidential Client Distinction

**Q: In MSAL context, what is the specific security capability that distinguishes a "Confidential Client" application from a "Public Client" application?**

**A:** The ability to safely store **configuration-time secrets** (application secrets) to prove its identity without them being accessible/inspectable by users.

**Context:**

- **Public Clients:** Mobile/SPAs. Cannot hold secrets because users can inspect the source code/bytecode.
    
- **Confidential Clients:** Web Apps/Daemons. Run on servers where secrets are kept on a back channel.
    

---

## Card 2: MSAL Token Lifecycle Management

**Q: How does the Microsoft Authentication Library (MSAL) handle token expiration to reduce the developer's workload?**

**A:** It maintains a **token cache** and automatically **refreshes tokens** when they are close to expiring, so the app doesn't need to handle expiration logic manually.

**Context:** Without MSAL, developers would have to manually code against the OAuth protocol to check expiration times and request new tokens.

---

## Card 3: Selecting the Client Credentials Flow

**Q: Which MSAL authentication flow is required for server-to-server communication (e.g., daemons or automated scripts) where no user interaction is possible?**

**A:** **Client credentials flow**

**Context:** This flow uses the **application's identity** rather than a user's identity. In contrast, flows like "Authorization Code" or "Device Code" authenticate on behalf of a specific user.

## Card 4: Composition of Authority

**Q: In the context of MSAL application registration, which two parameters combine to form the "Authority"?**

**A:**

1. **The Instance** (The Identity Provider URL)
    
2. **The Audience** (The target sign-in group, e.g., single-tenant vs multi-tenant)
    

**Context:** Example: `https://login.microsoftonline.com` (Instance) + `/common` (Audience). The Authority defines _who_ provides the identity and _who_ can use it.

---

## Card 5: Confidential Client Credentials Constraints

**Q: When configuring a `ConfidentialClientApplicationBuilder`, what is the constraint regarding the `.WithCertificate()` and `.WithClientSecret()` modifiers?**

**A:** They are **mutually exclusive** — providing both will cause MSAL to throw an exception.

**Context:** You must choose exactly one method for the app to prove its identity: either a shared string secret OR an X509 certificate. You cannot use both simultaneously.

---
# 🛠 Practice Exercises
**Objective:** Learn how to use the Microsoft Authentication Library (MSAL) for .NET to implement user authentication in a desktop application.

- [ ] **1. Follow the Guided Exercise:**
    - [ ] Complete the official Microsoft Learn exercise: [Implement interactive authentication with MSAL.NET](https://learn.microsoft.com/en-us/training/modules/implement-authentication-by-using-microsoft-authentication-library/4-interactive-authentication-msal). This will walk you through:
        - Registering an application in Microsoft Entra ID.
        - Configuring the application for public client (desktop) use.
        - Writing the .NET code to acquire a token interactively.
- [ ] **2. Token Caching and Silent Acquisition:**
    - [ ] **Goal:** Modify the application to first attempt a silent token acquisition before falling back to interactive login.
    - [ ] After the first successful interactive login, the token will be in MSAL's cache.
    - [ ] Relaunch the application and use `AcquireTokenSilent` to get the token from the cache without prompting the user for credentials again.
    - [ ] Implement the `try/catch` block so that if `AcquireTokenSilent` fails (e.g., the token has expired or the user revoked consent), it falls back to `AcquireTokenInteractive`.
- [ ] **3. Explore Different Authentication Flows (Conceptual):**
    - [ ] **Device Code Flow:**
        - Research how the device code flow works.
        - Modify your application to use `AcquireTokenWithDeviceCode`. This is useful for CLI apps or devices without a web browser. The user will be given a code to enter on another device to sign in.
    - [ ] **Integrated Windows Authentication (IWA):**
        - If you are on a domain-joined Windows machine, try to configure and use `AcquireTokenByIntegratedWindowsAuth`. This provides a seamless sign-in experience for users already logged into Windows.
---
# 📚 Additional Notes
**Any extra insights, tips, or gotchas:** 