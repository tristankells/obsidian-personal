---

tags: [azure, cloud, certification, AZ-204]
created: 2025-12-08
---
# 📝 Summary
**What is this module about?**  
After completing this module, you'll be able to:
- Explain the benefits of using Microsoft Graph
- Perform operations on Microsoft Graph by using REST and SDKs
- Apply best practices to help your applications get the most out of Microsoft Graph
- Retrieve user profile information with the Microsoft Graph SDK
---
# 🔗 Links
**Useful resources and official docs:**  
- [Introduction - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/microsoft-graph/1-introduction)
---
# ✅ Module Assessment
**Key questions and answers from the module assessment:**  
> [!question] Question 1 Which HTTP method is used to partially update a resource with new values?
> 
> - POST
> - PATCH
> - PUT
> 
> > [!success]- Answer 
> > PATCH

> [!question] Question 2 Which of the components of the Microsoft 365 platform is used to deliver data external to Azure into Microsoft Graph services and applications?
> 
> - Microsoft Graph API
> - Microsoft Graph connectors
> - Microsoft Graph Data Connect
> 
> > [!success]- Answer 
> > Microsoft Graph connectors
---
---
# 🧠 Flashcards
**Important terms and definitions for quick recall:**  
## Card 1: Purpose of Microsoft Graph API

**Q: In the Microsoft 365 platform, what is the primary function of the Microsoft Graph API's single endpoint ([https://graph.microsoft.com](https://graph.microsoft.com))?**  
**A:** It provides unified access—via REST or SDKs—to Microsoft 365, Windows 10, and Enterprise Mobility + Security data, including identity, access, compliance, and security services.

**Context:** Microsoft Graph acts as the main gateway to Microsoft 365 data and intelligence, offering a single programmability model.

---

## Card 2: Direction of Data Flow in Microsoft Graph Connectors

**Q: In Microsoft 365 architecture, what direction of data flow do Microsoft Graph connectors handle, and for what purpose?**  
**A:** They bring _external_ data _into_ Microsoft Graph to enhance Microsoft 365 experiences (e.g., Microsoft Search).

**Context:** Connectors ingest data from sources like Box, Google Drive, Jira, and Salesforce to enrich Microsoft 365 services.

---
**Q: When working with Microsoft Graph resources, methods, and enumerations, what default namespace should you assume they belong to unless documentation states otherwise?**  
**A:** The **microsoft.graph** OData namespace.

**Context:** Most API elements are defined in microsoft.graph, with some exceptions like callRecords in microsoft.graph.callRecords.

---
## Card 1: Purpose of the Microsoft Graph SDK Core Library

**Q: In Microsoft Graph SDK architecture, what key capabilities does the _core library_ add to improve application reliability and performance?**  
**A:** It provides built-in support for retries, secure redirects, transparent authentication, payload compression, paging, and batch request creation.

**Context:** The SDK consists of a _service library_ (models + request builders) and a _core library_ (cross-service enhancements).

---

## Card 2: Difference Between Microsoft.Graph and Microsoft.Graph.Beta NuGet Packages

**Q: When installing the Microsoft Graph .NET SDK, what is the main functional difference between the `Microsoft.Graph` and `Microsoft.Graph.Beta` packages?**  
**A:** `Microsoft.Graph` targets the **v1.0** endpoint, while `Microsoft.Graph.Beta` targets the **beta** endpoint—both using the fluent API and both depending on `Microsoft.Graph.Core`.

**Context:** v1.0 is production-ready; beta is preview-only and may introduce breaking changes.

---
**Q: According to Microsoft Graph best practices, when should an application use _delegated permissions_ instead of _application permissions_?**  
**A:** Delegated permissions should be used when an interactive user is signed in; application permissions are only for non-interactive scenarios like background services or daemons.

**Context:** Using application permissions in interactive scenarios can create compliance and security risks by granting broader access than intended.

## Card 2: Handling Pagination in Microsoft Graph

**Q: What mechanism should an application use to retrieve additional pages when Microsoft Graph returns a paged collection response?**  
**A:** Follow the URL in the `@odata.nextLink` property until no further `nextLink` is present.

**Context:** Microsoft Graph often paginates large collections due to server-side limits; the final page omits `@odata.nextLink`.

---

## Card 3: Purpose of Evolvable Enumerations in Microsoft Graph

**Q: What problem do _evolvable enumerations_ solve in Microsoft Graph, and how can a client opt in to receiving unknown enum members?**  
**A:** They allow Microsoft Graph to add new enum values without breaking existing apps; clients can opt in to unknown members by sending an HTTP `Prefer` header.

**Context:** By default, GET operations return only known enum members unless the client explicitly requests otherwise.
# 🛠 Practice Exercises
**Objective:** Learn how to use the Microsoft Graph SDK to interact with Microsoft 365 services, focusing on retrieving user data.

- [ ] **1. Set up a .NET Application for Microsoft Graph:**
    - [ ] Follow the official Microsoft Learn exercise to create a .NET console application that authenticates and retrieves user profile information: [Retrieve user profile information with the Microsoft Graph SDK](https://learn.microsoft.com/en-us/training/modules/microsoft-graph/5a-exercise-microsoft-graph-user-profile).
- [ ] **2. Extend the Application:**
    - [ ] **Goal:** Go beyond the basic profile to retrieve more detailed user information.
    - [ ] **List User's Files:** Modify the application to query the signed-in user's OneDrive for Business and list the names of the first 10 files in their root directory.
    - [ ] **Read User's Calendar:** Add functionality to read the user's calendar and display their upcoming appointments for the next 7 days.
    - [ ] **Send an Email:** Implement a feature to send an email from the signed-in user's account to their own email address with a subject like "Microsoft Graph Test".
---
# 📚 Additional Notes
**Any extra insights, tips, or gotchas:** 