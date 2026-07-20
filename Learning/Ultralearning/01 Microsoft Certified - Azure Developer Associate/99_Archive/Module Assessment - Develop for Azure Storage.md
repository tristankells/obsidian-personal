
## [[10 - Develop solutions that use Blob storage - Explore Azure Blob storage]]

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

## [[11 - Develop solutions that use Blob storage - Manage the Azure Blob storage lifecycle]]

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

## [[12 - Develop solutions that use Blob storage - Work with Azure Blob storage]]

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

## [[13 - Develop solutions that use Azure Cosmos - DB Explore Azure Cosmos DB]]

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

## [[14 - Develop solutions that use Azure Cosmos DB - Work with Azure Cosmos DB]]

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
