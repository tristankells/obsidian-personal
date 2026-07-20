A company implements a multi-region Azure Cosmos DB account.

You need to configure the default consistency level for the account. The consistency level must ensure that update operations made as a batch within a transaction are always visible together.

Which consistency level should you use?

Select only one answer.

Bounded Staleness

Session

**This answer is incorrect.**

Consistent Prefix

**This answer is correct.**

Eventual

This item tests the candidate’s knowledge of selecting the appropriate consistency level for operations in Azure Cosmos DB. The Consistent Prefix consistency level ensures that updates made as a batch within a transaction are returned consistently with the transaction in which they were committed. Write operations within a transaction of multiple documents are always visible together. The Bounded Staleness consistency level is used to manage the lag of data between any two regions based on an updated version of an item or the time intervals between read and write. The Session consistency level is used to ensure that within a single client session, reads are guaranteed to honor the read-your-writes and write-follows-reads guarantees. The Eventual consistency level is used when no ordering guarantee is required.

[Explore consistency levels](https://learn.microsoft.com/training/modules/explore-azure-cosmos-db/4-cosmos-db-consistency-levels-overview)