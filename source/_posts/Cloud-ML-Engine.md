---
title: Cloud ML Engine & Machine Learning & ML API
date: 2018-07-04 10:09:54
tags: [GCP, ML, Cloud ML Engine]
categories: [GCP, Cloud ML Engine]
---

Use python to run c++

### Scale tiers
* BASIC
* STANDARD_1
* PREMIUM_1
* BASIC_GPU
* BASIC_TPU
* CUSTOM

On GCP:
Collect data
- login APIs
- cloud pub-sub
- other real-time streaming

Organize data
- BigQuery
- Dataflow
- Machine learning processing SDK

Create model
- Tensorflow

Train & deploy model
- Cloud engine

### TensorFlow

* categorical_column_with_hash_bucket
Use it when we don't know the set of possible values in advance, each possible value in the feature column occupation will be hashed to an integer ID as we encounter them in training.
* categorical_column_with_identity
Use this when your inputs are integers in the range [0, num_buckets), and you want to use the input value itself as the categorical ID. Values outside this range will result in default_value if specified, otherwise it will fail.
* categorical_column_with_vocabulary_file/list
Use it when you know the set of all possible feature values of a column and there are only a few of them

Question:
tf.session()


### Wide & Deep learning
Wide for memorization: seagulls can fly, pigeons can fly
Deep for generalization: animals with wings can fly
One can combine the strengths of both.
It's useful for generic large-scale regression and classification problems with sparse inputs (categorical features with a large number of possible feature values), such as recommender systems, search, and ranking problems.

### Run a ML engine training job locally
```bash
gcloud ml-engine local train
```
This command runs the specified module in an environment similar to that of a live Cloud ML Engine Training Job.
This is especially useful in the case of testing distributed models, as it allows you to validate that you are properly interacting with the Cloud ML Engine cluster configuration.

### Type of ML
https://elitedatascience.com/machine-learning-algorithms
* Regressor
Suoervised learning task for modeling and predicting contiunuous, numeric variables. such as prediciting real=estate preices, stock priuces movements or student test scores.
* Classifier
Classification is supervised learning task for modeling and predicting categorical variables. Such as predicting employee churn, email spam, financial fraud, or student letter grades.
* Clustering estimator
Clustering is an unsupervised learning task for finding natural groupings of observations based on the inherent structure within your dataset. Such as customer segmentation, grouping similar items in e-commerce, and social network analysis.


* Supervised learning vs Unsupervised learning
* test cases with label or not.

### Online prediction vs batch prediction
* Online
Optimized to minimize the latency of serving predictions.
Predictions returned in the reponse message.
* Batch
Optimized to handle a high volume of instances in a job and to run more complex models.
Predictions written to output files in a Cloud Storage location that you specify.
https://cloud.google.com/ml-engine/docs/tensorflow/prediction-overview#online_prediction_versus_batch_prediction

### One-hot column
https://hackernoon.com/what-is-one-hot-encoding-why-and-when-do-you-have-to-use-it-e3c6186d008f

### Embedding
https://www.tensorflow.org/programmers_guide/embedding

### Hyperparameters
If model parameters are variables that get adjusted by training with existing data, your hyperparameters are the variables about the training process itself.
* Number of hidden layers
* Number of nodes in each hidden layer
* Learning rate


### Feature engineering
* base feature column - one of the raw columns in the original dataframe
* derived feature column - any new columns created based on some transformations defined over one or multiple base columns

Type:
* Bucketization
* Crossed feature columns

You could use bucketization to turn year of birth and income into categorical features, but thr raw conlumns are continuous.



### Error measurement
Regression: MSE
Classification: cross-entropy

### Performance evaluation
For unbalanced dataset
confusion matrix - to describe the performance 

![confusionMatrix](https://philsblog.b-cdn.net/images/confusionMatrix.png "confusionMatrix")

Accuracy when ML says “cat” —— 991 / 1000 - if balance
Precision = TP / (FP + FP) —— 1/1 - if unbalanced - accuracy when classifier says yes - things are common
Recall = TP / (TP + FN) —— 1/10- if unbalanced - Accuracy when the truth is yes - things are rare


### Prepare the dataset:
Good dataset should cover all cases, Ensure to include negative cases
But before you throw out the outliers, you need to first see whether if you can collect enough outliers, for some outliers:
- cannot just throw out it
- a better approach: why does this happen?
- reflect something about the data
- You want to make sure enough examples in the training dataset, so should keep it
- the fewer things you throw out, the more robust your model is

### splitting dataset
Original data split into:
training data
validation data
Test data

cross validation - change the split, take the average, if data is not enough

### ML APIs
Natural language API analyses
* Sentiment
* Category
* Entity
* Syntax


## Machine learning

### Overfitting
If our model does much better on the training set than on the test set, then we’re likely overfitting.

Reduce number of nodes or layers
Dropout or early stopping


bias and variance


### MapReduce vs Spark
Spark in memory, fast, 100 times faster than hadoop mapreduce, good for streaming
* Resilient Distributed Datasets
* can use disk
* near real-time analytics

MapReduce
* Persistent storage

## Question:
what is TextLineReader - read directly to graph
bucketized_column - discretizing a continuous variable
sparse_column_with_keys - encoding categorical data
