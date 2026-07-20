---
title: "11 - Develop solutions that use Blob storage - Manage the Azure Blob storage lifecycle"
tags: [azure, cloud, certification, AZ-204]
created: 2025-12-02
---
# 📘 Azure Learning Module: Manage the Azure Blob storage lifecycle
_A structured note for tracking progress and key takeaways from an Azure learning module._

---
## 📝 Summary
**What is this module about?**  
After completing this module, you'll be able to:
- Describe how each of the access tiers is optimized.
- Create and implement a lifecycle policy.
- Rehydrate blob data stored in an archive tier.

---
## 🔗 Links
**Useful resources and official docs:**  
- [Introduction - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/manage-azure-blob-storage-lifecycle/1-introduction)

---
## ✅ Module Assessment
**Key questions and answers from the module assessment:**
> [!question] Question 1 Which access tier is considered to be offline and can't be read or modified?
> 
> - Cool
> - Archive
> - Hot
> 
> > [!success]- Answer 
> > Archive

> [!question] Question 2 Which of the following storage account types supports lifecycle policies?
> 
> - General Purpose v1
> - General Purpose v2
> - FileStorage
> 
> > [!success]- Answer 
> > General Purpose v2

---
## 🧠 Flashcards
**Important terms and definitions for quick recall:**
Q: What are the two methods for rehydrating an archived blob in Azure Storage, and which one does Microsoft recommend?
A:
- **Copy to online tier** (recommended): Copy the archived blob to a new blob in hot or cool tier using Copy Blob operation
- **Change tier directly**: Use Set Blob Tier to change the archived blob's tier to hot or cool [Rehydrate blob data from the archive tier - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/manage-azure-blob-storage-lifecycle/5-rehydrate-blob-data)
---
**Q: What are the two rehydration priority options for archived blobs, and what are their expected completion times?**

**A:**
- **Standard priority**: Processed in order received; up to 15 hours
- **High priority**: Prioritized over standard requests; under 1 hour for objects under 10 GB
[Rehydrate blob data from the archive tier - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/manage-azure-blob-storage-lifecycle/5-rehydrate-blob-data)
Set via `x-ms-rehydrate-priority` header; monitor progress using Get Blob Properties.

---
## 🛠 Practice Exercises
**Hands-on tasks or labs:**
- Setup a storage policy for your applications logs.
- Setup a storage policy for your applications backups.

---
## 📚 Additional Notes
**Any extra insights, tips, or gotchas:**