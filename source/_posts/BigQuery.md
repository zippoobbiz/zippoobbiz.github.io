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
* Support both standard SQL(SQL 2011), legacy SQL
* No-ops
* Generate immutable audit logs. you know every time somebody’s runs a query on it and you basically get those audit logs which cannot be tampered with. So you will know what people have done to each dataset.

### Structure
* Big query is not transactional
* every column is stored in a separate file which is encrypted and replicated
* BQ is primarily meant for immutable very large datasets
* table is materialised / view is live

Tools with connector:
Tableau, Looker, Qlik, Data studio, etc

Supported ingest format: JSON, CSV, Avro, etc.


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

### Questions:

Is could SQL and Spanner respond quicker than BigQuery?
what’s tail latency? tail skew?
use having clause to avoid tail skew
