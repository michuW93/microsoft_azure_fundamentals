microsoft_azure_fundamentals-DP-900-

# microsoft_azure_fundamentals-DP-900-
Tutorial based on Henry Been tutorial

# Types of data
* **Structured**: Follows a predefined schema, often in a tabular form. Appears in CRM, ERP, administrative systems. Data is organized in tables, tables contains records. Records conforms to a schema. Tables have primary key and can have foreign keys. We use relational databases for structured data and we communicate with it with Structured Query Language (SQL) which is declarative. 
Examples of Relations Database: **Microsoft SQL Server** - there is Azure Service called **Microsoft Azure SQL Database**, **MySQL**, **PostgreSQL** - more complex than MySQL
* **Unstructured**: No predefined structure, no notion or fields, labels or types. Example: videos, images, audio files. Much harder to automatically process, often processed using machine learning to generate more structure data. We use non relational databases for unstructured data. They don't store data in tables but in collections or containers, they don't follow predefined schema. Different types available: **Document database**, **Wide-column store** but without predefined schema and **key-value store**, **Graph databases**. Examples of non relational dbs: **Redis** - often used for caching, **Cassandra**, **Azure CosmosDB** - only available on Azure.
* **Semi-structured**: Is not necessarily tabular in nature, yet has an observable structure. Example: log files, data export/import formats e.g XML, JSON, CSV
![alt text](https://github.com/michuW93/microsoft_azure_fundamentals/blob/master/dp-900/images/types_of_data.png?raw=true)
