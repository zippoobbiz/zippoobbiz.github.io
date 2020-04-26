---
title: BigQuery
date: 2018-07-01 14:24:58
tags: [GCP, BigQuery]
categories: [Cloud, GCP, BigQuery]
---

![bigquery](https://philsblog.b-cdn.net/images/bigquery.png "bigquery")

### feature summary
* Petabyte scale DW on GCP for interactive analysis (near real time analysis, it’s not totally real time, cannot respond in millisecond, microsecond).
* Prefer demoralised table structure using nested, repeated fields.
* Separate storage and compute.
* Data stored in bigQuery is durable, it’s replicated in multiple places and it’s pretty inexpensive in terms of storing.
* Support both standard SQL(SQL 2011), legacy SQL. Default is legacy SQL. Standard SQL is preferred since BigQuery 2.0
* No-ops
* Generate immutable audit logs. you know every time somebody’s runs a query on it and you basically get those audit logs which cannot be tampered with. So you will know what people have done to each dataset.
* 

### Cache
Query results are cached for approximately 24 hours by default
Not cached cases:
* When a destination table is specified in the job configuration, the web UI, the command line, or the API
* If any of the referenced tables or logical views have changed since the results were previously cached
* When any of the tables referenced by the query have recently received streaming inserts (a streaming buffer is attached to the table) even if no new rows have arrived
* If the query uses non-deterministic functions; for example, date and time functions such as CURRENT_TIMESTAMP() and NOW(), and other functions such as CURRENT_USER() return different values depending on when a query is executed
* If you are querying multiple tables using a wildcard
* If the cached results have expired; typical cache lifetime is 24 hours, but the cached results are best-effort and may be invalidated sooner
* If the query runs against an external data source


### Structure
* Big query is not transactional
* every column is stored in a separate file which is encrypted and replicated
* BQ is primarily meant for immutable very large datasets
* table is materialised / view is live

Tools with connector:
Tableau, Looker, Qlik, Data studio, etc

Supported ingest format: JSON (newline delimited only), CSV, Avro, Parquet, ORC, Google Cloud Datastore (Store on GCS only).

### Ingestion:
streaming and batch
Why use dataflow if we can use stream input directly on BigQuery? Because BigQuery only accept table format, the source data mey need to be converted in dataflow.
Can load data from:
* File upload
* Google Cloud Storage
* Google Drive
* Google Cloud Bigtable
* Stream data in from Fluentd by using a plugin

Cannot load from:
Cloud SQL

Cannot use the Web UI to:
* Upload a file greater than 10 MB in size
* Upload multiple files at the same time
* Uploada file in SQL format

All the above three operations can be performed using the "bq" command.

### Sharing
BigQuery is a way for you to share data beyond the silos of your company’s structure, it’s a way of collaboration
you can share the dataset, allow them to write ad hoc query, also share the query, share the ability of analysis
access control on data set
dataSets contain tables and views
You can select specific rows and columns and save it as view, then share it with others(other project)

### External storage:
GCS, google sheet, BigTable

#### From BigTable
Permanent - can share
* Create a table definition file (for the CLI or API)
* Create a table in BigQuery linked to the external data source
* Query the data using the permanent table

To share you need:
* READER or bigquery.dataViewer
* biguqery.user
* bigtable.reader

Temporary
it cannot be shared with others, is useful for one-time, d-hoc queries over external data, or for extract, transform, and load (ETL) processes.

* A table definition file with a query
* An inline schema definition with a query
* A JSON schema definition file with a query

* Create a table definition file
* Submit both a query and a table definition file


SQL Functions:
ARRAY_AGG
UNNEST
REGEXP_CONTAINS
STARTS_WITH

Navigation
LEAD, LAG, NTH_VALUE

Window function
RANK OVER

approx function

### tips
only order at outer query
use skydiver GUI to monitor bigquery

### Pricing

Pay for using / flat rate price
Cancel jobs, pay for what have processed so far.
Can Set billing limits

Charge on ingest streaming
1TB/month free
$5 per TB
Discount on old data.
Storage cost is about the same as the cost of GCS, get the sam discount as well (after 90 days)

can limit the usage on the project or the user

#### reduce cost
* Use preview options
* Use Query validator before you run your query
* Avoiding select * statement
* Hard limit the capacity allowed to be processed on projects and users

### Partition
Up to 2,500 partitions
Daily limits: 2,000 partition updates per table per day
Rate limit: 50 partition updates every 10 seconds
You cannot change an existing table into a partitioned table. You must create a partitioned table from scratch. Then you can either stream data into it every day and the data will automatically be put in the right partition, or you can load data into a specific partition by using "$YYYYMMDD" at the end of the table name.

pseudo column _PARTITIONTIME
user can use pseudo column, but cannot see it

### wildcard
union join all similar named tables within the dataset
tables must have the same structure
_TABLE_SUFFIX in where clause

### Authorized Views:
Create views, add account to the view, add authorized view from the source table
An authorized view allows you to share query results with particular users and groups without giving them read access to the underlying tables. Authorized views can only be created in a dataset that does not contain the tables queried by the view. When you create an authorized view, you use the view's SQL query to restrict access to only the reows and columns you want the users to see.
### Questions:

Is could SQL and Spanner respond quicker than BigQuery?
what’s tail latency? tail skew?
use having clause to avoid tail skew

### Jobs
* load
* extract
* query
* copy

### IAM
For example, a user who merely has bigquery.dataViewer permissions on a dataset without any other permissions can only list the tables in the dataset and use the get() APIs to read the contents of the tables. The user cannot query the data without additional permissions.

For an example of a user with permissions to run queries, consider the following scenario. A user who has bigquery.user permissions in projectA, and bigquery.dataViewer permissions on projectA:dataset1 and projectB:dataset2 can run a query in projectA that uses either or both of these datasets.

The dataViewer doesn’t have the ability to incur costs

#### Roles

* bigquery.user
	- Permissions to run jobs, including queries, within the project. 
	- Enumerate their own jobs, cancel their own jobs, and enumerate datasets within a project. 
	- Allows the creation of new datasets within the project; the creator is granted the bigquery.dataOwner role for these new datasets.

* bigquery.jobUser
	- Permissions to run jobs, including queries, within the project. 
	- Can enumerate their own jobs and cancel their own jobs.
	- Does not allow access to any BigQuery data

* bigquery.dataViewer
	- Read the dataset's metadata and to list tables in the dataset.
	- Read data and metadata from the dataset's tables.

* bigquery.dataEditor
	- Read the dataset's metadata and to list tables in the dataset.
	- Create, update, get, and delete the dataset's tables.

* bigquery.dataOwner
	- Read, update, and delete the dataset.
	- Create, update, get, and delete the dataset's tables.

* bigquery.admin
	- all

### Appliction profile??
* stores settings that tell your Cloud Bigtable instance how to handle incoming requests from an application
* affect how your applications communicate with an instance that uses replication
* especially useful for instances that have 2 clusters