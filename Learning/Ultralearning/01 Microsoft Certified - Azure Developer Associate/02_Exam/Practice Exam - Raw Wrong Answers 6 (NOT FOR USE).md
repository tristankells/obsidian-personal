Question 13 of 50

You have an application that writes data to Azure Cosmos DB.

The application must offer monotonic reads, with no guarantee that the value read is the last value written.

You need to configure the consistency level.

Which consistency level should you use?

Select only one answer.

strong

bounded staleness

**This answer is incorrect.**

session

**This answer is correct.**

eventual

This item tests the candidate's knowledge of Azure Cosmos DB consistency levels.

Session consistency offers all the guarantees listed. It provides write latencies, availability, and read throughput comparable to that of eventual consistency. It also provides the consistency guarantees that suit the needs of applications written to operate in the context of a user. Strong consistency has reads guaranteed to return the most recent committed version of an item. A client never sees an uncommitted or partial write. Users are guaranteed to read the latest committed write. It has the highest write latency and lowest read throughput of all consistency levels. In bounded staleness consistency, the reads are guaranteed to honor the consistent-prefix guarantee. It should be used when there is a need for low write latencies but require a total global order guarantee. In eventual consistency, there is no ordering guarantee for reads. In the absence of any further writes, the replicas eventually converge. It is the weakest form of consistency because a client may read values that are older than the ones it had read before. Eventual consistency is ideal when the application does not require any ordering guarantees.

[AZ-204: Develop solutions that use Azure Cosmos DB - Training | Microsoft Learn](https://learn.microsoft.com/training/paths/az-204-develop-solutions-that-use-azure-cosmos-db/)


Question 15 of 50

You plan to create a key namespace hierarchy in Azure App Configuration.

You need to separate individual key names.

Which character should you use?

Select only one answer.

:

**This answer is correct.**

*

,

**This answer is incorrect.**

\

This item tests the candidate’s knowledge of configuring key namespace hierarchy of App Configuration, which is part of implementing secure cloud solutions.

The colon character (:) is used to separate names of individual keys when creating a namespace hierarchy in Azure App Configuration. The asterisk character (*) is one of reserved characters in Azure App Configuration, so it cannot be used to separate names of individual keys when creating a namespace hierarchy in Azure App Configuration. The comma character (,) is one of reserved characters in Azure App Configuration, so it cannot be used to separate names of individual keys when creating a namespace hierarchy in Azure App Configuration. The backslash character () is one of reserved characters in Azure App Configuration, so it cannot be used to separate names of individual keys when creating a namespace hierarchy in Azure App Configuration.

[Create paired keys and values - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/implement-azure-app-configuration/3-keys-values)