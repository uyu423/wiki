---
title: Hadoop
description: 
published: true
date: 2023-02-27T17:32:39.405Z
tags: 
editor: markdown
dateCreated: 2023-02-27T17:32:38.045Z
---

- [Hadoop***Korean** document is available*](/ko/Knowledge-base/Dictionary/hadoop)
{.links-list}


# Overview
Hadoop is an open-source software framework used for distributed storage and distributed processing of very large datasets on computer clusters. It is designed to scale up from single servers to thousands of machines, each offering local computation and storage.

# Description
Hadoop is a software framework for distributed storage and distributed processing of very large datasets on computer clusters built from commodity hardware. It provides a distributed file system (HDFS) and a framework for the analysis and transformation of very large datasets using the MapReduce programming model.

Hadoop works by breaking down a large dataset into smaller chunks, and then assigning each chunk to a node in the cluster. Each node processes its assigned chunk and sends the results back to the master node. The master node then combines all the results into a single output. This approach allows for the distributed processing of very large datasets across multiple nodes, and for the efficient use of computing resources.

Hadoop is designed to be highly scalable and fault tolerant. It can run on commodity hardware, and can scale from a single server to thousands of machines. It also provides built-in support for data replication, which helps to ensure that data is not lost in the event of a node failure.

Hadoop is widely used in the industry for a variety of tasks, such as web indexing, data mining, log processing, machine learning, and more. It is also used in the scientific community for research and analysis of large datasets.

# History
Hadoop was created by Doug Cutting and Mike Cafarella in 2005. It was initially developed as part of the Apache Nutch project, with the goal of providing a distributed computing platform for web search.

In 2006, Yahoo! adopted Hadoop as an internal platform for its web search indexing. This helped to popularize the technology, and led to the creation of the Apache Hadoop project in 2007.

Since then, Hadoop has become one of the most widely used distributed computing frameworks in the industry. It is used by organizations of all sizes, from small startups to large enterprises.

# Features
- Distributed Storage: Hadoop provides a distributed file system (HDFS) for storing data across multiple nodes in the cluster. It is designed for high throughput, scalability, and fault tolerance.

- Distributed Processing: Hadoop provides a framework for distributed processing of large datasets using the MapReduce programming model.

- Fault Tolerance: Hadoop is designed to be highly fault tolerant, with built-in support for data replication to ensure that data is not lost in the event of a node failure.

- Scalability: Hadoop is designed to scale from a single server to thousands of machines, each offering local computation and storage.

# Example
Hadoop is commonly used for processing large datasets in the industry. For example, it is used by companies such as Amazon, Facebook, and Twitter for data mining, web indexing, and log processing.

# Pros and Cons
Pros: 
- Highly scalable and fault tolerant
- Supports distributed storage and processing of large datasets
- Open source and widely used

Cons: 
- Difficult to set up and maintain
- Not suitable for real-time applications
- Performance can be unpredictable

# Related Technology
- Apache Spark: An open-source distributed computing framework that is built on top of Hadoop.

- Apache Flink: An open-source distributed streaming processing framework for real-time data processing.

- Apache Kafka: An open-source distributed streaming platform for building real-time data pipelines and streaming applications.