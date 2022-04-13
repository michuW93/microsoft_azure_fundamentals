microsoft_azure_fundamentals-DP-900-

# microsoft_azure_fundamentals-DP-900-
Tutorial based on Henry Been tutorial

# Types of data
* **Structured**: Follows a predefined schema, often in a tabular form. Appears in CRM, ERP, administrative systems. Data is organized in tables, tables contains records. Records conforms to a schema. Tables have primary key and can have foreign keys. We use relational databases for structured data and we communicate with it with Structured Query Language (SQL) which is declarative. 
Examples of Relations Database: **Microsoft SQL Server** - there is Azure Service called **Microsoft Azure SQL Database**, **MySQL**, **PostgreSQL** - more complex than MySQL
* **Unstructured**: No predefined structure, no notion or fields, labels or types. Example: videos, images, audio files. Much harder to automatically process, often processed using machine learning to generate more structure data. We use non relational databases for unstructured data. They don't store data in tables but in collections or containers, they don't follow predefined schema. Different types available: **Document database**, **Wide-column store** but without predefined schema and **key-value store**, **Graph databases**. Examples of non relational dbs: **Redis** - often used for caching, **Cassandra**, **Azure CosmosDB** - only available on Azure.
* **Semi-structured**: Is not necessarily tabular in nature, yet has an observable structure. Example: log files, data export/import formats e.g XML, JSON, CSV
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/dp-900/images/types_of_data.png?raw=true)

# Workloads:
* **Transactional** - support high volumes of reads and writes to support information systems like CRMs, tracking software or record keeping. Answers are always correct and full. Transactions / ACID properties, OLTP

ACID is a set of properties that you would like to apply when modifying a database.
   * Atomicity - means that you can guarantee that all of a transaction happens, or none of it does; you can do complex operations as one single unit, all or nothing, and a crash, power failure, error, or anything else won't allow you to be in a state in which only some of the related changes have happened. 
   * Consistency - means that you guarantee that your data will be consistent; none of the constraints you have on related data will ever be violated.
   * Isolation - means that one transaction cannot read data from another transaction that is not yet completed. If two transactions are executing concurrently, each one will see the world as if they were executing sequentially, and if one needs to read data that is written by another, it will have to wait until the other is finished.
   * Durability - means that once a transaction is complete, it is guaranteed that all of the changes have been recorded to a durable medium (such as a hard disk), and the fact that the transaction has been completed is likewise recorded.

A transaction is a set of related changes which is used to achieve some of the ACID properties. Transactions are tools to achieve the ACID properties.
So, transactions are a mechanism for guaranteeing these properties; they are a way of grouping related actions together such that as a whole, a group of operations can be atomic, produce consistent results, be isolated from other operations, and be durably recorded.


* **Analytical** - support queries for getting insights or an overview over large amounts of data for KPIs, analysis, reports and business intelligence. Lower volume of read-only queries but larger amount of data. Batch-based or streaming data (OLAP)


# Analytical processing types
* Batch data - periodically transfer data to another database for analytical querying. Executes on schedule, all data is stored for analytical querying, you query the data after loading whenever you want, easy joining of datasets, efficient opportunities
* Streaming data = continously calculate new nalytical query results when data is added or updated. Executes near real-time, stores queries, not other data, queries are predefined, combaining datasets is more difficult

You can mix all data types and database types in both batch data and streaming data approches!

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/dp-900/images/batch_data.png?raw=true)
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/dp-900/images/streaming_data.png?raw=true)

