---
title: Cloud Dataproc
date: 2018-07-01 09:06:11
tags: [GCP, Dataproc]
categories: [GCP, Dataproc]
---

{% qnimg gcp.png %}

Use dataproc process unstructured data, it takes care of all the over head and normally take 90 secs to spin up
Cheep storage Terabytes to Petabytes is good running it on cloud.
Use CLI and GC console to operate. The console and GC command make the same API call to operate.
Create clusters specifically for the job
Select zone next to your GCS
  why GCS?
* Don’t need to specify the storage size if store it on GCS
* moving HDFS to GSC allows you to use fewer persistent workers and more pre-emptable workers, HDFS cannot be run on pre-eemptable worker
* HDFS replicate 3 times to prevent nodes failure, no need to worry about it if store on GCS.

move to GCS:
* Copy local data to GCS
* Update file prefix from hfs:// to gs://
* Use Cloud Dataproc

Can dataproc read data from bigtable? bigquery?(via GCS, and big query connector, The connector to GCS is built into Dataproc)
standard mode vs high availability mode?

### Scaling
* Vertical scaling: larger computer
* horizontal scaling: more computers

horizontal is better but difficult

### Migrate your hadoop
If your hadoop :
reads and writes to a HBase, you can use bigTable
HDFS -> move to GCS
If read & write SQL -> bigQuery


### Spark & panda
Spark is declarative programming, the opposite one is called imperative programming
You tell the system what you want and it figures out how to implement it
use on-premise, cannot just add cluster, you need to rebalance the data

resilient distributed data sets RDDs - hide the complexity of the location of data within the cluster and also the complexity of the replication.
Spark partitions data and memory across the cluster and knows how to recover through an RTDD’s lineage should anything go wrong.

panda format is in memory, limited by size. Don’t use it as full-data, use it after aggregation
panda dataframe is mutabel, spark dataframe is immutable.

### Installation scripts
 
you can load multiple initialisation scripts to customise the software on dataproc worker and master
Dataproc is aware of new instances joining the cluster and make sure that they run the cluster’s initialisation scripts
may need to wait a few minutes after the cluster spin up
The scripts are designed for all nodes(including master and worker), you can specify the package to be installed for different ROLEs in the scripts
dataproc install datalab as default?

### Hadoop Eco system

##### Oozie
Oozie is a workflow scheduler system to manage Apache Hadoop jobs.

##### Sqoop
Transfers large amounts of data into hfs from relational databases such as MySQL. It is a transferring framework.

##### Pig
Pig is a high level scripting language that is used with Apache Hadoop. Pig enables data workers to write complex data transformations without knowing Java. Pig’s simple SQL-like scripting language is called Pig Latin, and appeals to developers already familiar with scripting languages and SQL.

##### Hive
Apache Hive is an open-source data warehouse system for querying and analyzing large datasets stored in HDFS.
Hive supports HiveQL which is like SQL, HiveQL is then translated to map-reduce jobs in the background.
Map-reduce is a data processing technique used commonly to extract, transform and load data on Hadoop



