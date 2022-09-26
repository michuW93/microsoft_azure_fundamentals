microsoft_azure_developer-AZ-204-

Tutorial based on David Tucker videos

# Relationed DB vs NoSQL DB
Relational Database: Fixed schema, Table based structure, Vertical scaling and manual sharding for scalability, Provides ACID guarantees (atomicity, consistency, isolation, durability), data normalization

NoSQL Databases: Fluid schema, Multiple structures (key-value, graph, document, wide-columns), Horizontal scaling and data partitioning for scalability, Provides BASE(basically available, soft state, eventual consistency) sementics, Non-normalized data

From Microsoft, CosmosDB documentation: If your transactional volumes are reaching extreme levels, such as many thousands of transactions per second, you should consider a distrubuted NoSQL database

# Capabilities of CosmosDB
Azure CosmosDB is Microsoft's globally distrubuted, multi-model database service.

* Provides extrmaly low latency (single digit milisecond)
* Provides SLA for throughput, latency, availability and consistency
* support multi-region replication at any point
* provides five-nines of high-availability for both reads and writes
* enables elastic scalability
* priving is for the thtoughput you provision
* supports multiple consistency options

Additional CosmosDB features:
* integrated analytics
* region support
* schema-agnostic
* atumatic indexing
* supports multiple SDK's

Cosmos DB Organization:
* Cosmos DB account (SQL API) - it must be created first, in your <b>Cosmos DB account</b> there will be Databases. In databases there will be <b>containers</b> (similar to tables in relational DB). In tables will be <b>items</b> which are similar to rows in table.

Supported Cosmos DB API's:
* SQL - if you want to leverage a SQL-like language, you want to store data as JSON documents and in general if no other use cases fit, you don't know what to take then choose SQL API
* Cassandra - if you want Cassandra Query Language to query data (CQL) or you want to be able to leverage existsing Cassandra tools, you want to store data in a wide-column format (two dimentsional key-value store)
* MongoDB - if you are familiar with MongiDB API to query data, or if you have existsing MongoDB and want to migrate to cloud or you want to store data as JSON documents
* Gremlin - graph database, so if you want to store graph relationships
* Azure table - if you have expirience with Azure Table Storage

Database Entity:
* SQL - Database
* Cassandra - keyspace
* MongoDB - database
* Gremlin - database
* Azure Table -n/a, it will create anything based on first table which is created

Container entity:
* SQL - container
* Cassandra - Table
* MongoDB - collection
* Gremlin - Graph
* Azure Table - table

How to create Cosmos DB Container:
First you need to create account and choose API (az cosmosdb create --name accName --resource-group) <br/>
then create sql database (az cosmosdb sql database create --account-name accountName --name samleDB) <br/>
then create a sql database container (az cosmosdb sql container create --resource-group --account-name --database-name --name --partition-key-path)

Selecting an SDK:
* SQL API - utilize latest Cosmos DB SDK
* MongoDB, Cassandra, Gremlin use current SDK's for thoses API's
* Azure Table API leverage the currecnt Table Storage SDK

Traditional Database scaling: vertically - upgrade CPU, memory etc. or Horizontal scaling - add new machine. <br/>
to scale Cosmos DB we need to request unit. RU - a request unit encapsulates many of the resources needed for the database into a single unit. As a beseline, one RU is equal to a 1kb item read operation from a CosmosDB container. Resources which are encapsulated in RU's are processing power(CPU), memory and IOPS (input/output operations per second)

Managing CosmosDB throughput:
* provisioned - you set a specific amount of RU. It's ideal for always-on production implementation, can be configured at the database or container, it's evenly distributed to partitions, requires 10RU's per GB of storage. Once RU's are consumed for a partition, future requests will be rate limited. By default, it requires a manual scaling approach to acquire more RU's. There is also autoscaling(provisioned) - with provisioned throughput, you can specify a maximum RU throughput amount, and Cosmos DB will ensure that your data is available up to the thoughput amount. The minumum throughput is calculated as 10% of the maximum.
* serverless - pay only for the request units consumed and storage used, ideal for off and on workloads such as development workloads. It's currently in preview. Max is 5000 RU, requires a new account type, it supports only SQL API

Best practices:
* use a partition strategy to evenly spread throughput on partitions
* provision thoughput at the container for predictable performance
* use the serverless account type for development workloads
* understand the link between consistency types and the amount of RU's consumed


# Data consistency levels
Distributed databases that rely on replication for high availability, low latency, or both, must make a fundamental tradeoff between the read consistency, availability, latency and thoughput

Consistency levels:
* eventual - someone in Europe do some changes in db, someone in Asia is reading row from this table. There is a big chance that guy in Asia won't have this last update from guy in Europe. It will be replicated later but if someone write into db in different region and someone else in nearly the same time read it from other region won't have latest update. The lowest latency, higher thougput, higher availability. Provides no guarantees for order
* consistent prefix - guarantees that updates are returned in order
* session - guarantees that a client session will read its own writes
* bounded staleness - guarantees that a read has a max lag (either version or time)
* strong - the highest latency, lower thoughput, lower availability. Strong consistency guarantees that reads get the mose recent version of an item. Traditional dbs have it. 

Consistency levels for SQL API's:
* account default - you can set consistency level for account, every operation will follow this consistency level
* request-specific level - diff consistency level for request

Gremlin and Azure Table API's, Cosmos db uses account default consistency level. <br/>
For Cassandra writes, the account default consistency level is used but for cassandra reads, the client consistency is mapped to a Cosmos DB level. <br/>
For MongoDB the write concern uses the account default consistency level, the read concern will use a mapping to a Cosmos DB level

Thoughput considerations - both strong and bounded staleness reads will consume twice the normal amount of request units for a request, as Cosmos DB will need to query two replicas to meet the criteria of the consistency level.

Data partitioning:
* logical partition - is a set of items within a container that share the same partiion key. A container can have as many logical partitions as it needs, but each partition is limited to 20GB of storage. Logical partitions are managed by Cosmos DB but their use is governed by your partition key strategy.
* physical partition - a container is scaled by distributing data and thoughput across physical partitions. Internally, one or more logical partitions are mapped to a single physical partition. They are entirely managed by Azure Cosmos DB.
* replica set - a physical partition contains multiple replicas of the data, known as a replica set. By having this data replicated, you enable your storage to be durable and fault tolerant. These replica sets are managed by Cosmos DB.
* partition key - serves as the means of routing your request to the correct partition. Made up of both the key and the value of the defined partition key. Should be the value that does not change for the item. Should also have many different values represented in the container. Azure Cosmos DB uses hash-based partitioning to spread logical partitions across physical partitions. Azure Cosmos DB hashes the partition key value of an item. Then Cosmos DB allocates the key space of partition key hashes evenly across the physical partitions.

Strategy considerations:
* throughput is distributed evenly across all of your physical partitions
* multi-item transactions require triggers or stored procedures
* you will want to minimize cross-partition queries for heavier workloads
* decide upon a partition key strategy before creating your container

<b>Partition key can't change so for example email of employee as partition key is wrong decision because mail can change</b>

Hot partition

Physical partition include logical partitions.
