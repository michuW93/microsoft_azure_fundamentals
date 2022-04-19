microsoft_azure_fundamentals-DP-900-

# microsoft_azure_fundamentals-DP-900-
Tutorial based on Henry Been, Emilio Melo, Niraj Joshi, Ifedayo Bamikole, Mohit Batra, Nikola Ilic tutorial

# What is data?
Data is a collection of facts, such as numbers, words, measurements, or just description of things.

Data helps you make better decisions - decisions that are based on the knowledge coming from the data.

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

**Main Azure Data Factory components**:
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

Data lake repository of data stored in it's natural format, every chunk of data is assigned with unique ID.

Hadoop consist of:
* distributed storage (Hadoop distributed file system) to store huge amount of data
* map reduce key-value mechanism, paraler processing framework


Azure HDInsight is a manged Hadoop service on the cloud. Hadoop distributed file system and map reduce remainst the same. Integration with other cloud services - Azure Data Factory, CosmosDB, Spark, Kafka, etc.

Azure HDInsights pros: scale up or down base on traffic, cost (as you dont need to keep huge dbs on premises servers), 

Cluster types:
* Hadoop - batch processing,
* Kafka - streaming platform,
* ML Services - predictive modelling
* Spark - In-memory processing,
* Interactive query - in memory caching 

# Azure Databricks
It's fully-managed, *Apache Spark* based cloud-based platform, that can be used for Big Data processing and Machine Learning. 
Pros:
* multiple languages: Java, Scala, R, SQL etc.
* integration with Azure Active Directory and Azure services: Azure Data Service, Azure Storage
* fullfils multiple industry security compliances  


Azure Databricks components:
* Workspace - Apache Spark workspace for exploration and visualisation 
* Cluster - Apache Spark cluster that can be created in seconds and autoscale and share across users
* Notebook - Apache Spark Notebook that can write, query, explore and visualise datasets

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/dp-900/images/ETL_azure_databricks.png?raw=true)

Azure Databricks can be used in machine learning process as well as streaming (Structured Streaming).

# Azure Synapse
**Azure Synapse is not a single service, it's group of multiple well-integrated Azure data services.** It brings data integration, enterprise data warehousing and big data analytics.

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/dp-900/images/synapse_workspace.png?raw=true)

* Storage: Azure Data Lake Gen2 (one acc is mounted by default)
* Compute: Dedicated SQL pools, Apache Spark pools, Mapping Data Flows, Serverless SQL Pool
* Ingestion: Synapse Pipelines (shares code with Azure Data Factory and can copy data from variety of sources), Mapping Data Flows
* connected services: Azure Cosmos DB (directly quering), Azure ML (integration with Azure Cognitive Services), Power BI, Azure SQL etc.

Synapse Pipelines - Data Integration service that allows to create data-driven workflows. 

**Ingest** (Ingest data at scale using COPY activity with support for 90+ connectors) -> **Transform** (Transform data at scale with code-free, Spark Based Mapping Data Flows) -> **Orchestrate** (Automate data movement and processing using Pipelines and Control Flow activities).


**Dedicated SQL Pool**:
* Earlier known as Azure SQL Data Warehouse
* Available as standalone service and within Synapse
* like a SQL Server Database
* Massive Parallel Processing (MPP) architecture. One control node -> several compute nodes (more nodes, more to pay) -> azure storage. If there is a query then control node analyse and send querites to compute nodes, they do the same and query db then get answer and merge results from many dbs and send results to control node which merge results from many compute node and send response.
* elastically scale compute and storage separately
* pause or resume service to save cost
* Polybase - control node send metadata to compute node and compute nodes read sth from Azure Storage directly so Polybase allows to read and write data in external storage using T-SQL, parallel processing of files - extremaly fast.

**Spark on Synapse**:
* open source, in-memory engine, runs on cluster
* performs distributed processing of data
* multiple language support
* integration with Synapse services

We can use Spark for Batch processing, stream processing, machine learning.

**Serverless SQL Pool** (uses distributed SQL engine called Polaris) - distributed data processing system that allows to run federated queries on variety of sources using T-SQL. How query execution works? User send query to control node, it analyze query and send to some of some compute nodes, compute nodes then run queries against external datasources (data lake, cosmosDB, spark tables).



# Questions:
Your company needs to implement a relational database in Azure, maintenance must be minimized. You should use Azure SQL Database.
