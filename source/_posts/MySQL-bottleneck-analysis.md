---
title: MySQL bottleneck analysis
date: 2016-11-14 16:29:35
tags: [Tech, SQL]
categories: [Dev, SQL]
---

# Find bottleneck

![Alt text](http://og2api1gp.bkt.clouddn.com/static/images/bottleneck.png "Optional title")

### IOPS

> Input/output operations per second (IOPS, pronounced eye-ops) is a performance measurement used to characterize computer storage devices like hard disk drives (HDD), solid state drives (SSD), and storage area networks (SAN). – Wikipedia'

### IO

Any system that involves with storage has IO bottleneck. Databases are just some data files, so interacting with a database is an IO operation.

There are two situations when we are using MySQL, OLTP and OLAP. They is a difference regarding the aspect of using MySQL.

OLTP: On-line *Transaction* Processing, business, focus on concurrency.
OLAP: On-line *Analytical* Processing, log and data warehousing, focus on throughput.

There will be an option when you install MySQL on Windows.

![Alt text](http://og2api1gp.bkt.clouddn.com/static/images/sqloption.png "Optional title")

### CPU

Be careful when using *order * and *group by*, since both of them consume computing resources, which means more CPU usage.


### Network

In a distributed environment, each node between databases is more likely to become a bottleneck.

# When bottleneck detected

1) Hardware, OS, Network

* IO ( add more memory; improve IO performance)
* CPU (Multi-core)
* Network (MPLS）
