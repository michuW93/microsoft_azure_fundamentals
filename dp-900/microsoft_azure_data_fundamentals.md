microsoft_azure_fundamentals-DP-900-

# microsoft_azure_fundamentals-DP-900-
Tutorial based on Henry Been, Emilio Melo, Niraj Joshi tutorial

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

# Azure Data Factory
What problem does it solve? Nowadays we collect data from many sources: business app, erp, social media, IoT etc. then we need one source of truth so we need to **extract, tranform and load** into Data Warehouse. Azure data factory is doing ETL for us.

Definition: a cloud-based (PaaS Service) data integration service (consolidates data from multiple sources into a common view) that allows you to orchestrate and automate data movement and data transformation (transforms data itself (mapping data flows) or calls other services for it).

ETL(transform before loading, designed for reliability) vs ELT(transform after loading, designed for agility)
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/dp-900/images/etl_vs_elt.jpeg?raw=true)


There are two main versions of ADF v1 and v2. v1 base on configurations by JSON while v2 has clean graphical interface which is much easier to use.
There are several ways how you can interact with ADF e.g Data Factory resources, PowerShell, Python, REST Api, ARM templates. Highly integrated e.g with Azure Key Vault to securely hold credentials, Azure Monitor, Databricks etc.
ADF is not data storage, there is no data in ADF, you need to persist data by the end of execution.

**Main ADF components**:
* activities - pipeline is logical set of activities. 3 kinds of activities: Data movement, data transformations, data control
* pipelines - can be craeted graphically on the Data Factory site or thought code.
* trigger - when you want pipeline to execute e.g Monday 7:00. There are three types of triggers - schedule, tumbling window (for periodic data processing e.g every 2 hours) and event-based (fired based on an event e.g file arrival or file delete).
* Integration runtimes - are the compute infrastructure of Azure Data Factory which is needed to execute activities. It provides four main capabilities: execution of Data Flow activities, Data movement activities, dispatch of activities, SSIS package execution
* linked services - similar to Connection Strings - tells you where to find the data. Can point to SQL Database, Blob Storega
* datasets - represenations of the data that we're working with so generally concerned with the data structures inside a data store e.g describing name column is string, age is number. Can point to Tables, Files

# HDInsight
Big data attributes:
* high volume of data incoming from varied sources such as blobs, sensor data, social media and others which occupies a huge space,
* velocity - frequency with which data accumulates, such as tweeter feeds, share market pricing, GPS data etc.
* variety - data comes from variet mediums and sources,
* veracity - uncertainty of the data, it can be unstructured, semi-structured or structured 
