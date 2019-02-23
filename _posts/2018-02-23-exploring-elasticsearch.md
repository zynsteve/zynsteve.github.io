---
title: Exploring Elasticsearch
categories:
- Tutorial
tags:
- Search Engine
---


![Learning Elasticsearch](https://i0.wp.com/thecuriousdev.org/wp-content/uploads/2018/01/Elasticsearch-Logo-Color-V.jpg.png?fit=3422%2C1781&ssl=1)
## Introduction
> Elasticsearch is a distributed, RESTful search and analytics engine capable of solving a growing number of use cases. As the heart of the Elastic Stack, it centrally stores your data so you can discover the expected and uncover the unexpected.

Elasticsearch is a search seriver based on Lucene. It provides a distributed full-text search engine based on RESTful web API. Elasticsearch is developed with Java, and is deployed under Apache licence. It is a popular enterprise search engine.
<!-- more -->

## Why Elasticsearch
The disadvantages of relational database:
+ can not score
+ can not be distributed
+ can not parse complicated search request
+ low efficiency
+ can not tokenize

## Installation
### elasticsearch-rtf
Elasticsearch with built-in APIs.
#### download
```bash
git clone git://github.com/medcl/elasticsearch-rtf.git -b master --depth 1
```
#### run
```bash
cd elasticsearch/bin
./elasticsearch
```
#### open
[http://localhost:9200/](http://localhost:9200/)
![elasticsearch-rtf](/assets/images/post/exploring-elasticsearch/elasticsearch-rtf.png)
#### note:
add configurtions in elasticsearch-rtf/config/elasticsearch.yml
```yaml
http.cors.enabled: true
http.cors.allow-origin: "*"
http.cors.allow-methods: OPTIONS, HEAD, GET, POST, PUT, DELETE
http.cors.allow-headers: "X-Requested-With, Content-Type, Content-Length, X-User"
```

### elasticsearch-head
A web front end for an elastic search cluster.
#### download
```bash
git clone git://github.com/mobz/elasticsearch-head.git
```
#### run
```bash
cd elasticsearch-head
npm install
npm run start
```
#### open
[http://localhost:9100/](http://localhost:9100/)
![elasticsearch-head](/assets/images/post/exploring-elasticsearch/elasticsearch-head.png)

### Kibana
Kibana is an open source data visualization plugin for Elasticsearch. It provides visualization capabilities on top of the content indexed on an Elasticsearch cluster.
#### download
https://www.elastic.co/downloads/kibana
#### run
```bash
cd kibana/bin
./kibana
```
#### open
[http://localhost:5601/](http://localhost:5601/)
![kibana](/assets/images/post/exploring-elasticsearch/kibana.png)

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

### Comparsion with MySQL

|Elasticsearch|MySQL|
|---|---|
|index|database|
|type|table|
|document|row|
|field|column|

### HTTP Methods

|HTTP Verb|CRUD|Entire Collection (e.g. /customers)|Specific Item (e.g. /customers/{id})|
|-----|-----|-----|-----|
|POST|Create|201 (Created), 'Location' header with link to /customers/{id} containing new ID.|404 (Not Found), 409 (Conflict) if resource already exists..|
|GET|Read|200 (OK), list of customers. Use pagination, sorting and filtering to navigate big lists.|200 (OK), single customer. 404 (Not Found), if ID not found or invalid.|
|PUT|Update/Replace|405 (Method Not Allowed), unless you want to update/replace every resource in the entire collection.|200 (OK) or 204 (No Content). 404 (Not Found), if ID not found or invalid.|
|PATCH|Update/Modify|405 (Method Not Allowed), unless you want to modify the collection itself.|200 (OK) or 204 (No Content). 404 (Not Found), if ID not found or invalid.|
|DELETE|Delete|405 (Method Not Allowed), unless you want to delete the whole collection—not often desirable.|200 (OK). 404 (Not Found), if ID not found or invalid.|

### Inverted Index
Elasticsearch uses a structure called an inverted index, which is designed to allow very fast full-text searches. An inverted index consists of a list of all the unique words that appear in any document, and for each word, a list of the documents in which it appears.

For example, let’s say we have two documents, each with a content field containing the following:

The quick brown fox jumped over the lazy dog
Quick brown foxes leap over lazy dogs in summer
To create an inverted index, we first split the content field of each document into separate words (which we call terms, or tokens), create a sorted list of all the unique terms, and then list in which document each term appears. The result looks something like this:

|Term|Doc_1|Doc_2|
|---|---|---|
|quick||X|
|The|X|
|brown|X|X|
|dog|X||
|fox|X||
|in||X|
|jumped|X||
|lazy|X|X|
|leap||X|
|over|X|X|
|summer||X|
|the|X||

Now, if we want to search for quick brown, we just need to find the documents in which each term appears:

|Term|Doc_1|Doc_2|
|---|---|---|
|brown|X|X|
|quick|X||
|---|---|---|
|Total|2|1|

## Elasticsearch CRUD
### create
```
PUT linkedin/job/1
{
  "title": "Java Software Engineer",
  "salary": 150000,
  "company": {
    "name": "Magic Company",
    "address": "California"
  },
  "post_date": "02/15/2018",
  "application": 150
}
```
### get
```
GET linkedin/job/1?_source
```
### update
```
POST linkedin/job/1/_update
{
  "doc": {
    "salary": 200000
  }
}
```
### delete
```
DELETE linkedin/job/1
```

## Mapping
```
PUT linkedin
{
  "mappings": {
    "job": {
      "properties": {
        "title": {
          "store": true,
          "type": "text"
        },
        "company_name": {
          "store": true,
          "type": "keyword"
        },
        "description": {
          "type": "text"
        },
        "comments": {
          "type": "integer"
        },
        "post_date": {
          "type": "date",
          "format": "MM/dd/yyyy"
        }
      }
    }
  }
}
```

## Search
### match
```
GET linkedin/job/_search
{
  "query": {
    "match": {
      "title": "Java Developer"
    }
  }
}
```
### term
```
GET linkedin/job/_search
{
  "query": {
    "term": {
      "title": "Java"
    }
  }
}
```
