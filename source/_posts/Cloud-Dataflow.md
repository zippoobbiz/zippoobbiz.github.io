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