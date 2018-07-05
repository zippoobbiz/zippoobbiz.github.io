---
title: GCP Data Engineer preparation
date: 2018-07-03 10:07:07
tags: [GCP, GCS, GCE, Cloud SQL, Dataproc, Datastore, BigTable, BigQuery, Datalab, TensorFlow, Cloud ML Engine, ML APIs]
categories: [GCP]
---

{% qnimg gcp.png %}

I am summarizing everything I have learned from GCP so far. It includes all of the resources I have found.
In this page, most of the content comes in bullet points format. Have a quick look through them, see if you can tell the story behind each of item. If you can, then you have a pretty good coverage for the GCP Data Engineer Cert. If you haven't heard of them, don't worry, you still have time, just google them or go to the sub page to find out more dertails. (There are some sub pages which will give you a bit more details of the things summarized in this page.)
Please just comment below if you found something missing from the exam and have fun!

### Why GCP? Why Cloud? 
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

Each zone is a physical data center
zone a b and c doesn’t means the geographical zone.- to make sure all your vms are at the same place, do deploy them in the same session

Highly durable, stores data redundantly, highly available, infinite scalability and consistent. Mainly used for storing binary or object data. Such as images, audio, video and backups.
Cloud storage offers different products for accessibility and archival.

* Multi-regional - Ideal for content that is required to be served across geographic regions.
* Regional - For use within a single region.
* Nearline - Used for data accessed less than once a month. (Archival solution, you may still be able to retrieve in less then a second)
* Coldline - Used for data access less than once a year (Archival solution, you may still be able to retrieve in less then a second)

Amazon Glacier may take hours

### Google Computer Engine
N1-standard-4
if only 60% of usage, get 15% discount
preemptible VM 80% discount (Not sure) others can take it away anytime
It's useful when you just want to run an ad hoc function that is not incorporated in to other GCP Paas products.
An instance can have only one service account.

### Cloud SQL
Single machine
Handle **gigabytes** of data
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

Highly scalable and managed NoSQL database. Highly Durable and Available. Supports ACID transactions (which is typical for most SQL data warehouse solutions), SQL-like queries.
Cloud datastore are mainly used for User profiles, such as social network profiles and game statuses.
Highly Scalable, automatic sharing and replication (Highly Available)
Supports ACID Transactions (consistent and durable)
SQL like queries
Can Update Attributes (or add Attributes which is like the columns and rows)

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


### Datalab
python numpy panda
Can use Python SQL JS to process data

### DataStudio 
data sources
* BigQuery
* MySQL
* CloudSQL
* Google Sheet
* Google analytics

need the right permission
live update
datastudio is stored on google drive
dimension X 
metrics  Y

### ML
gradient descent - walk down an error surface - doesn’t guaranteed to converge
learning rate - hyper parameter
epoch - a traversal through the entire training dataset
Weights - parameters we optimize
Batch size - the amount of data we compute error on
Evaluation - is the model good enough? Has to be done on full dataset
Training - gradient descent + evaluation

Neurons - one unit of combining inputs
Hidden layer - set of neutrons that operate on the same set of inputs
Inputs - What you feed into a neuron
Features -  transformation of inputs, such as x^2
Feature Engineering - coming up with what transformations to include
Softmax - normalize all input probabilities

Anything in ML model must be numeric

### TensorFlow
Python -> c++


### StackDriver functions 
* Debugger - allows you to inspect the state of a running application in real time without stopping or slowing it down. You can use it to see your code behavior in production.
* Error reporting - counts, analyzes and aggregates the crashes in your cloud services. You can see the errors in a management interface provided by Stackdriver. You can also receive emails and mobile alerts on new errors.
* Monitoring - provides an overview of performance, uptime and health of your cloud services. It collects metrics, events and metadata from GCP, AWS and other popular open source softwares. It ingests these metrics and displays them via a dashboard.
* Alerting - allows you to create policies to notify you when the health and uptime check results go over a certain limit. For example if uptime of a node is not over 98% alert you. The alerts can be notifications sent to Slack, Campfire, HipChat and PagerDuty.
* Tracing - Trace tracks how requests propagate through your application and receive detailed near real time performance insights. It auto analyses to generate latency reports to show you performance degradations on your VMs. What this means is that if your VM or app slows down tracing will pick this up.
* Logging - Logging allow you to store, search, analyst, monitor and alert on log data and events from GCP. Logging is fully-managed that can scale and ingest logs from thousands of VMs. You can also analyze this in real-time.

### IAM
Roles:
* predefined
* primitive
* custom

When you assign both predefined and primitive roles to a user, the permissions granted are a union of each role's permissions

Member types :
* Google account (Single person) 
* Service account (Not a person)
	can be used by services and applications running on your Google Compute Engine instance to interact with other Google Cloud Platform APIs
	An instance can have only one service account.
	Two types of service accounts are available to Compute Engine instances:
		- User-managed service accounts
		- Google-managed service accounts

* Google Group (Multiple people)

### Disk
Standard persistent disk vs SSD, is standard persistent disk HDD?
preemptible instance will self close after running 24 hours
Vm snapshots are used for backup operation or transfer of data, it’s a copy of the disk , snapshot already contains the os

### {% post_link Cloud-Dataprep Dataprep %}

### {% post_link Cloud-Dataflow Dataflow %}

### {% post_link Cloud-Pub-Sub Pub/sub %}


