# 📋 Overview

This guide maps all free-tier Azure services you can use to implement AZ-204 exam concepts with your existing .NET web application and API—**without paying anything**.

---

## ✅ **ALWAYS-FREE AZURE SERVICES FOR AZ-204 (No Credit Required)**

### **DOMAIN 1: Develop Azure Compute Solutions (25-30%)**

#### **1.1 Azure App Service (Always Free - F1 Tier)**

**Free Tier:** 10 web, mobile, or API apps with 1 GB storage and 165 MB/day data transfer **Duration:** ALWAYS FREE (not time-limited)

**What You Can Do:**

- [ ] Deploy your .NET web application to App Service
- [ ] Deploy your .NET Web API to App Service
- [ ] Configure custom domains (using your Cloudflare domain)
- [ ] Set up continuous deployment from GitHub
- [ ] Configure application settings and connection strings
- [ ] Implement App Service authentication

**Limitations on Free Tier:**

- ❌ No deployment slots (staging/production)
- ❌ No autoscaling
- ❌ No custom SSL (but Let's Encrypt works)
- ✅ Still great for learning core concepts

**AZ-204 Topics Covered:**

- Create an Azure App Service Web App
- Enable diagnostics logging
- Deploy code to a web app
- Configure web app settings

**Implementation Steps:**

1. Create Free App Service plan (F1 tier)
2. Deploy your existing .NET app via Visual Studio/VS Code
3. Configure application insights (free tier - see monitoring section)

---

#### **1.2 Azure Functions (Always Free)**

**Free Tier:** 1 million executions per month + 400,000 GB-s of resource consumption **Duration:** ALWAYS FREE (not time-limited)

**What You Can Do:**

- [ ] Create HTTP-triggered functions for your API
- [ ] Create timer-triggered functions for background jobs (up to once per minute is very achievable)
- [ ] Create queue-triggered functions
- [ ] Create blob-triggered functions
- [ ] Implement function bindings (input/output)

**Limitations:**

- ❌ Durable Functions require premium plan (skip for free tier)
- ✅ 1M executions is MORE than enough for learning

**AZ-204 Topics Covered:**

- Create and deploy Azure Functions
- Implement input and output bindings
- Implement function triggers (HTTP, timer, queue, blob)

**Implementation Steps:**

1. Create Function App (Consumption plan - free)
2. Convert some API endpoints to serverless functions
3. Create scheduled tasks (e.g., data cleanup, reports)
4. Implement queue processing functions

**Example Use Cases for Your App:**

- Image processing function (blob trigger)
- Scheduled email notifications (timer trigger - every 5 minutes)
- API rate limiting function (HTTP trigger)
- Background data processing (queue trigger)

---

#### **1.3 ⚠️ Azure Container Instances - LIMITED FREE OPTIONS**

**Reality Check:** Container instances have minimal free tier options without credits

**Alternative Free Approach:**

- [ ] Learn Docker locally (completely free)
- [ ] Build container images for your .NET app
- [ ] Push to Docker Hub (free tier: 1 private repo)
- [ ] Learn Dockerfile and containerization concepts
- [ ] When you have Azure credits later, you'll be ready

**What to Learn Now (Free):**

- [ ] Create Dockerfile for your .NET app
- [ ] Build and test containers locally
- [ ] Understand container concepts
- [ ] Practice docker-compose for multi-container apps

---

#### **1.4 ⚠️ Azure Container Registry - SKIP FOR NOW**

**Reality Check:** Basic tier costs ~$5/month

**Alternative:**

- [ ] Use Docker Hub free tier (1 private repository)
- [ ] Learn container registry concepts
- [ ] Practice locally with docker registry

---

#### **1.5 ⚠️ Azure Kubernetes Service - SKIP FOR NOW**

**Reality Check:** Requires VMs which cost money without free credits

**Alternative:**

- [ ] Install minikube or kind locally (completely free)
- [ ] Learn Kubernetes concepts locally
- [ ] Practice kubectl commands
- [ ] Create deployment YAML files
- [ ] When you have credits, deploy to AKS

---

### **DOMAIN 2: Develop for Azure Storage (15-20%)**

#### **⚠️ 2.1 Azure Blob Storage - VERY LIMITED WITHOUT CREDITS**

**Reality Check:** Without the 12-month free tier, you get minimal free storage

**What's Actually Free:**

- Very small amounts of storage operations per month
- Not practical for real application usage

**Alternative Approach:**

- [ ] Use Azure Storage Emulator (Azurite) - **COMPLETELY FREE**
- [ ] Develop locally with Azurite
- [ ] Learn all blob operations locally
- [ ] Test your code without any Azure costs

**Azurite Setup (Free Local Development):**

```bash
# Install Azurite (local storage emulator)
npm install -g azurite

# Run Azurite
azurite --silent --location c:\azurite --debug c:\azurite\debug.log

# Use connection string in your app:
UseDevelopmentStorage=true
```

**What You Can Learn (Completely Free):**

- [ ] Blob upload/download operations
- [ ] Container management
- [ ] Blob properties and metadata
- [ ] SAS token generation and usage
- [ ] All blob storage patterns

**AZ-204 Topics Covered:**

- Create and configure Azure Storage accounts (learn concepts)
- Upload, download, and manage blobs (practice with Azurite)
- Set blob properties and metadata
- Implement storage security (SAS tokens work locally)
- Manage blob lifecycle (learn concepts)

---

#### **2.2 Azure Queue Storage - USE AZURITE**

**Free Solution:** Azure Storage Emulator (Azurite)

**What You Can Do (Completely Free):**

- [ ] Implement message queuing with Azurite
- [ ] Create background job processing
- [ ] Practice queue operations (enqueue, dequeue, peek)
- [ ] Implement retry logic
- [ ] Test queue-triggered functions locally

**AZ-204 Topics Covered:**

- Create and manage queues
- Add messages to and retrieve messages from queues
- Implement queue storage security

---

#### **2.3 Azure Table Storage - USE AZURITE**

**Free Solution:** Azure Storage Emulator (Azurite)

**What You Can Do (Completely Free):**

- [ ] Store NoSQL data locally
- [ ] Implement CRUD operations
- [ ] Practice partitioning strategies
- [ ] Query table data

**AZ-204 Topics Covered:**

- Create tables and entities
- Query Table storage
- Implement partitioning strategies

---

#### **2.4 Azure Files - SKIP**

**Reality Check:** Not available in always-free tier

**Alternative:**

- [ ] Learn concepts through documentation
- [ ] Skip hands-on for now

---

#### **2.5 Azure Cosmos DB (Always Free)**

**Free Tier:** First 1000 RU/s and 25 GB storage **FOREVER** **Duration:** ALWAYS FREE (not time-limited)

**This is a GOLD MINE for free learning!**

**What You Can Do:**

- [ ] Migrate some of your data to NoSQL
- [ ] Practice different APIs (SQL, MongoDB, Cassandra, Gremlin, Table)
- [ ] Implement global distribution concepts
- [ ] Practice consistency levels
- [ ] Implement change feed
- [ ] Query with SQL API

**Limitations:**

- 1000 RU/s throughput (enough for development)
- 25 GB storage (plenty for learning)
- Limited regions (but you can still learn replication concepts)

**AZ-204 Topics Covered:**

- Create Cosmos DB resources
- Implement partitioning strategies
- Configure consistency levels
- Query Cosmos DB

**Implementation Steps:**

1. Create Cosmos DB account (SQL API) - **SELECT FREE TIER**
2. Migrate a data table to Cosmos DB
3. Update your API to query Cosmos DB
4. Implement change feed for real-time updates

**Example Use Cases:**

- Product catalog
- User profiles
- Real-time analytics
- Shopping cart data

**PRO TIP:** You can only have ONE free Cosmos DB account per subscription, so make it count!

---

### **DOMAIN 3: Implement Azure Security (15-20%)**

#### **⚠️ 3.1 Azure Key Vault - LIMITED WITHOUT 12-MONTH FREE**

**Reality Check:** Basic operations have minimal costs (~$0.03 per 10,000 operations)

**What This Means:**

- Creating a Key Vault: Free
- Storing secrets: ~$0.03 per secret per month
- Reading secrets: ~$0.03 per 10,000 operations
- For learning purposes: **Costs pennies per month**

**Recommendation:**

- [ ] Create ONE Key Vault for learning
- [ ] Store a few secrets (will cost cents)
- [ ] Practice retrieving secrets in your app
- [ ] Expected monthly cost: **$0.50-$2.00**

**If You Want Completely Free:**

- [ ] Use Azure Key Vault SDK with local development
- [ ] Use user secrets in .NET (local development)
- [ ] Learn concepts without cloud deployment

**AZ-204 Topics Covered:**

- Create and manage Key Vaults (concepts)
- Store and retrieve secrets (practice locally)
- Implement managed identities (free - see below)
- Configure Key Vault access policies

---

#### **3.2 Azure Active Directory (Azure AD) / Microsoft Entra ID (Always Free)**

**Free Tier:** Free for up to 50,000 objects **Duration:** ALWAYS FREE

**What You Can Do:**

- [ ] Implement user authentication
- [ ] Configure app registrations
- [ ] Implement OAuth 2.0 / OpenID Connect
- [ ] Configure API permissions
- [ ] Implement role-based access control (RBAC)
- [ ] Use Microsoft Identity Platform

**AZ-204 Topics Covered:**

- Implement authentication
- Implement secure cloud solutions
- Implement OAuth 2.0 authentication
- Register applications in Azure AD

**Implementation Steps:**

1. Register your web app in Azure AD (FREE)
2. Register your API in Azure AD (FREE)
3. Implement authentication in web app (FREE)
4. Implement authorization in API (FREE)
5. Configure API scopes and permissions (FREE)

**Example Implementation:**

- Replace custom login with Azure AD
- Implement "Login with Microsoft"
- Secure API endpoints with bearer tokens
- Implement role-based access

**This is 100% FREE and a core AZ-204 topic!**

---

#### **3.3 Managed Identities (Always Free)**

**Free Tier:** Completely free feature **Duration:** ALWAYS FREE

**What You Can Do:**

- [ ] Enable managed identity for App Service (FREE)
- [ ] Enable managed identity for Functions (FREE)
- [ ] Access Key Vault without storing credentials
- [ ] Access Storage without connection strings
- [ ] Access Cosmos DB with managed identity

**AZ-204 Topics Covered:**

- Implement managed identities for Azure resources
- Implement secure app configuration

**Implementation Steps:**

1. Enable system-assigned managed identity on App Service
2. Grant identity access to resources
3. Update code to use DefaultAzureCredential
4. Remove connection strings from configuration

**This is COMPLETELY FREE and essential for security!**

---

### **DOMAIN 4: Monitor, Troubleshoot, and Optimize (10-15%)**

#### **4.1 Application Insights (Always Free)**

**Free Tier:** 5 GB data ingestion per month **FOREVER** **Duration:** ALWAYS FREE

**What You Can Do:**

- [ ] Monitor application performance
- [ ] Track custom events and metrics
- [ ] Implement distributed tracing
- [ ] Monitor dependencies
- [ ] Track exceptions and failures
- [ ] Create availability tests (limited on free tier)
- [ ] Analyze user behavior
- [ ] Create custom dashboards

**Limitations on Free Tier:**

- 5 GB/month ingestion (plenty for learning)
- 90-day data retention
- Limited multi-step web tests

**AZ-204 Topics Covered:**

- Implement Application Insights
- Configure an app or service to use Application Insights
- Monitor and analyze metrics
- Implement availability tests

**Implementation Steps:**

1. Create Application Insights resource (FREE)
2. Add Application Insights SDK to your app
3. Configure instrumentation key
4. Implement custom telemetry
5. Create alerts for failures
6. Set up basic availability tests

**Custom Tracking Examples:**

```csharp
telemetryClient.TrackEvent("UserPurchase", 
    new Dictionary<string, string> { { "ProductId", "123" } },
    new Dictionary<string, double> { { "Amount", 99.99 } });

telemetryClient.TrackMetric("QueueLength", queueLength);
telemetryClient.TrackDependency("SQL", "GetUser", startTime, duration, success);
```

**This is one of the BEST free services for learning!**

---

#### **4.2 Azure Monitor (Always Free Components)**

**Free Tier:** Basic metrics and activity logs are free **FOREVER**

**What You Can Do:**

- [ ] Create metric alerts (limited)
- [ ] Monitor resource health
- [ ] View activity logs
- [ ] Create action groups (email/webhook)
- [ ] Configure basic log alerts

**Limitations:**

- Limited alert rules on free resources
- Advanced features require paid tiers

---

#### **4.3 Azure Log Analytics (Limited Free)**

**Reality Check:** 5 GB/month free with Application Insights, but standalone costs

**Recommendation:**

- [ ] Use Application Insights instead (includes Log Analytics)
- [ ] Learn KQL queries through App Insights
- [ ] Practice log queries on your telemetry data

---

#### **4.4 ⚠️ Azure Content Delivery Network (CDN) - SKIP FOR NOW**

**Reality Check:** Basic tier has minimal costs (~$0.085/GB)

**Alternative:**

- [ ] Use Cloudflare CDN (you're already using it!)
- [ ] Learn CDN concepts through Cloudflare
- [ ] Azure CDN concepts are similar

---

### **DOMAIN 5: Connect to and Consume Services (20-25%)**

#### **⚠️ 5.1 Azure Service Bus - NOT FREE**

**Reality Check:** Basic tier costs ~$0.05/hour (~$10-12/month)

**Alternative for Learning:**

- [ ] Use Azure Queue Storage with Azurite (completely free)
- [ ] Learn Service Bus concepts through documentation
- [ ] Understand differences: Queue Storage vs Service Bus
- [ ] Skip hands-on until you have credits

**What You Miss:**

- Topics and subscriptions (pub/sub)
- Advanced messaging features
- Sessions and transactions

**What You Can Still Learn:**

- Basic queuing concepts work the same
- Message patterns
- Dead-letter concepts

---

#### **5.2 Azure Event Grid (Always Free)**

**Free Tier:** 100,000 operations per month **FOREVER** **Duration:** ALWAYS FREE

**What You Can Do:**

- [ ] Implement event-driven architecture
- [ ] Subscribe to system events (free)
- [ ] Create custom topics (10/month free)
- [ ] Implement event handlers with Functions
- [ ] Filter events
- [ ] Route events to different endpoints

**Limitations:**

- 10 custom topics max on free tier
- 100,000 operations (plenty for learning)

**AZ-204 Topics Covered:**

- Implement solutions that use Azure Event Grid
- Implement event-driven solutions

**Implementation Steps:**

1. Create Event Grid topic (FREE - within limits)
2. Subscribe to blob storage events (FREE)
3. Trigger functions on events (FREE)
4. Process events in your application

**Example Use Cases:**

- Trigger image processing when uploaded
- Send notifications on data changes
- Trigger workflows on storage events
- Real-time notifications

**This is EXCELLENT for learning event-driven patterns!**

---

#### **⚠️ 5.3 Azure Event Hubs - NOT FREE**

**Reality Check:** Basic tier costs ~$11/month minimum

**Alternative:**

- [ ] Learn concepts through documentation
- [ ] Use Event Grid for simpler event scenarios
- [ ] Skip hands-on until you have credits

---

#### **5.4 Azure API Management (Consumption Tier - Always Free)**

**Free Tier:** First 1 million calls **FOREVER** **Duration:** ALWAYS FREE

**What You Can Do:**

- [ ] Create API gateway
- [ ] Implement API policies (rate limiting, caching, transformation)
- [ ] Configure API security
- [ ] Transform requests and responses
- [ ] Create API documentation
- [ ] Implement API versioning
- [ ] Monitor API usage

**Limitations on Consumption Tier:**

- No developer portal UI (but APIs work great)
- Limited to 1000 requests/second
- No custom domains (but fine for learning)

**AZ-204 Topics Covered:**

- Create an APIM instance
- Configure authentication for APIs
- Define policies for APIs

**Implementation Steps:**

1. Create API Management service (Consumption tier - FREE)
2. Import your Web API
3. Configure policies (rate limiting, CORS, caching)
4. Implement API key authentication
5. Test API transformations
6. Monitor API calls

**This is AMAZING for learning - completely free!**

---

#### **⚠️ 5.5 Azure Logic Apps - MINIMAL FREE**

**Reality Check:** Consumption plan charges per action (~$0.000025 per action)

**What This Means:**

- First 4,000 actions: **FREE**
- After that: Pennies per action
- For learning: **Costs very little (maybe $1-2/month)**

**Recommendation:**

- [ ] Create a few Logic Apps for learning
- [ ] Keep workflows simple
- [ ] Disable when not testing
- [ ] Expected cost: **$0-2/month**

**What You Can Learn (Nearly Free):**

- [ ] Create automated workflows
- [ ] Connect to various connectors
- [ ] Implement approval workflows
- [ ] Process data transformations

---

#### **5.6 Azure SignalR Service (Always Free)**

**Free Tier:** 20 concurrent connections, 20,000 messages/day **FOREVER** **Duration:** ALWAYS FREE

**What You Can Do:**

- [ ] Implement real-time communication
- [ ] Add real-time features to your app
- [ ] Implement chat functionality
- [ ] Push updates to connected clients

**Limitations:**

- 20 concurrent connections (enough for development)
- 20,000 messages per day (plenty for learning)

**AZ-204 Topics Covered:**

- Implement real-time messaging

**Implementation Steps:**

1. Create SignalR Service (Free tier)
2. Add real-time notifications to your app
3. Implement live updates
4. Create simple chat features

**Example Use Cases:**

- Real-time notifications
- Live dashboard updates
- Simple chat
- Progress indicators

**This is PERFECT for adding real-time features!**

---

### **ADDITIONAL FREE SERVICES (Not Core AZ-204 but Useful)**

#### **Azure DevOps (Always Free)**

**Free Tier:** Free for first 5 users

**What You Can Do:**

- [ ] Set up CI/CD pipelines
- [ ] Implement automated builds
- [ ] Deploy to Azure automatically
- [ ] Track work items
- [ ] Host Git repositories

---

#### **Azure Virtual Network (Always Free)**

**Free Tier:** First 100 virtual networks free

**What You Can Do:**

- [ ] Create virtual networks
- [ ] Configure subnets
- [ ] Implement network security groups
- [ ] Practice VNet peering concepts

---

#### **Azure Load Balancer (Always Free - Basic)**

**Free Tier:** Basic load balancer is free

**What You Can Do:**

- [ ] Distribute traffic across instances
- [ ] Configure health probes
- [ ] Implement load balancing rules

---

## 🗓️ **8-WEEK IMPLEMENTATION PLAN**

### **Week 1: Foundation & Compute**

- [ ] Create Azure free account
- [ ] Deploy .NET web app to App Service (Free tier)
- [ ] Deploy .NET API to App Service
- [ ] Set up Application Insights
- [ ] Configure custom domain via Cloudflare

**Deliverable:** Web app and API running on Azure

---

### **Week 2: Storage Implementation**

- [ ] Create Storage Account
- [ ] Implement blob upload/download in your app
- [ ] Add queue processing
- [ ] Set up table storage for session data
- [ ] Configure lifecycle management

**Deliverable:** App using Blob, Queue, and Table storage

---

### **Week 3: Security Implementation**

- [ ] Create Key Vault
- [ ] Move all secrets to Key Vault
- [ ] Enable managed identity on App Service
- [ ] Configure app to read from Key Vault
- [ ] Implement Azure AD authentication

**Deliverable:** Fully secured application with no secrets in code

---

### **Week 4: Serverless & Functions**

- [ ] Create Function App
- [ ] Convert 2-3 API endpoints to functions
- [ ] Create timer-triggered background job
- [ ] Create queue-triggered function
- [ ] Create blob-triggered function

**Deliverable:** Hybrid app with serverless components

---

### **Week 5: Containers**

- [ ] Containerize your .NET application
- [ ] Create Azure Container Registry
- [ ] Push images to ACR
- [ ] Deploy to Azure Container Instances
- [ ] Set up automated builds

**Deliverable:** Containerized application running in Azure

---

### **Week 6: Data & NoSQL**

- [ ] Create Cosmos DB account (free tier)
- [ ] Migrate one data table to Cosmos DB
- [ ] Update API to query Cosmos DB
- [ ] Implement change feed
- [ ] Practice different consistency levels

**Deliverable:** Hybrid SQL/NoSQL application

---

### **Week 7: Integration & Messaging**

- [ ] Create Event Grid topic
- [ ] Set up blob storage event subscription
- [ ] Create API Management instance
- [ ] Import your API
- [ ] Configure API policies
- [ ] Add SignalR for real-time updates

**Deliverable:** Event-driven app with API gateway

---

### **Week 8: Monitoring & Optimization**

- [ ] Configure advanced Application Insights tracking
- [ ] Create custom metrics and events
- [ ] Set up availability tests
- [ ] Create alerts
- [ ] Set up CDN for static content
- [ ] Implement Azure Monitor dashboards
- [ ] Configure log analytics queries

**Deliverable:** Fully monitored, production-ready application

---

## 📊 **COST TRACKING & LIMITS**

### **How to Stay Free:**

1. **Set up billing alerts:**
    
    - [ ] Go to Cost Management + Billing
    - [ ] Create alert for $1, $5, $10 thresholds
    - [ ] Review costs weekly
2. **Monitor free tier usage:**
    
    - [ ] Check Azure free services page monthly
    - [ ] Track App Service hours (1 GB free)
    - [ ] Monitor storage usage (5 GB limit)
    - [ ] Watch Function executions (1M free)
    - [ ] Track Application Insights ingestion (5 GB free)
3. **Delete resources when done:**
    
    - [ ] Delete VMs immediately after practice
    - [ ] Remove Service Bus after learning
    - [ ] Keep only always-free services running
4. **Use resource groups:**
    
    - [ ] Create separate resource group for experiments
    - [ ] Delete entire group when done with section
    - [ ] Easy cleanup

---

## ✅ **QUICK START CHECKLIST**

**Before You Begin:**

- [ ] Create Azure free account
- [ ] Verify $200 credit applied (30 days)
- [ ] Set up billing alerts
- [ ] Install Azure CLI
- [ ] Install Azure Storage Explorer
- [ ] Install Azure Data Studio (optional)
- [ ] Set up Visual Studio/VS Code with Azure extensions

**Essential Extensions for VS Code:**

- [ ] Azure Account
- [ ] Azure App Service
- [ ] Azure Functions
- [ ] Azure Storage
- [ ] Azure Resources

---

## 🎯 **AZ-204 EXAM TOPIC COVERAGE**

**Percentage of Free Services per Domain:**

|Domain|Free Services Available|Coverage|
|---|---|---|
|Compute Solutions (25-30%)|App Service, Functions, Containers, AKS|100%|
|Azure Storage (15-20%)|Blob, Queue, Table, Files, Cosmos DB|100%|
|Security (15-20%)|Key Vault, Azure AD, Managed Identity|100%|
|Monitor & Optimize (10-15%)|App Insights, Monitor, CDN|100%|
|Connect & Consume (20-25%)|Event Grid, SignalR, API Management|95%|

**Services with Minimal Cost (that you can practice then delete):**

- Service Bus Basic: ~$10/month (use for 1-2 days then delete)
- Event Hubs Basic: ~$11/month (use for 1-2 days then delete)
- Small VMs: B1s tier (750 hours free for 12 months)

**Total Cost for 8 Weeks:** $0 if you stay within free tiers and delete temporary resources!

---

## 💡 **PRO TIPS**

1. **Use the $200 credit wisely:**
    
    - Save it for services without free tiers
    - Practice Service Bus for a few days
    - Try Event Hubs briefly
    - Delete immediately after learning
2. **Resource naming convention:**
    
    ```
    rg-myapp-dev
    app-myapp-web-dev
    func-myapp-process-dev
    st-myapp-dev (storage accounts can't have dashes)
    kv-myapp-dev
    ```
    
3. **Use tags for tracking:**
    
    - Tag: Project = "AZ204Learning"
    - Tag: Environment = "Dev"
    - Tag: AutoDelete = "30days"
4. **Script everything:**
    
    - Learn Azure CLI commands
    - Learn ARM templates
    - Learn Bicep
    - Automate deployment
5. **Document your learning:**
    
    - Take screenshots
    - Write blog posts
    - Create GitHub repo with your code
    - Share your architecture diagrams

---

## 📚 **ADDITIONAL FREE RESOURCES**

- [ ] Microsoft Learn modules (free)
- [ ] Azure documentation
- [ ] Azure Architecture Center
- [ ] Azure free workshops
- [ ] Azure Friday videos (YouTube)
- [ ] John Savill's Azure videos (YouTube)
- [ ] Microsoft Virtual Training Days (free)

---

## 🎓 **CERTIFICATION PREP**

After implementing these services:

- [ ] Take Microsoft Learn assessment tests
- [ ] Practice with free AZ-204 practice questions
- [ ] Join Azure study groups
- [ ] Review Microsoft documentation
- [ ] Take practice exams
- [ ] Schedule AZ-204 exam

**Remember:** Hands-on experience is worth more than memorization for AZ-204!

---

## ⚠️ **IMPORTANT REMINDERS**

1. **Always delete resources you're not using**
2. **Set up cost alerts immediately**
3. **Never leave VMs running overnight**
4. **Use free tiers first, paid tiers only for quick practice**
5. **Review your bill weekly**
6. **The $200 credit expires after 30 days**
7. **12-month free services end after 12 months**
8. **Always-free services have usage limits**

**Good luck with your AZ-204 implementation! 🚀**