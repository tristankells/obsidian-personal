---
title: "12 - Develop solutions that use Blob storage - Work with Azure Blob storage"
tags: [azure, cloud, certification, AZ-204]
created: 2025-12-02
---
# 📘 Azure Learning Module: Work with Azure Blob storage
_A structured note for tracking progress and key takeaways from an Azure learning module._

---
## 📝 Summary
**What is this module about?**  
After completing this module, you'll be able to:
- Create an application to create and manipulate data by using the Azure Storage client library for Blob storage.
- Manage container properties and metadata by using .NET and REST.

---
## 🔗 Links
**Useful resources and official docs:**  

---
## ✅ Module Assessment
**Key questions and answers from the module assessment:**
> [!question] Question 1 Which of the following standard HTTP headers are supported for both containers and blobs when setting properties by using REST?
> 
> - Last-Modified
> - Content-Length
> - Origin
> 
> > [!success]- Answer 
> > Last-Modified

> [!question] Question 2 Which of the following classes of the Azure Storage client library for .NET allows you to manipulate both Azure Storage containers and their blobs?
> 
> - BlobClient
> - BlobContainerClient
> - BlobUriBuilder
> 
> > [!success]- Answer 
> > BlobContainerClient

---
## 🧠 Flashcards
**Important terms and definitions for quick recall:**
**Q: What are the three main client object types in Azure Blob Storage SDK, and what level of resources does each interact with?**

**A:**
1. **BlobServiceClient**: Storage account level - retrieve/configure account properties, list/create/delete containers
2. **BlobContainerClient**: Container level - create/delete/configure containers, list/upload/delete blobs within them
3. **BlobClient**: Blob level - interact with specific individual blob resources
---
**Q: What authentication method is recommended in the Azure Storage SDK?**

**A:** **DefaultAzureCredential** is used to authenticate via Microsoft Entra security principal. 

---
- Azure Blob containers support what 2 types of data, in addition to the data they contain?
	- System Properties & User-Defined metadata.
https://learn.microsoft.com/en-us/training/modules/work-azure-blob-storage/5-manage-container-properties-metadata-dotnet
---
- What is the header prefix for adding metadata to to blob or container?
	- x-ms-meta-{nameOfMetadata}

https://learn.microsoft.com/en-us/training/modules/work-azure-blob-storage/6-set-retrieve-properties-metadata-rest

---
## 🛠 Practice Exercises
**Objective:** Learn to programmatically interact with Azure Blob Storage using the .NET client library to create resources and manage metadata.

- [ ] **1. Programmatic Blob Storage Management:**
    - [ ] **Goal:** Write a .NET console application to create a container and upload a blob.
    - [ ] Follow the official Microsoft Learn exercise: [Create Blob storage resources by using the .NET client library](https://learn.microsoft.com/en-us/training/modules/work-azure-blob-storage/4-develop-blob-storage-dotnet). This will guide you through:
        - Setting up a .NET project with the necessary Azure Storage SDK packages.
        - Authenticating to your Azure Storage account.
        - Creating a `BlobServiceClient` and a `BlobContainerClient`.
        - Programmatically creating a new container.
        - Uploading a local file as a blob to the new container.
- [ ] **2. Manage Blob Metadata:**
    - [ ] **Goal:** Add, read, and update custom metadata for a blob.
    - [ ] **Add Metadata:**
        - Extend your .NET application. After uploading a blob, get a `BlobClient` for that blob.
        - Create a `Dictionary<string, string>` with some custom metadata (e.g., `{"Author", "YourName"}, {"Status", "InProgress"}`).
        - Use the `SetMetadataAsync` method on the `BlobClient` to attach this metadata to the blob.
    - [ ] **Read Metadata:**
        - Use the `GetPropertiesAsync` method on the `BlobClient`.
        - Access the `Metadata` property from the result to read and display the custom metadata you just set.
    - [ ] **Verify in Portal:**
        - Navigate to the blob in the Azure portal and view its properties to confirm that your custom metadata is visible. This shows how metadata can be used to store additional, queryable information about your blobs.

---
## 📚 Additional Notes
**Any extra insights, tips, or gotchas:**