---
title: Common GCP command
date: 2018-07-18 09:28:59
tags:
---

GCP commands:

# app engine
gcloud app create
mvn appengine:deploy


# choose project
gcloud config list
gcloud config list account
gcloud config list project

gcloud config set project gcp-test-xxxxx
gcloud projects list

# Authentication & organizations
gcloud auth login
gcloud auth list
gcloud organizations list

