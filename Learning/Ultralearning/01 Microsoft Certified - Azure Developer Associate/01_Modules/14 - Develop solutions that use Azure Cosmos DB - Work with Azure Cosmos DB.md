---
title: "14 - Develop solutions that use Azure Cosmos DB - Work with Azure Cosmos DB"
tags: [azure, cloud, certification, AZ-204]
created: 2025-12-02
---
# 📘 Azure Learning Module: Work with Azure Cosmos DB
_A structured note for tracking progress and key takeaways from an Azure learning module._

---
## 📝 Summary
**What is this module about?**  
After completing this module, you'll be able to:
- Identify classes and methods used to create resources.
- Create resources in Azure Cosmos DB for NoSQL using .NET.
- Write stored procedures, triggers, and user-defined functions by using JavaScript.

---
## 🔗 Links
**Useful resources and official docs:**  
[Work with Azure Cosmos DB - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/work-with-cosmos-db/)

---
## ✅ Module Assessment
**Key questions and answers from the module assessment:**
> [!question] Question 1 What is the purpose of the context object in a stored procedure in Azure Cosmos DB?
> 
> - It provides access to the database schema and metadata.
> - It allows for the creation of new collections within the database.
> - It provides access to all operations that can be performed in Azure Cosmos DB, and access to the request and response objects.
> 
> > [!success]- 
> > Answer It provides access to all operations that can be performed in Azure Cosmos DB, and access to the request and response objects.

> [!question] Question 2 What is the role of pretriggers in Azure Cosmos DB?
> 
> - Pretriggers are automatically executed for each database operation.
> - Pretriggers are executed before modifying a database item and must be specified for each database operation where you want them to execute.
> - Pretriggers are used to execute operations after modifying a database item.
> 
> > [!success]- Answer 
> > Pretriggers are executed before modifying a database item and must be specified for each database operation where you want them to execute.

> [!question] Question 3 What is the purpose of the lease container in the Azure Cosmos DB change feed processor?
> 
> - It stores the data from which the change feed is generated.
> - It processes the change feed across multiple workers.
> - It acts as a state storage and coordinates processing the change feed across multiple workers.
> 
> > [!success]- Answer 
> > It acts as a state storage and coordinates processing the change feed across multiple workers.

---
## 🧠 Flashcards
**Important terms and definitions for quick recall:**
## Card 1: Reading an Item with .NET SDK v3

**Q: In Azure Cosmos DB .NET SDK v3, what two parameters are required by the Container.ReadItemAsync method to read an item?**

**A:** (1) The item's id property, and (2) a PartitionKey value

**Context:** Azure Cosmos DB .NET SDK v3 read operation - method also requires a type parameter to serialize the item to (e.g., `ReadItemAsync<SalesOrder>`). This is a point read operation that costs 1 RU for a 1-KB item.

## Card 1: Context Object Access

**Q: In Azure Cosmos DB stored procedures, what does the context object provide access to?**

**A:** All operations that can be performed in Azure Cosmos DB, plus access to the request and response objects

**Context:** Azure Cosmos DB stored procedures (JavaScript) - obtained via `getContext()`. Use `context.getCollection()` for container operations and `context.getResponse()` to set response body.

---

## Card 2: Bounded Execution Return Value

**Q: In Azure Cosmos DB stored procedures, what does the Boolean return value from collection functions (like createDocument) indicate?**

**A:** Whether the operation completed or not (within the limited execution time)

**Context:** Azure Cosmos DB bounded execution - all operations must complete within a limited time on the server. If false, the operation didn't complete within time constraints.

---

## Card 3: Transaction Continuation Model

**Q: How does Azure Cosmos DB's transaction continuation model allow stored procedures to handle workloads that exceed time limits?**

**A:** The stored procedure returns a continuation value (like a bookmark or progress marker) before timing out. The application then calls the stored procedure again with this value, allowing it to resume from where it left off rather than starting over.

**Context:** Azure Cosmos DB stored procedure transactions - think of it like processing items in batches: if you need to update 10,000 items but can only do 1,000 before timing out, you return "1000" as the continuation. The next call starts at item 1001. The continuation value can be any format (number, string, object) that helps track your progress. This pattern repeats until the entire workload finishes.

---
## Card 1: Pretrigger vs Post-trigger Timing

**Q: In Azure Cosmos DB, when are pretriggers executed versus post-triggers?**

**A:** Pretriggers are executed before modifying a database item; post-triggers are executed after modifying a database item

**Context:** Azure Cosmos DB triggers - triggers are NOT automatically executed; they must be specified for each database operation. Both types must be registered using the Azure Cosmos DB SDKs.

---

## Card 2: Post-trigger Transactional Behavior

**Q: What happens to the underlying item modification if a post-trigger throws an exception in Azure Cosmos DB?**

**A:** The whole transaction fails, anything committed is rolled back, and an exception is returned

**Context:** Azure Cosmos DB post-trigger transactions - post-triggers run as part of the same transaction as the underlying item modification. This ensures atomicity: either both the item modification and post-trigger succeed, or both fail together.

---
## Card 1: Change Feed Operations Coverage

**Q: What types of operations does Azure Cosmos DB change feed currently capture?**

**A:** Inserts and updates only (delete operations are not logged)

**Context:** Azure Cosmos DB change feed - for deletes, use a workaround: add a "deleted" attribute set to "true" with a TTL value, so the item appears in change feed as an update before being automatically deleted.

---

## Card 2: Push Model vs Pull Model Recommendation

**Q: For Azure Cosmos DB change feed, which model (push or pull) is recommended and why?**

**A:** Push model is recommended because you don't need to worry about polling the change feed, storing state for the last processed change, or handling complexity

**Context:** Azure Cosmos DB change feed models - push model (change feed processor or Azure Functions) handles complexity internally. Pull model gives extra low-level control for scenarios like reading specific partition keys or one-time data migration.

---

## Card 3: Change Feed Processor Four Components

**Q: What are the four main components required to implement Azure Cosmos DB's change feed processor?**

**A:** (1) Monitored container (source of changes), (2) Lease container (state storage), (3) Compute instance (hosts processor), (4) Delegate (code to process changes)

**Context:** Change feed processor (.NET V3 and Java V4 SDKs) - monitored container generates the change feed, lease container coordinates across multiple workers, compute instance has unique identifier, delegate defines what to do with each batch of changes.

---
## 🛠 Practice Exercises
**Objective:** Learn how to programmatically manage Azure Cosmos DB resources using the .NET SDK and explore server-side logic with the change feed.

- [ ] **1. Programmatic Resource Creation:**
    - [ ] **Goal:** Write a .NET application to create a Cosmos DB database and container.
    - [ ] Follow the official Microsoft Learn exercise: [Create resources in Azure Cosmos DB for NoSQL using .NET](https://learn.microsoft.com/en-us/training/modules/work-with-cosmos-db/3-exercise-work-cosmos-db-dotnet). This will teach you how to:
        - Use the `CosmosClient` to interact with your Cosmos DB account.
        - Create a new database with `CreateDatabaseIfNotExistsAsync`.
        - Create a new container with `CreateContainerIfNotExistsAsync`, specifying the partition key path.
- [ ] **2. Implement a Change Feed Processor:**
    - [ ] **Goal:** Create a background process that reacts to data changes in a Cosmos DB container in real-time.
    - [ ] **Use Case:** Imagine you want to de-normalize data. When a user updates their name in a "users" container, you want to automatically update their name on all the "posts" they have created in a different container.
    - [ ] **Implementation:**
        - Create a C# console application that uses the Change Feed Processor library.
        - Configure it to monitor your primary container (the "monitored container").
        - Create a second container to act as the "lease container" to track the state of the change feed processor.
        - Write the delegate code that will be executed when changes are detected. This code will receive a batch of changed documents.
        - For each change, your code should trigger the logic to update the related documents in the other container.
    - [ ] **Alternative with Azure Functions:**
        - Instead of a console app, create an Azure Function with a **Cosmos DB Trigger**.
        - Configure the trigger to point to your monitored container and lease container.
        - The body of the function is your delegate code. This is often a simpler and more "serverless" way to process the change feed.

---
## 📚 Additional Notes
**Any extra insights, tips, or gotchas:**