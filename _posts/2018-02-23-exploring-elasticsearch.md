---
title: Exploring Elasticsearch
description: Exploring Elasticsearch.
categories:
 - Tutorial
tags:
 - Database
---


![Learning Elasticsearch](https://i0.wp.com/thecuriousdev.org/wp-content/uploads/2018/01/Elasticsearch-Logo-Color-V.jpg.png?fit=3422%2C1781&ssl=1)
## Introduction
> Elasticsearch is a distributed, RESTful search and analytics engine capable of solving a growing number of use cases. As the heart of the Elastic Stack, it centrally stores your data so you can discover the expected and uncover the unexpected.


## Key Concepts
### Node
It refers to a single running instance of Elasticsearch. Single physical and virtual server accommodates multiple nodes depending upon the capabilities of their physical resources like RAM, storage and processing power.

### Cluster
It is a collection of one or more nodes. Cluster provides collective indexing and search capabilities across all the nodes for entire data.

### Index
It is a collection of different type of documents and document properties. Index also uses the concept of shards to improve the performance. For example, a set of document contains data of a social networking application.

### Type
It is a collection of documents sharing a set of common fields present in the same index. For example, an Index contains data of a social networking application, and then there can be a specific type for user profile data, another type for messaging data and another for comments data.

### Document
It is a collection of fields in a specific manner defined in JSON format. Every document belongs to a type and resides inside an index. Every document is associated with a unique identifier, called the UID.

### Shard
Indexes are horizontally subdivided into shards. This means each shard contains all the properties of document, but contains less number of JSON objects than index. The horizontal separation makes shard an independent node, which can be store in any node. Primary shard is the original horizontal part of an index and then these primary shards are replicated into replica shards.

### Replicas
Elasticsearch allows a user to create replicas of their indexes and shards. Replication not only helps in increasing the availability of data in case of failure, but also improves the performance of searching by carrying out a parallel search operation in these replicas.
