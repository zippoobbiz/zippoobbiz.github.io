---
title: GCP Fundamentals
date: 2018-07-03 10:07:07
tags: [GCP, GCS, GCE, Cloud SQL, Dataproc, Datastore, BigTable, BigQuery, Datalab, TensorFlow, Cloud ML Engine, ML APIs]
categories: [GCP]
---

{% qnimg gcp.png %}

Why GCP? 
MapReduce tends to be limited by the number of compute nodes that you have. Use cloud, you have:
Grate scalability and reliability
As no-ops as possible, minimise a system administration overhead
As flexible as possible


### GCS
Global scale data and computer infrastrure, Staging area
BLOB, raw data in any format
Disk goes away with compute engine, GCS will always be there
durable, replicated
can use it to stage the data onto other GCP products

Load data to GCS: gustil cp
K V pare, even it looks like directory.
can get access by: REST API, console
Transfer service - could be one time, could be recurring
source: locamachine, AWS S3, etc.
every bucket belongs to a project.
edge cached

### Google Computer Engine
N1-standard-4
if only 60% of usage, get 15% discount
preemptible VM 80% discount (Not sure) others can take it away anytime

### Cloud SQL
Single machine
Handle *gigabytes* of data
Relational database, support update and deletes individual fields
Flexible pricing, passivate it when not running, good for testing
Managed backups by google
connect from anywhere
automatic replication
fast connection from GCE & GAE etc.
Google security

### {% post_link Cloud-Dataproc Dataproc %}
Cluster contains master(s), workers
Resizable
##### storage
* Can use HDFS on clusters node.
* Can store data on GCS and use preemptible(probably 10 standard, 30 preemptible) to run your job.(You don’t want to store it on node, because you don’t want to pay the compute when you only need storage) separate the compute and storage. Store it in the save place as the cluster.

Think the cluster as a job specific resources.
Google managed hadoop Pig, Hive, Spark programs
Hadoop ecosystem
Spark - interactive SQL
pig - ETL script
Hive - do queries
Presto???

### Datastore
Terabytes
HashMap K V pare
Search by *key or property*
*Transactional*
what's kind in datastore???
Support CRUD operation
hierarchical data

### {% post_link BigTable BigTable %}
Petabytes
Support append only operation
No transactional support
Always right a new row, append to the table, read the latest data from the table backward, so always get the newest version of the object
High throughput 
No-ops
flattened data
Search only based on the rowkey, important to design the good key
to find the key quickly, avoid hotspot, want it to be distributed.
Make the table tall and narrow.
column family, group related columns? but why?????

### {% post_link BigQuery BigQuery %}
standard SQL 2011 / lagecy SQL
user defined function in JS
Query CSV, JSON, Avro files on GCS or Google sheets without ingestion, called federated data
You can join data between google sheet and big query, can you join other type of data from GCS？
Loading data from GCS, can you load from Datastore?
Can stream data in using dataflow as well.

### {% post_link Cloud-Dataprep Dataprep %}

### {% post_link Cloud-Dataflow Dataflow %}

### {% post_link Cloud-Pub-Sub Pub/sub %}

### Datalab
python numpy panda

### TensorFlow
Python runs c++

### Cloud ML Engine

### ML APIs



