---
title: Cloud Dataprep
date: 2018-06-29 07:52:10
tags: [GCP, Dataprep]
categories: [GCP, Dataprep]
---

![dataprep](https://philsblog.b-cdn.net/images/dataprep.png "dataprep")

Interactive graphical system for preparing structured or unstructured data for use in:
analytics -> BigQuery
visualisation -> Data Studio
train machine learning models -> 

Input integration : GCS, BigQuery and files
Dataprep offers a graphical user interface for interactively designing a pipeline
The elements are divided in to datasets, recipes and output

A dataset roughly translates into a Dataflow pipeline read, 
a recipe usually translates into multiple pipeline transformations.
and output translates into a pipeline action  
 
create Dataflow pipelines without coding
the pipeline can be output as a Dataflow Template for continued use in Dataflow
