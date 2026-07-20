---
title: "13 - Develop solutions that use Azure Cosmos DB - Explore Azure Cosmos DB"
tags: [azure, cloud, certification, AZ-204]
created: 2025-12-02
---
# 📘 Azure Learning Module: Explore Azure Cosmos DB
_A structured note for tracking progress and key takeaways from an Azure learning module._

---
## 📝 Summary
**What is this module about?**  
After completing this module, you'll be able to:
- Identify the key benefits provided by Azure Cosmos DB
- Describe the elements in an Azure Cosmos DB account and how they are organized
- Explain the different consistency levels and choose the correct one for your project
- Explore the APIs supported in Azure Cosmos DB and choose the appropriate API for your solution
- Describe how request units impact costs
- Create Azure Cosmos DB resources by using the Azure portal

---
## 🔗 Links
**Useful resources and official docs:**  

---
## ✅ Module Assessment
**Key questions and answers from the module assessment:**
> [!question] Question 1 Which of the following consistency levels offers the greatest throughput?
> 
> - Strong
> - Session
> - Eventual
> 
> > [!success]- Answer 
> > Eventual

> [!question] Question 2 What are request units (RUs) in Azure Cosmos DB?
> 
> - A unit of measurement used to express the cost of all database operations in Azure Cosmos DB.
> - A unit of time used to measure the duration of database operations.
> - A unit of storage used to measure the amount of data stored in Azure Cosmos DB.
> 
> > [!success]- Answer 
> > A unit of measurement used to express the cost of all database operations in Azure Cosmos DB.

---
## 🧠 Flashcards
**Important terms and definitions for quick recall:**
## Card 1: What is Azure Cosmos DB?

**Q: What type of database is Azure Cosmos DB, and what are its three primary design goals?**

**A:** A fully managed NoSQL database designed for: (1) low latency, (2) elastic scalability, and (3) global distribution with high availability

**Context:** Azure Cosmos DB fundamental definition - these three characteristics distinguish it from traditional databases

---

## Card 2: Multi-Master Replication Capability

**Q: What unique capability does Azure Cosmos DB's multi-master replication provide that traditional databases don't?**

**A:** Every region supports both writes AND reads (not just read replicas), enabling unlimited elastic write scalability globally

**Context:** Azure Cosmos DB's key differentiator - guarantees 99.999% availability and <10ms latency at 99th percentile across all regions

---
## Card 1: Hierarchy Structure

**Q: What are the four levels of the Azure Cosmos DB resource hierarchy, from top to bottom?**

**A:** (1) Account, (2) Database, (3) Container, (4) Items

**Context:** Azure Cosmos DB resource organization - Account contains databases, databases contain containers, containers store items. Container is the fundamental unit of scalability.

---

## Card 2: Partition Key Purpose

**Q: In Azure Cosmos DB, what is the primary purpose of the partition key you specify when creating a container?**

**A:** To help Azure Cosmos DB distribute data efficiently across partitions (physical servers)

**Context:** Azure Cosmos DB partitioning - the partition key value routes data to appropriate partitions for write, update, delete, and query operations. Also used in WHERE clauses for efficient retrieval.

---

## Card 3: Physical vs Logical Partition Limits

**Q: What are the storage and throughput limits for an Azure Cosmos DB physical partition?**

**A:** Up to 50 GB of storage and 10,000 Request Units (RU/s) per second

**Context:** Azure Cosmos DB partitioning architecture - logical partitions (20 GB limit) are abstracted on top of physical partitions. Containers scale by adding more partitions automatically.

---

## Card 1: Consistency Level Spectrum

**Q: What are the five consistency levels in Azure Cosmos DB, ordered from strongest to weakest?**

**A:** (1) Strong, (2) Bounded staleness, (3) Session, (4) Consistent prefix, (5) Eventual

**Context:** Azure Cosmos DB consistency spectrum - these levels are region-agnostic and guaranteed regardless of number of regions or write region configuration. Each offers different availability and performance tradeoffs.

---
## Card 1: Strong Consistency Guarantee

**Q: What guarantee does Azure Cosmos DB's Strong consistency level provide about read operations?**

**A:** Reads are guaranteed to return the most recent committed version of an item (linearizability guarantee)

**Context:** Strong consistency - clients never see uncommitted or partial writes. This is the strongest consistency level but has performance tradeoffs.

---

## Card 2: Bounded Staleness Configuration

**Q: In Azure Cosmos DB's Bounded Staleness consistency, what are the two ways you can configure the maximum staleness of data?**

**A:** (1) By number of versions (K updates) of an item, or (2) by time interval (T) that reads lag behind writes - whichever is reached first

**Context:** Bounded Staleness consistency - beneficial for single-region write accounts with 2+ regions. Writes are throttled if data lag exceeds configured bounds.

---

## Card 3: Session Consistency Guarantees

**Q: Within a single client session in Azure Cosmos DB, what two read guarantees does Session consistency provide?**

**A:** (1) Read-your-writes and (2) write-follows-reads guarantees

**Context:** Session consistency - assumes single writer session or shared session token for multiple writers. Most commonly used consistency level for single-region applications.

---

## Card 4: Eventual Consistency Characteristics

**Q: What guarantee does Azure Cosmos DB's Eventual consistency level provide about read ordering?**

**A:** No ordering guarantee - clients might read values older than ones they read before

**Context:** Eventual consistency - weakest form, but ideal for applications without ordering requirements (e.g., Retweets, Likes, non-threaded comments). Replicas converge when writes stop.

---
## Card 1: API for NoSQL Advantage

**Q: What is the primary advantage of Azure Cosmos DB's API for NoSQL compared to other Cosmos DB APIs?**

**A:** New features are first available on API for NoSQL accounts (best end-to-end experience with full control over interface, service, and SDK)

**Context:** Azure Cosmos DB API for NoSQL - stores data in document format and supports querying with SQL syntax. Native to Azure Cosmos DB.

---

## Card 2: Wire Protocol APIs

**Q: Which Azure Cosmos DB APIs implement the wire protocol of open-source database engines rather than using native code?**

**A:** API for MongoDB, PostgreSQL, Cassandra, Gremlin, and Table

**Context:** Azure Cosmos DB compatibility - these APIs are best for existing applications where you don't want to rewrite the data access layer, while still getting Cosmos DB benefits like automatic scaling and performance guarantees.

---
**Q: In Azure Cosmos DB, what does one Request Unit (RU) represent, and what is the cost of a point read for a 1-KB item?**

**A:** One RU represents the system resources (CPU, IOPS, memory) needed for database operations; a point read of a 1-KB item by ID and partition key costs exactly 1 RU

**Context:** Azure Cosmos DB pricing - all database operations (writes, reads, queries) are normalized and measured in RUs regardless of which API you use. RUs determine billing in both provisioned throughput and serverless modes.

---
## 🛠 Practice Exercises
**Objective:** Gain foundational experience with Azure Cosmos DB by creating an account, database, and container, and considering it as a potential backend for a real application.

- [ ] **1. Create Cosmos DB Resources via Azure Portal:**
    - [ ] **Goal:** Get familiar with the basic components of a Cosmos DB setup.
    - [ ] Follow the official Microsoft Learn exercise: [Create Azure Cosmos DB resources by using the Azure portal](https://learn.microsoft.com/en-us/training/modules/explore-azure-cosmos-db/8-create-cosmos-db-resources-portal). This will guide you through:
        - Creating a Cosmos DB account.
        - Choosing an API (e.g., API for NoSQL).
        - Creating a database and a container.
        - Understanding the importance of setting a partition key.
- [ ] **2. Evaluate Cosmos DB for the "Envelopes" App:**
    - [ ] **Goal:** Think critically about how to model your existing relational "Envelopes" application data in a NoSQL database like Cosmos DB.
    - [ ] **Data Modeling Exercise (Conceptual):**
        - How would you structure your "envelopes" and "transactions" in a single Cosmos DB container?
        - Would you embed transactions within each envelope document, or would you store them as separate items with a reference to the envelope?
        - What would you choose as the partition key to ensure even data distribution and efficient queries? (e.g., `userId`, `envelopeId`).
    - [ ] **API Selection:**
        - The note mentions "PostgreSQL?". This is a good thought. The **API for PostgreSQL** in Cosmos DB allows you to use a familiar relational API with the benefits of Cosmos DB's distributed architecture.
        - **Task:** Research the pros and cons of using the API for NoSQL vs. the API for PostgreSQL for the "Envelopes" app. Consider query flexibility, cost, and ease of migration from your current relational model.

---
## 📚 Additional Notes
**Any extra insights, tips, or gotchas:**