microsoft_azure_developer-AZ-204-

Tutorial based on David Tucker and Thomas Claudius Huber videos

# Relationed DB vs NoSQL DB
Relational Database: Fixed schema, Table based structure, Vertical scaling and manual sharding for scalability, Provides ACID guarantees (atomicity, consistency, isolation, durability), data normalization

NoSQL Databases: Fluid schema, Multiple structures (key-value, graph, document, wide-columns), Horizontal scaling and data partitioning for scalability, Provides BASE(basically available, soft state, eventual consistency) sementics, Non-normalized data

From Microsoft, CosmosDB documentation: If your transactional volumes are reaching extreme levels, such as many thousands of transactions per second, you should consider a distrubuted NoSQL database

# Capabilities of CosmosDB
Azure CosmosDB is Microsoft's globally distributed, multi-model database service.

* Provides extremaly low latency (single digit milisecond)
* Provides SLA for throughput, latency, availability and consistency
* support multi-region replication at any point
* provides five-nines of high-availability for both reads and writes
* enables elastic scalability
* pricing is for the throughput you provision
* supports multiple consistency options

Additional CosmosDB features:
* integrated analytics
* region support
* schema-agnostic
* automatic indexing
* supports multiple SDK's

Cosmos DB Organization:
* Cosmos DB account (SQL API) - it must be created first, in your <b>Cosmos DB account</b> there will be Databases. In databases there will be <b>containers</b> (similar to tables in relational DB). In tables will be <b>items</b> which are similar to rows in table.

Supported Cosmos DB API's:
* SQL - if you want to leverage a SQL-like language, you want to store data as JSON documents and in general if no other use cases fit, you don't know what to take then choose SQL API
* Cassandra - if you want Cassandra Query Language to query data (CQL) or you want to be able to leverage existsing Cassandra tools, you want to store data in a wide-column format (two dimentsional key-value store)
* MongoDB - if you are familiar with MongoDB API to query data, or if you have existsing MongoDB and want to migrate to cloud or you want to store data as JSON documents
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
* Azure Table API leverage the current Table Storage SDK

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
* logical partition - is a set of items within a container that share the same partiton key. A container can have as many logical partitions as it needs, but each partition is limited to 20GB of storage. Logical partitions are managed by Cosmos DB but their use is governed by your partition key strategy.
* physical partition - a container is scaled by distributing data and thoughput across physical partitions. Internally, one or more logical partitions are mapped to a single physical partition. They are entirely managed by Azure Cosmos DB.
* replica set - a physical partition contains multiple replicas of the data, known as a replica set. By having this data replicated, you enable your storage to be durable and fault tolerant. These replica sets are managed by Cosmos DB.
* partition key - serves as the means of routing your request to the correct partition. Made up of both the key and the value of the defined partition key. Should be the value that does not change for the item. Should also have many different values represented in the container. Azure Cosmos DB uses hash-based partitioning to spread logical partitions across physical partitions. Azure Cosmos DB hashes the partition key value of an item. Then Cosmos DB allocates the key space of partition key hashes evenly across the physical partitions.

Strategy considerations:
* throughput is distributed evenly across all of your physical partitions
* multi-item transactions require triggers or stored procedures
* you will want to minimize cross-partition queries for heavier workloads
* decide upon a partition key strategy before creating your container

<b>Partition key can't change so for example email of employee as partition key is wrong decision because mail can change</b>

Hot partition - by Erick Ramirez:
There's no hard rule for it but it's generally just a partition (or a subset of partitions) which are accessed more frequently than other partitions in the table.

We generally refer to hot partitions in the context of unbalanced loads in the cluster such that some nodes are accessed significantly more compared to other nodes.

Think of a situation where an application keyspace has a replication factor of 3 in a data centre which has 50 nodes. In a table of users where one of the users is a service account that is used to connect multiple times a day for monitoring.

The 3 replicas out of the 50 nodes which hold this service account will have a significantly higher utilisation compared to the rest of the nodes because it is a hot partition.

Physical partition include logical partitions.

# server side programming with CosmosDB
Server-side capabilities - Cosmos DB provides a robust approach for executing code in response to actions taken on the data stored in Cosmos DB. While in some cases these mirror traditional database constructs, they are fundamentally different in implmentation and have unique limitations.

Cosmos DB server-side concepts:
* stored procedures - executed within the database engine, supports only Javascript, can be created and managed via the portal and via the SDK. Executes on a single partition and it only has access to that partition. Partition key must be provided with the execution request. Supports a transaction model as all statements will be removed if it fails
* triggers - executed within the database engine, supports only Javascript, can be created and managed via the portal and via the SDK. They can be executed either before (pre) or after (post) data is written. Pre triggers can handle data transformation and validation, post triggers can handle aggregation and change notifications. Triggers are not guaranteed to execute as they have to be specified in a request. Errors in either the PRE or POST trigger will result in data being rolled back.
* user defined functions (UDF's) - executed within the database engine, supports only Javascript, can be created and managed via the portal and via the SDK. Enables you to define a custom function that can be leveraged in a query. Enables encapsulation of common logic in query conditions. 
* change feed - while all other server-side programming approaches enable execution on the Cosmos DB engine, change feed processing enables you to react to data changes using server-side code outside of the Cosmos DB engine. Enables you to be notified for any insert and update on your data. Deletes are not directly supported but you can leverage a soft-delete flag. A change will appear exactly once in the change feed. Reading data from the database will consume thoughput. Partition updates will be in order but between partitions there is no guarantee. Is not supported for the Azure Table API

Change feed approaches: Azure Functions, change feed processor

# Properties and metadata.
Blob Container has System properties. One of system properties is <b>ETag</b> (entity tag), <b>lastModified<b/>. <br/>
Blob also has System properties with ETag, LastModified, Content-Type, Content-Length, x-ms-blob-type. <br/>
ETag and LastModified are read only! <br/>
Blob container besides <b>System Properties<b/> also can have <b>Used-defined metadata</b>. In User-defined metadata it's string based key-value pairs which is stored in the container. The same concept exists on the Blob - so it also can have User-defined metadata.
  
Properties and metadatas are set and retrieved via HTTP headers.
  
# Access Tiers for Block Blobs
* hot (default) - used for frequently accessed data, it's online
* cool - infrequently accessed data stored for at least 30 days, it's online
* archive - data that can be archived for at least 180 days, it's offline
  
Access and transaction costs are low for hot tier and high for archive but on the other hand storage costs per GB is low for archive tier and high for hot tier.
  
For storage account you can set default access tier - hot or cool where hot is default. In Block Blob you can choose hot, cool, archive. Notice that archive can be set only on Block Blob level. 
  
To move data from archived to cool or hot it can take several hours and process is called <b>Rehydrating</b> <br/>
Support access tiers only for StorageV2 and BlobStorage. Access tiers can be changed manually in Azure Portal but also we can manage the Blob lifecycle (Lifecycle Management in Azure Portal) with rules when it should change state.
  
For blob soft delete can be enabled then when you remove blob you can click `show deleted blobs` and then click `undelete` so again blob which was removed previously is restored. The same appply for `versions` and `snapshots`
  
# Snapshots and verions
Snapshot is read only copy of Blob in a specific point of time. So if you want to create blob from current version then just need to click `create snapshot`. <br/>
Version let us to get previous version of blob - let's say that we have image.png blob, then we upload again image.png with other content. It will be overriden but still we can get original version when we enabled `Version` in Azure Portal. You can even restore original version of image.png. In general versions let us keep history of changes for our blob

Lease can be acquire for Blob and then it's not possible to change or delete. If need to unblock then `break lease`
  
Immutable Blob Storage - in `access policy` you can set `time-based retention` on e.g 7 days, then for 7 days Blob can't be changed or deleted.
  
# Moving items between storage account and containers
To move items in blob storage you copy items from source to target and then delete the source. Tools to copy items in Blob Storage: Azure CLI (`az storage blob copy start`), AzCopy (`azcopy copy`), .NET client library. 
  
  
PS /home/pluralsight-50a97207> Get-AzStorageContainer -Context $storageAccount.Context

Storage Account Name: psblobstorageacc414481

Name                 PublicAccess         LastModified                   IsDeleted  VersionId
----                 ------------         ------------                   ---------  ---------
cars-and-engines     Off                  9/28/2022 11:54:35 AM +00:00              
food                 Off                  9/28/2022 11:46:58 AM +00:00  
  
  
  
PS /home/pluralsight-50a97207> $carsAndEnginesContainer.CloudBlobContainer.Metadata.Add("content","pictures about cars and engine")
PS /home/pluralsight-50a97207> $carsAndEnginesContainer.CloudBlobContainer.Metadata.Add("pictures_count","4")
PS /home/pluralsight-50a97207> $carsAndEnginesContainer.CloudBlobContainer.SetMetadata()
PS /home/pluralsight-50a97207> 
PS /home/pluralsight-50a97207> $carsAndEnginesContainer.CloudBlobContainer.Metadata.Remove("content")
True
PS /home/pluralsight-50a97207> 
PS /home/pluralsight-50a97207> $carsAndEnginesContainer.CloudBlobContainer.Metadata

Key            Value
---            -----
pictures_count 4
  
  
PS /home/pluralsight-50a97207> $carsAndEnginesContainer.CloudBlobContainer.Metadata["pictures_count"]
4
  
  PS /home/pluralsight-50a97207> $carEngine1Blob.ICloudBlob.Metadata.Add("cylinders","6")
PS /home/pluralsight-50a97207> $carEngine1Blob.ICloudBlob.Metadata.Add("liters","3")
PS /home/pluralsight-50a97207> $carEngine1Blob.ICloudBlob.Metadata.Add("traction","rear")
PS /home/pluralsight-50a97207> $carEngine1Blob.ICloudBlob.SetMetadata()
PS /home/pluralsight-50a97207> $carEngine1Blob.ICloudBlob.Metadata

Key       Value
---       -----
cylinders 6
liters    3
traction  rear

PS /home/pluralsight-50a97207> $carEngine1Blob.ICloudBlob.Metadata.Remove("cylinders")
True
PS /home/pluralsight-50a97207> $carEngine1Blob.ICloudBlob.Metadata

Key      Value
---      -----
liters   3
traction rear

  
  PS /home/pluralsight-b06e4edc> Get-AzStorageAccountManagementPolicy -ResourceGroupName pluralsight-resource-group -AccountName globomanticsp52f01z2lm
Get-AzStorageAccountManagementPolicy: No ManagementPolicy found for account globomanticsp52f01z2lm
  
# Review CosmosDB
Cosmos DB supported API: SQL, Cassandra, MongoDB, Gremlin, Azure Table. SQL is the most important here. 
  
Consistency levels: <b>Consistent Prefix</b> - ensure we will have right order of reading. <b>Session</b> - we will see our own writes but not others.
  
Cosmos DV server-side Concepts: store procedures, tiggers and User defined functions are JavaScript based and runs in CosmosDB environment, change feed can run in any environment - azure functions or your own.
  
# Review Blob
Copying data between storage account
  
Data rehydration Priorities:
* standard priority - it can take from 1 to 15 hours
* high priority - it can be rehydrated faster but cost more
  
Only Read-access geo-redundant Storage and read-access geo-redundant storeage can read from second location, i mean from non-primary regions
  
azCopy
  
Rehydration take between one and 15 hours <br/>
Multiple containers in the same container group - it's not supported on Windows (--hyper-v), so it will be e.g --sku B1 --is-linux </br>
To update the metadata of the blobs: fetchAttributesAsync, then Metadata.Add, then SetMetadataAsync
