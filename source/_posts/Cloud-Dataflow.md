---
title: Cloud Dataflow
date: 2018-06-30 14:54:28
tags: [GCP, Dataflow]
categories: [GCP, Dataflow]
---

{% qnimg dataflow.jpg %}

Dataflow TextIO.write will shard your file, you can avoid it by withoutSharding()

Dataflow can do everything you do in MapReduce
ParDo: parallel processing
should not contain any state
Process one item at a time
can do filtering
Extracting parts of input
calculating values from different parts of inputs


Map Vs FlatMap
Map: one input -> one output
FlatMap: to filter, only return the value needed

Combine Vs Group By
combine by key is faster and optimised by google
Group by is not balanced

### Major components
* Pipelines
* PCollection
* Transforms
* I/O Sources and Sinks 

### Cancel jobs
* Cancel
cancel it right away
* Drain
Dataflow service will immediately stop ingesting new data from input sources, but the Dataflow service will preserve any existing resources (such as worker instances) to finish processing and writing any buffered data in your pipeline.

### The Cloud Dataflow connector
Spanner
BigTable

Dataflow has built in R/W for BigQuery

### Windowing
default windowing behavior is to assign all elements of a PCollection to a single global window, even for unbounded PCollection

### Triggers
Type:
* Time-based triggers
	The default trigger is time based, it emit after the watermark passes the end of the window
	AfterWatermark
	AfterProcessingTime
* Data-driven triggers
* Composite triggers

### Access Control
 The Cloud Dataflow Worker role (roles/dataflow.worker) provides the permissions (dataflow.workItems.lease, dataflow.workItems.update, and dataflow.workItems.sendMessage) necessary for a Compute Engine service account to execute work units for a Cloud Dataflow pipeline. It should typically only be assigned to such an account, and only includes the ability to request and update work from the Cloud Dataflow service.

