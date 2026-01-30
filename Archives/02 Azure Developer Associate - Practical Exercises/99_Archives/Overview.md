# Todo
- Need to read through [[🎯 AZ-204 Free Azure Services Implementation Plan]], and map each product use cases with a real feature you you would like in envelopes.
- Create a document for each product, numbered in the order you would use them.
- Create an overall plan to complete the steps on each document as you go.
- Add links to Azure / Microsoft guides to each document.
- Take careful considerations for when you can't figure out how to do something without reference, and create exercises / flash cards you can revisit to cement that knowledge.
- Build up your reservoir of guides, snippets and cookbooks as you go.


```
Here is my app:

```
```

Envelopes.App is a private C# web application designed for envelope-based budgeting. Built with Blazor WebAssembly, it enables users to manage their finances by allocating funds to different virtual envelopes, following the envelope budgeting methodology.

Current Features:

- Dashboard summarizing budget and envelope categories
- Account and transaction management
- Categorization of expenses and incomes
- Budget planning with adjustable frequencies (e.g., monthly, fortnightly)
- Category notes, planned/actual amounts, accumulation settings, and summary views
- Notification system for feedback and workflow
- Uses GraphQL for backend data interactions

Technologies and Frameworks:

- .NET (C#), Blazor WebAssembly for frontend/UI
- GraphQL.Client for backend API integration
- Bootstrap and Bootstrap Icons for styling
- Follows best practices for configuration and sensitive data management

The application architecture is modular, with features for accounts, categories, transactions, incomes, and planning, all integrated into a modern, responsive web interface.

Envelopes.App serves as the frontend client for the Envelopes.Api backend. It communicates with Envelopes.Api—primarily via GraphQL and HTTP APIs—to retrieve and manage financial data such as accounts, transactions, categories, and planning information. All user interactions in Envelopes.App, such as budgeting or transaction entry, result in secure API requests to Envelopes.Api, which acts as the authoritative data source for the application.

```
```

I'm studying towards AZ-204, and I want to use the free Azure services to get some pracical hands on experiecne with the following topics:

#### **1.1 Azure App Service (Always Free - F1 Tier)**
**1.2 Azure Functions (Always Free)**
 **2.2 Azure Queue Storage - USE AZURITE**
 **2.3 Azure Table Storage - USE AZURITE**
 #### **2.5 Azure Cosmos DB (Always Free)**
 Azure Key Vault - LIMITED WITHOUT 12-MONTH FREE**
 Azure Active Directory (Azure AD) / Microsoft Entra ID (Always Free)**
 #### **3.3 Managed Identities (Always Free)**
 **4.1 Application Insights (Always Free)**
 **4.2 Azure Monitor (Always Free Components)**
 **4.3 Azure Log Analytics (Limited Free)**
 **5.2 Azure Event Grid (Always Free)**
 #### **5.4 Azure API Management (Consumption Tier - Always Free)**
 #### **5.6 Azure SignalR Service (Always Free)**
 #### **Azure DevOps (Always Free)**
 **Azure Virtual Network (Always Free)**
 #### **Azure Load Balancer (Always Free - Basic)**
 
Can you write me a 8 week schedule, with a checklist of features of each component I should explore to be ready for AZ-204 exam? Could you relate this list with actual uses cases for feaures I could add to my enveloeps budgetting app?








```