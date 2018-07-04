---
title: BigQuery
date: 2018-07-01 14:24:58
tags: [GCP, BigQuery]
categories: [GCP, BigQuery]
---

{% qnimg bigquery.png %}

### feature summary
* Petabyte scale DW on GCP for interactive analysis (near real time analysis, it’s not totally real time, cannot respond in millisecond, microsecond).
* Prefer demoralised table structure using nested, repeated fields.
* Separate storage and compute.
* Data stored in bigQuery is durable, it’s replicated in multiple places and it’s pretty inexpensive in terms of storing.
* Support both standard SQL(SQL 2011), legacy SQL. Default is legacy SQL. Standard SQL is preferred since BigQuery 2.0
* No-ops
* Generate immutable audit logs. you know every time somebody’s runs a query on it and you basically get those audit logs which cannot be tampered with. So you will know what people have done to each dataset.
* Query results are cached for approximately 24 hours by default, query results are not cached if you specify a destination table.

### Structure
* Big query is not transactional
* every column is stored in a separate file which is encrypted and replicated
* BQ is primarily meant for immutable very large datasets
* table is materialised / view is live

Tools with connector:
Tableau, Looker, Qlik, Data studio, etc

Supported ingest format: JSON, CSV, Avro, etc.

### Ingestion:
streaming and batch
Why use dataflow if we can use stream input directly on BigQuery? Because BigQuery only accept table format, the source data mey need to be converted in dataflow.
Can load data from:
* File upload
* Google Cloud Storage
* Google Drive
* Google Cloud Bigtable

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
GCS, google sheet, bigtable


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
