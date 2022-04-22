microsoft_azure_fundamentals-DP-900-

# microsoft_azure_fundamentals-DP-900-
Tutorial based on Henry Been, Emilio Melo, Niraj Joshi, Ifedayo Bamikole, Mohit Batra, Nikola Ilic, Pinal Dave, Viktor Suha, Mihaela Danci tutorial

# What is data?
Data is a collection of facts, such as numbers, words, measurements, or just description of things.

Data helps you make better decisions - decisions that are based on the knowledge coming from the data.

# Types of data
Different types of data require different types of storage.

* **Structured**: Follows a predefined schema, often in a tabular form. Appears in CRM, ERP, administrative systems, banking solutions, flight reservations, e-commerce app etc. Data is organized in tables, tables contains records. Records conforms to a schema. Tables have primary key and can have foreign keys. We use relational databases for structured data and we communicate with it with Structured Query Language (SQL) which is declarative. 
Examples of Relations Database: **Microsoft SQL Server** - there is Azure Service called **Microsoft Azure SQL Database**, **MySQL**, **PostgreSQL** - more complex than MySQL

Normalization is the process of organising data in database it allows to avoid data redundancy withing tables and relationships. Redundant Data wastes space and causes maintenance problems. In most cases 3rd Normal Form is considered necessary. It eliminate transitive dependency.
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/dp-900/images/3_normal_form_0.jpg?raw=true)

![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/dp-900/images/3_normal_form.png?raw=true)

**In general normalization improves data integrity and reduces data redundancy but it doesn't eliminate relationships between database tables**.


* **Unstructured**: No predefined structure, no notion or fields, labels or types. Example: videos, images, audio files. Much harder to automatically process, often processed using machine learning to generate more structure data. We use non relational databases for unstructured data. They don't store data in tables but in collections or containers, they don't follow predefined schema. Different types available: **Document database**, **Wide-column store** but without predefined schema and **key-value store**, **Graph databases**. Examples of non relational dbs: **Redis** - often used for caching, **Cassandra**, **Azure CosmosDB** - only available on Azure.
* **Semi-structured**: Is not necessarily tabular in nature, yet has an observable structure. Example: log files, data export/import formats e.g XML, JSON, CSV
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/dp-900/images/types_of_data.png?raw=true)



# Workloads:
* **Transactional** - support high volumes of reads and writes to support information systems like CRMs, tracking software or record keeping. Answers are always correct and full. Transactions / ACID properties, OLTP (suitable for high volume of transactions, Support insert, update and delete statements, convenient for running ad-hoc queries, focus on data integrity). Relational database are suitable for transaction processing

ACID is a set of properties that you would like to apply when modifying a database.
   * Atomicity - means that you can guarantee that all of a transaction happens, or none of it does; you can do complex operations as one single unit, all or nothing, and a crash, power failure, error, or anything else won't allow you to be in a state in which only some of the related changes have happened. 
   * Consistency - means that you guarantee that your data will be consistent; none of the constraints you have on related data will ever be violated.
   * Isolation - means that one transaction cannot read data from another transaction that is not yet completed. If two transactions are executing concurrently, each one will see the world as if they were executing sequentially, and if one needs to read data that is written by another, it will have to wait until the other is finished.
   * Durability - means that once a transaction is complete, it is guaranteed that all of the changes have been recorded to a durable medium (such as a hard disk), and the fact that the transaction has been completed is likewise recorded.

A transaction is a set of related changes which is used to achieve some of the ACID properties. Transactions are tools to achieve the ACID properties.
So, transactions are a mechanism for guaranteeing these properties; they are a way of grouping related actions together such that as a whole, a group of operations can be atomic, produce consistent results, be isolated from other operations, and be durably recorded.


* **Analytical** - support queries for getting insights or an overview over large amounts of data for KPIs, analysis, reports and business intelligence. Lower volume of read-only queries but larger amount of data. Batch-based or streaming data (Online Analytical Processing System - OLAP). While Transactional systems are for WRITE, analytical systems are for READ. OLAP focus shifts from single transaction to aggregated data so it's for big picture. Generate insights - Sales trends, customer retention, process improvement.
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/dp-900/images/olap_workflow.png?raw=true)


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

# Delivery Models in Azure
Infrastructure as a service: Azure VMs, Storage accounts

Platform as a service: Azure SQL DB, CosmosDB, Synapse Analytics

Software as a service: Outlook, Office365

# Azure Data Services
Azure data services are built to ensure that your database is available for at least 99.99% of the time.

**Azure SQL Database** - platform as a service offering from Microsoft. Azure SQL DB Available Options:
* Single DB - you set it up and run. You are charged per hour you requested.
* Elastic Pool - multiple databases share the same resources (memory, storage, process)
* Managed Instance - you can install multiple DB's on single instance. You have full control over security and resources like in traditional on-prem server.

**Azure DB for MySQL** is commonly implemented using single server deployment mode. You can create Azure DB for MySQL by command-line interface, Azure PowerShell, Azure portal.
* based on MySQL Community Edition
* Automatic backups and restores
* Automated maintenance
* elastic scaling
* build-in high availability
* cost optimization

**Azure DB for PostgreSQL** - it's hybrid relational-object database which means you can store relational and non-relational data in it using custom data types to define entity properties. It can store and handle geometric data such as circles, lines, triangles etc. It provides two deployment models: single server and hyperscale (Citus) for large DBs

# Queries in relational DBs
DML - data manipulation language. SELECT, INSERT, CREATE, DELETE, etc.
DDL - data definition language. CREATE, DROP, ALTER, RENAME e.g ALTER TABLE Employee ADD BirthData date;

# Azure Table Storage (non relational)
Azure Table Storage is a scalable key-value store held in the cloud. Items are reffered as rows and fields are refered as columns. No relationships, no stored procedures, denormalized data, grouping related rows based on partition key to search much faster. Very useful for event logging, performance monitoring data

Advantages:
* simpler to scale
* semi-structured data
* no complex relationships so fast row insertion and faster data retrieval when you know partition key
* high-availability in a single region - data is copied multiple times in a single region

# Azure Blob Storage 
Azure Blob (**binary large object**) storage is a service that enables you to store massive amounts of unstructured data, or blobs, in the cloud. Advantages: Reduncancy(3 copies in one region), soft delete - we can get back accidentally removed or overwritten blob. Example usecase: serving images/docs from browser, streaming video and audio, storing data for backups and store

Three types of blobs:
* Block - it's good for large binary objects which change infrequently
* page - collection of fixed size, 512 byte pages. They are optimized to support random read and writes
* append - an append blob is block blog optimized to support append operations, you cant update or delete exsisting blobs, you can only append new blob at the end of last blob

There are three types of access tiers:
* hot (default) - for data which we have to access frequently
* cool - cost less than hot but also provides lesser performance
* archive - lowest storage cost but latency to retrieve data is the highest. If we want to access archived data we need to rehydrate(bring data back to cool or hot tier) our data first.

# Azure File Storage
Azure File storage enables you to create files shares in the cloud, and access these file shares from anywhere with an internet connection. It uses SMB 3.0 protocol. Azure file storage supports Azure Active Directory so we can control access using authentication and authorisation. Advantages: very high capacity, supports Azure File Syns and AzCopy, data encryption at rest (when your data is not moving then it's 100% encrypted). Example usecases: Migration of application to the cloud, data sharing across on-premises and could, hosting high availability workload data

There are two tiers for Azure File storage:
* standard - HDD (hard disk drives)
* premium - SSD

# Azure CosmosDB
Azure Cosmos DB is multi-model NoSQL database management system. Data as partitioned set of documents where document is a collection of files identified by a key. Azure CosmosDB supports JavaScript Object Notation (JSON), CosmosDB supports many APIs like SQL API, Table API, MongoDB API, Gremlin API etc.

CosmosDB is used where you have a frequent bursts of large activity (IoT). Single digit latency e.g it's useful for gaming platforms, it's also great for e-commerce because of elastic scale up or down. Skype, Xbox, Microsoft 365 are using CosmosDB

Advantages:
* high availability 99.999%
* replication across regions
* 10-ms or less latancies for reads/writes
* certified for compliance standards
* encrypted at rest and in motion - data is always secured


# Time Series Data
Time series data is a set of values organized by time. Usecase: asset progress over time, detect anomalies, visualize trends, compare historical trends.

Challanges:
* high volume - a lot of data
* high speed storage
* powerful computation

in Azure we have **Azure time series insights** to manage it. It's stream processing, data store, analytics, reporting

# Azure Data Studio
Azure data studo:
* lightweight
* multi-database desktop tool - it let you connect to multiple different databases including SQL Server and PostgreSQL
* cross-platform because runs on Windows, Linux and MacOS
* open source - code is on GitHub

In Azure Data Studio you can import files with data into tables, you can compare database schema with different database etc.

Working with Azure Data Studio: first you connect to db, then you run query then you can e.g visualize data on bar chart or export query results to different formats e.g JSON

Database connections:
* SQL Server,
* PostgreSQL
* SQL Server Big data cluster
* azure SQL database
* Azure Synapse Analytics
* Azure data explorer
* Azure Database for PostgreSQL


Azure Data Studio vs SQL Server Management Studio - when you mostly run and edit queries and dont need complex database management tool use Azure Data Studio, in the other hand when you mostly manage the database and need full database management capability, including security task use SQL Server Management Studio (it works only on Windows).


Main components of Azure Data Studio:
* connections - where you create and manage database connections. You can create server groups to categorize connections for easier maintenance e.g test dbs
* dashboards - can display custom properties e.g performance data
* object explorer - to explore tables or views (**In a database, a view is the result set of a stored query on the data, which the database users can query just as they would in a persistent database collection object. This pre-established query command is kept in the database dictionary. Unlike ordinary base tables in a relational database, a view does not form part of the physical schema: as a result set, it is a virtual table computed or collated dynamically from data in the database when access to that view is requested**)
* query editor - to run and edit SQL query
* query result viewer - displays data
* notebooks
* extensions

* command Palette - shortcuts
* integrated terminal - to run PowerShell or bash commands without leaving tool
* source control
* accounts
* settings
* deployment wizard


# Power BI (charts creator)
Power BI Desktop is a free desktop application that supports the full analytics workflow from connecting to data to insights generation. In general Power BI is a collection of software services, apps, and connectors that work together to turn unrelated sources of data into interactive insights.

There is also a Web version of Power BI also you can check content on iOS, Android, Windows, anywhere.

It can also produce Paginated reports - they are great for content ready to be printed. In Interactive report when we have 1000 rows it will just print some of these, on the other hand paginated report will print all 1000 rows over multiple pages.

In Data Warehouse Modeling, a star schema and a snowflake schema consists of Fact and Dimension tables.

**Fact Table:**
It contains all the primary keys of the dimension and associated facts or measures(is a property on which calculations can be made) like quantity sold, amount sold and average sales.

**Dimension Tables:**
* Dimension tables provides descriptive information for all the measurements recorded in fact table.
* Dimensions are relatively very small as comparison of fact table.
* Commonly used dimensions are people, products, place and time.

































# Questions:
1. Your company needs to implement a relational database in Azure, maintenance must be minimized. You should use Azure SQL Database.
2. You need to query table Products in an Azure SQL database. You must have SELECT access to the Products table, you must have user in the database and your IP address must be allowed to connect to the database.
