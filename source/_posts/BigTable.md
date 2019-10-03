---
title: BigTable
date: 2018-07-02 22:34:22
tags: [GCP, BigTable]
categories: [GCP, BigTable]
---

![bigtable](https://philsblog.b-cdn.net/images/bigtable.png "bigtable")

### feature summary
It's OLAP, so no transaction.
More expensive than bigqeury
Low latency, high throughput
100,000 QPS @ 6ms latency for 10-node cluster
You pay for the number of cluster
Global availability
Also separate computing and storage - the cluster only contains the pointer to the data, the data is remain on colossus, nodes only hold meta data
Data is stored on contiguous rows, as tablets, stored on GCS
Create the cluster first. You can add nodes, remove nodes without having any down time
Use Python or data flow, HBase client, HBase API, BigQuery 
Insert data by creating a mutation
Requests -> clients -> front-end server -> nodes
Switching between SSD and HDD storage
Good for ML continues training
You can use Cloud Dataproc to create one or more Compute Engine instances that can connect to a Cloud Bigtable instance and run Hadoop jobs. 
Bigtable tables are sparse; if a cell does not contain any data, it does not take up any space.

Support 4 dimention data model: rowkey, column family, column, timesstamp
Does this mean Bigtable support SCD?


Instance type: Production/Development, difference?
Prod - minimun 3 nodes
Dev - one single-node cluster
0.65/hr per node for both types

### rowKey
* sorted in a Ascding order
* unique id
* can be premitive, structure or array
* represent internally as byte array

columns can be added on the fly, however the column family cannot
### Read & write

### structure

Only one rowkey, none of the other columes can be indexed
Column family - related columns that tends to be updated together

## design
* Return adjacent rows as much as possible 
* distributed writing as much as possible
* distributed reads as much as possible

### Avoid hotspotting
* Field promotion - prefered
	avoids hotspotting in almost all cases and it tends to make it easier to desing a row key that facilitates queries
* Salting


#### Wide short vs narrow tall
Wide for dense data
Narrow for sparse data, e.g. user & follower
The row key should consist of the the most queried data

Query the data using:
* Row key
* Row prefix
* Row range

Rows are all sorted in ascending order. - from the lowest to the highest
Contiguous rowkeys will be stored on the same tablet, which make is quicker for searching. （you want the related entities are stored adjacently）
If you need the last few recored - then use reverse timestamp

Avoid Keyrow type examples :
* domains
* sequential IDs
* static, repeatedly updated identifiers

### Best practice

BigTable learns over time - have to leave BigTable up and running in a typical scenario. Let big query warm up for couple of hours and make sure you are not using BigTable for small amount of data(cannot be smaller than 300GB, recommended greater than 1T)
BigTable will re-balance the data - which allows imperfect row key design

### performance
should expect 
* 10000 query/ second at about 6 millisecond latency read and write on SSD
* 10000QPS 50 latency writing on HDD
* 500QPS at 200ms latency on HDD

The number of nodes is linearly related to performance
make sure the client and BigTable are in the same zone.

### Price
Pay for the nodes per hour
and the storage volumne used

### HDD vs SSD

SSD clusters: 2.5 TB per node
HDD clusters: 8 TB per node