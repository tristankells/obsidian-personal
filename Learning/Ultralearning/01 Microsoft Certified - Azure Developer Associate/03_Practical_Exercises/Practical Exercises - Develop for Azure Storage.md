## [[10 - Develop solutions that use Blob storage - Explore Azure Blob storage]]

### Custom Practical Exercises

- [ ] **1. Blob Storage for Application Backups:**
    - [ ] **Goal:** Create a secure and cost-effective storage solution for application data backups.
    - [ ] Create a new Azure Storage Account.
    - [ ] Create a blob container named `envelopes-backups` and set its access level to "Private".
    - [ ] Manually upload a sample backup file (e.g., a `.zip` file) to the container.
- [ ] **2. Blob Storage for a CLI Tool:**
    - [ ] **Goal:** Set up a storage container to hold configuration files or scripts for a CLI tool.
    - [ ] In the same storage account, create a container named `cli-assets`.
    - [ ] Upload a sample configuration file (e.g., `config.yaml`) and a script file (e.g., `install.sh`).
- [ ] **3. Cost and Tier Investigation:**
    - [ ] **Goal:** Understand the cost implications of Azure Storage.
    - [ ] Research the Azure Storage pricing page to determine if there is a free tier.
    - [ ] Compare the costs of the Hot, Cool, and Archive access tiers and identify the best use case for each.
- [ ] **4. Accessing Blob Storage:**
    - [ ] **Goal:** Learn how to interact with stored blobs.
    - [ ] Use the Azure Portal to browse the files in both containers.
    - [ ] Install Azure Storage Explorer and connect it to your account to upload, download, and delete files.

## [[11 - Develop solutions that use Blob storage - Manage the Azure Blob storage lifecycle]]

### Custom Practical Exercises

- [ ] **1. Implement a Lifecycle Policy for Logs:**
    - [ ] **Goal:** Automatically move old log files to cheaper storage and then delete them.
    - [ ] Create a lifecycle policy that applies to your application's log container.
    - [ ] **Rule 1:** Move blobs to Cool storage after 30 days.
    - [ ] **Rule 2:** Move blobs from Cool to Archive storage after 90 days.
    - [ ] **Rule 3:** Delete blobs after 365 days.
- [ ] **2. Implement a Lifecycle Policy for Backups:**
    - [ ] **Goal:** Manage the lifecycle of application backups.
    - [ ] Create a lifecycle policy for your `envelopes-backups` container.
    - [ ] **Rule:** Move backups to Archive storage after 60 days to minimize costs.

## [[12 - Develop solutions that use Blob storage - Work with Azure Blob storage]]

### Azure Training Practical Exercises

- [ ] **1. Programmatic Blob Storage Management:**
    - [ ] **Goal:** Write a .NET console application to create a container and upload a blob.
    - [ ] Follow the official Microsoft Learn exercise: [Create Blob storage resources by using the .NET client library](https://learn.microsoft.com/en-us/training/modules/work-azure-blob-storage/4-develop-blob-storage-dotnet).

### Custom Practical Exercises

- [ ] **2. Manage Blob Metadata:**
    - [ ] **Goal:** Add, read, and update custom metadata for a blob.
    - [ ] Extend your .NET application to set metadata (e.g., `{"Author": "YourName", "Status": "InProgress"}`) on an uploaded blob.
    - [ ] Use the `GetPropertiesAsync` method to read the metadata.
    - [ ] Verify the metadata is visible in the Azure portal.

## [[13 - Develop solutions that use Azure Cosmos - DB Explore Azure Cosmos DB]]

### Azure Training Practical Exercises

- [ ] **1. Create Cosmos DB Resources via Azure Portal:**
    - [ ] **Goal:** Get familiar with the basic components of a Cosmos DB setup.
    - [ ] Follow the official Microsoft Learn exercise: [Create Azure Cosmos DB resources by using the Azure portal](https://learn.microsoft.com/en-us/training/modules/explore-azure-cosmos-db/8-create-cosmos-db-resources-portal).

### Custom Practical Exercises

- [ ] **2. Evaluate Cosmos DB for the "Envelopes" App:**
    - [ ] **Goal:** Conceptually model your relational "Envelopes" app data in a NoSQL database.
    - [ ] **Data Modeling:** How would you structure "envelopes" and "transactions" in a single container? Would you embed transactions or store them as separate items?
    - [ ] **Partition Key:** What would you choose as the partition key (e.g., `userId`, `envelopeId`) for even data distribution and efficient queries?
    - [ ] **API Selection:** Research the pros and cons of using the API for NoSQL vs. the API for PostgreSQL for the "Envelopes" app.

## [[14 - Develop solutions that use Azure Cosmos DB - Work with Azure Cosmos DB]]

### Azure Training Practical Exercises

- [ ] **1. Programmatic Resource Creation:**
    - [ ] **Goal:** Write a .NET application to create a Cosmos DB database and container.
    - [ ] Follow the official Microsoft Learn exercise: [Create resources in Azure Cosmos DB for NoSQL using .NET](https://learn.microsoft.com/en-us/training/modules/work-with-cosmos-db/3-exercise-work-cosmos-db-dotnet).

### Custom Practical Exercises

- [ ] **2. Implement a Change Feed Processor:**
    - [ ] **Goal:** Create a background process that reacts to data changes in a Cosmos DB container in real-time.
    - [ ] **Use Case:** When a user's name is updated in a "users" container, automatically update their name on all their "posts" in a different container.
    - [ ] **Implementation:** Create a C# console app using the Change Feed Processor library to monitor a container and write the delegate code to process changes.
    - [ ] **Alternative:** Create an Azure Function with a Cosmos DB Trigger to achieve the same result in a more "serverless" way.