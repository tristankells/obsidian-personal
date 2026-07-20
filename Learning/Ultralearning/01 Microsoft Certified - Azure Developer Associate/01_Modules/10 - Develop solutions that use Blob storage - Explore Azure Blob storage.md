# Summary
# Links
# Module assessment
> [!question] Question 1 Which of the following types of blobs are used to store virtual hard drive files?
> 
> - Block blobs
> - Append blobs
> - Page blobs
> 
> > [!success]- Answer 
> > Page blobs

> [!question] Question 2 Which of the following types of storage accounts is recommended for most scenarios using Azure Storage?
> 
> - General-purpose v2
> - General-purpose v1
> - FileStorage
> 
> > [!success]- Answer 
> > General-purpose v2

> [!question] Question 3 What is the maximum size of data that a block blob in Azure Blob storage can store?
> 
> - 8-TB
> - Unlimited
> - 190.7-TiB
> 
> > [!success]- Answer 
> > 190.7-TiB

> [!question] Question 4 What are the two versions of client-side encryption available in the Azure Blob Storage and Queue Storage client libraries?
> 
> - Version 1 uses Cipher Block Chaining (CBC) mode with AES and Version 2 uses Galois/Counter Mode (GCM) mode with AES
> - Version 1 uses Advanced Encryption Standard (AES) and Version 2 uses Federal Information Processing Standards (FIPS)
> - Version 1 uses Galois/Counter Mode (GCM) mode with AES and Version 2 uses Cipher Block Chaining (CBC) mode with AES
> 
> > [!success]- Answer 
> > Version 1 uses Cipher Block Chaining (CBC) mode with AES and Version 2 uses Galois/Counter Mode (GCM) mode with AES
# Notes
# Flashcards
- Under which conditions is it optimal to use a premium Block Blob storage account, instead of standard storage account?
	- Recommended for scenarios with **high transaction rates** or that **use smaller objects** or require consistently **low storage latency**.
	- [Explore Azure Blob storage - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/explore-azure-blob-storage/2-blob-storage-overview)
- What are the three kinds of premium storage accounts?
	- Premium block blobs, Premium file shares and Premium page blobs
	- [Explore Azure Blob storage - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/explore-azure-blob-storage/2-blob-storage-overview)
- What are the three types of Blobs?
	- Block (audio & video), append (logs) and page (virtual hard disk / VDH)
	- [Discover Azure Blob storage resource types - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/explore-azure-blob-storage/3-blob-storage-resources)
- What is the use case for Version 1 over version 2 client side encryption for storage accounts?
	- No support for Tablet Storage
- The Azure Blob Storage client libraries support client side encryption. Version 2 uses ___ mode, Version 1 uses ___ mode with AES.
	- Galois/Counter Mode (GCM)
	- Cipher Block Chaining (CBC) 
# 🛠 Practice Exercises
**Objective:** Understand the fundamentals of Azure Blob Storage by creating and managing storage for different use cases.

- [ ] **1. Blob Storage for Application Backups:**
    - [ ] **Goal:** Create a secure and cost-effective storage solution for application data backups.
    - [ ] Create a new Azure Storage Account.
    - [ ] Inside the storage account, create a blob container named `envelopes-backups`.
    - [ ] Set the container's access level to "Private" to ensure the backups are not publicly accessible.
    - [ ] Manually upload a sample backup file (e.g., a `.zip` or `.json` file) to the container to simulate a backup process.
- [ ] **2. Blob Storage for a Command-Line Interface (CLI) Tool:**
    - [ ] **Goal:** Set up a storage container to hold configuration files or scripts for a CLI tool.
    - [ ] In the same storage account, create a second container named `cli-assets`.
    - [ ] Upload a sample configuration file (e.g., `config.yaml`) and a script file (e.g., `install.sh`) to this container.
    - [ ] This simulates a common pattern where a central repository is needed for assets used by distributed tools.
- [ ] **3. Cost and Tier Investigation:**
    - [ ] **Goal:** Understand the cost implications of Azure Storage.
    - [ ] Research the Azure Storage pricing page.
    - [ ] Determine if there is a free tier or a free monthly allowance for blob storage.
    - [ ] Compare the costs of the different access tiers (Hot, Cool, Archive) and identify the best use case for each. For example, the `envelopes-backups` container might be a good candidate for the "Cool" tier if backups are accessed infrequently.
- [ ] **4. Accessing Blob Storage:**
    - [ ] **Goal:** Learn how to interact with the stored blobs.
    - [ ] Use the Azure Portal to browse the files in both containers.
    - [ ] Install Azure Storage Explorer, connect it to your Azure account, and use it to upload, download, and delete files from your containers. This provides a more powerful desktop experience for managing storage. 