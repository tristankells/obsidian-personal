---

tags: [azure, cloud, certification, AZ-204]
created: 2025-12-08
---
# 📝 Summary
**What is this module about?**  
After completing this module, you'll be able to:
- Identify the three types of shared access signatures
- Explain when to implement shared access signatures
- Create a stored access policy
---
# 🔗 Links
**Useful resources and official docs:**  
- [Discover Microsoft Graph - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/microsoft-graph/2-microsoft-graph-overview)
---
# ✅ Module Assessment
**Key questions and answers from the module assessment:**  

> [!question] Question 1 Which of the following types of shared access signatures (SAS) applies to Blob storage only?
> 
> - Account SAS
> - Service SAS
> - User delegation SAS
> 
> > [!success]- Answer 
> > User delegation SAS

> [!question] Question 2 Which of the following best practices provides the most flexible and secure way to use a service shared access signature (SAS)?
> 
> - Associate SAS tokens with a stored access policy.
> - Always use HTTPS
> - Implement a user delegation SAS
> 
> > [!success]- Answer 
> > Associate SAS tokens with a stored access policy.

---
# 🧠 Flashcards
**Important terms and definitions for quick recall:**  
## Card 1: Recommended SAS Type

**Q: According to Microsoft security best practices, which of the three Shared Access Signature (SAS) types is **recommended** because it is secured using **Microsoft Entra credentials**?**

**A:** User delegation SAS

**Context:** Using Microsoft Entra credentials makes the User delegation SAS more secure than the Service SAS or Account SAS, which are both secured using the storage account key.

---

## Card 2: SAS Scope Distinction

**Q: What is the primary difference in **scope** between an **Account SAS** and a **Service SAS**?**

**A:**

- **Service SAS** delegates access to resources within **one specific service** (e.g., just Blob storage).
    
- **Account SAS** delegates access to resources across **one or more storage services** (e.g., Blob, Queue, and Table storage simultaneously).
    

**Context:** Both Service SAS and Account SAS are secured using the storage account key, but the Account SAS provides a much broader level of access.

---

## Card 3: Alternative to SAS (Risk Mitigation)

**Q: If the risk of compromising a Shared Access Signature (SAS) is deemed unacceptable for an application, what architecture does Microsoft recommend to manage user access to storage instead?**

**A:** Create a **middle-tier service** to manage users and their access to storage resources.

---
## Card 4: Types of SAS

**Q: What are the three distinct types of Shared Access Signatures (SAS) supported by Azure Storage?**

**A:**

1. **User delegation SAS**
    
2. **Service SAS**
    
3. **Account SAS**
    

**Context:** The security mechanism and scope of delegated access differ for each type (Microsoft Entra credentials for User delegation; Storage Account Key for Service and Account).

---

## Card 5: Lightweight SAS Design Pattern

**Q: In a high-volume storage scenario, what is the key advantage of the design pattern where a lightweight service generates a SAS for the client?**

**A:** It mitigates the need for routing **all data** through the lightweight service, allowing the client to access storage resources **directly** with the defined SAS permissions.

**Context:** This design pattern is typically used when clients read and write their own data, and creating a scalable front-end proxy service to handle large amounts of data would be expensive or difficult.

---

## Card 6: SAS Requirement for Inter-Object Copy

**Q: In Azure Storage copy operations, under what specific condition must a Shared Access Signature (SAS) be used to authorize access to the **source** object, even if the source and destination objects reside within the **same** storage account?**

**A:** When the copy operation is between **different object types** (a **blob to a file**, or a **file to a blob**).

**Context:** SAS is required for the source when copying between different accounts, but this rule applies _even_ in the same account when the source and destination are fundamentally different storage types.

---

## Card 7: Stored Access Policy Control

**Q: What is the primary purpose of a **Stored Access Policy** in relation to a Service-level Shared Access Signature (SAS)?**

**A:** To provide an **extra level of server-side control** by grouping SAS tokens and allowing you to **change the start time, expiry time, or permissions**, or to **revoke** the signature after it has been issued.

**Context:** Stored access policies apply only to **Service SAS** and provide a central management point for permissions that would otherwise be permanently bound to the SAS token when generated.

---

## Card 8: Parameter Restriction for Stored Access Policies

**Q: When defining a Shared Access Signature (SAS) and linking it to a Stored Access Policy, what is the key rule regarding the specification of parameters like start time and expiry time?**

**A:** You **cannot specify a given parameter** (e.g., expiry time) on **both** the SAS token URI **and** the Stored Access Policy.

**Context:** The parameters must be specified entirely on the URI, entirely on the policy, or split between them, but never duplicated for a single parameter.

---
# 🛠 Practice Exercises
**Objective:** Learn how to generate different types of Shared Access Signatures (SAS) and manage them effectively using stored access policies.

- [ ] **1. Generate a Service SAS:**
    - [ ] **Goal:** Create a SAS token that grants temporary read-only access to a specific blob.
    - [ ] Create a storage account and a blob container. Upload a sample file (e.g., `test.txt`).
    - [ ] Using the Azure Portal or Azure Storage Explorer, generate a Service SAS for the `test.txt` blob with only "Read" permissions and a short expiry time (e.g., 1 hour).
    - [ ] Construct the full URL with the SAS token and try to access the blob in a private browser window. You should be able to view it.
    - [ ] Try to perform a write operation (which should fail).
- [ ] **2. Generate a User Delegation SAS:**
    - [ ] **Goal:** Create a more secure SAS token using Microsoft Entra ID credentials.
    - [ ] Assign your user account the "Storage Blob Data Contributor" role on the storage account.
    - [ ] Use Azure CLI or PowerShell to log in with your Entra ID credentials.
    - [ ] Request a user delegation key.
    - [ ] Use this key to create a user delegation SAS for a container with "Write" and "List" permissions.
    - [ ] Use a tool like `azcopy` with the generated SAS to upload a file to the container, proving the write access works.
- [ ] **3. Implement and Use a Stored Access Policy:**
    - [ ] **Goal:** Centrally manage and revoke access for a group of SAS tokens.
    - [ ] In your blob container, define a stored access policy named `read-policy` that grants read access for the next 24 hours.
    - [ ] Generate a new Service SAS for the container, but instead of defining the permissions and expiry time in the SAS itself, link it to the `read-policy`.
    - [ ] Verify that the SAS token works as expected.
    - [ ] **Revoke the SAS:** Go back to the stored access policy and either delete it or clear its expiry date.
    - [ ] Immediately try to use the SAS token again. It should now fail, demonstrating the power of centralized revocation.
---
# 📚 Additional Notes
**Any extra insights, tips, or gotchas:** 