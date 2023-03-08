---
title: 073: Integrating Spring Boot with Elasticsearch for Search and Analytics
description: 
published: true
date: 2023-02-02T04:43:43.532Z
tags: 
editor: markdown
dateCreated: 2023-02-02T04:43:39.051Z
---

- [073: Integración de Spring Boot con Elasticsearch para búsqueda y análisis***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/073-integrating-spring-boot-with-elasticsearch-for-search-and-analytics)
{.links-list}
- [073：将 Spring Boot 与 Elasticsearch 集成以进行搜索和分析***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/073-integrating-spring-boot-with-elasticsearch-for-search-and-analytics)
{.links-list}
- [073: 검색 및 분석을 위해 Elasticsearch와 Spring Boot 통합***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/073-integrating-spring-boot-with-elasticsearch-for-search-and-analytics)
{.links-list}


# Introduction

Elasticsearch is a powerful open source search and analytics engine that makes data easy to explore. Spring Boot is a popular Java application framework that makes it easy to create stand-alone, production-grade Spring-based applications.

In this post, we'll show how to integrate Spring Boot with Elasticsearch for search and analytics. We'll first create a Spring Boot application and add the required dependencies. Then we'll create an Elasticsearch index and add some data to it. Finally, we'll write a Spring Boot application that uses the Elasticsearch APIs to search and aggregate data from the index.

# Prerequisites

To follow along with this post, you will need the following:

- JDK 8 or later
- Gradle 4.0 or later

# Creating a Spring Boot Application

We'll start by creating a Spring Boot application. We'll use the Spring Initializr to generate a basic project structure. Navigate to http://start.spring.io/ and select the following options:

- Project: Gradle Project
- Language: Java
- Spring Boot Version: 2.0.3
- Project Metadata:
  - Group: com.example
  - Artifact: spring-boot-elasticsearch
  - Name: Spring Boot Elasticsearch
  - Description: A Spring Boot application that integrates with Elasticsearch
  - Package Name: com.example.springbootelasticsearch
  - Packaging: Jar
  - Java Version: 8
  - Dependencies: Web, Lombok

Click "Generate Project" to download the project archive. Extract the archive and import the project into your favorite IDE.

# Adding Dependencies

Next, we need to add the required dependencies to our project. We'll need the following dependencies:

- Spring Data Elasticsearch: Provides support for Elasticsearch in Spring applications
- Elasticsearch: The Elasticsearch engine itself
- Lombok: A library that can generate boilerplate code for us

Add the following dependencies to the `dependencies` section of your `build.gradle` file:

```groovy
dependencies {
    compile('org.springframework.boot:spring-boot-starter-data-elasticsearch')
    compile('org.elasticsearch:elasticsearch:6.3.2')
    compileOnly('org.projectlombok:lombok')
    testCompile('org.springframework.boot:spring-boot-starter-test')
}
```

# Configuring Elasticsearch

Next, we need to configure Elasticsearch. By default, Spring Boot will look for an Elasticsearch instance at `http://localhost:9200`. If you have Elasticsearch running on a different host or port, you can configure it by setting the `spring.data.elasticsearch.cluster-nodes` and `spring.data.elasticsearch.cluster-name` properties in your `application.properties` file. For example:

```properties
spring.data.elasticsearch.cluster-nodes=localhost:9300
spring.data.elasticsearch.cluster-name=my-cluster
```

# Creating an Elasticsearch Index

An Elasticsearch index is a collection of documents that have similar characteristics. We can think of an index as a table in a relational database. Just as we need to create a table before we can insert data into it, we need to create an index before we can add documents to it.

We can use the Elasticsearch APIs to create an index. The following example creates an index named `customers` with the `name` and `address` fields:

```java
@Autowired
private ElasticsearchOperations operations;

@Test
public void testCreateIndex() {
    operations.createIndex(Customer.class);
}
```

# Adding Data to the Index

Once we have created an index, we can add documents to it. A document is a JSON object that contains the data that we want to index. In our example, we'll index customer records. Each customer record will have a `name` and an `address`.

We can use the Elasticsearch APIs to index documents. The following example indexes a customer record:

```java
@Autowired
private ElasticsearchOperations operations;

@Test
public void testIndex() {
    Customer customer = new Customer();
    customer.setName("John Smith");
    customer.setAddress("123 Main Street");

    operations.index(customer);
}
```

# Searching the Index

Now that we have added some data to our index, we can search it. We can use the Elasticsearch APIs to search for documents. The following example searches for customer records that have the name "John Smith":

```java
@Autowired
private ElasticsearchOperations operations;

@Test
public void testSearch() {
    QueryBuilder query = QueryBuilders.queryStringQuery("name:John Smith");
    SearchHits<Customer> customers = operations.search(query, Customer.class);

    assertEquals(1, customers.getTotalHits());
    assertEquals("John Smith", customers.getSearchHit(0).getContent().getName());
}
```

# Aggregating Data

In addition to searching for documents, we can also aggregate data from the index. We can use the Elasticsearch APIs to run aggregations. The following example aggregates customer records by state:

```java
@Autowired
private ElasticsearchOperations operations;

@Test
public void testAggregation() {
    QueryBuilder query = QueryBuilders.matchAllQuery();
    AggregationBuilder aggregation = AggregationBuilders.terms("by_state").field("address.state");
    SearchQuery searchQuery = new NativeSearchQueryBuilder()
            .withQuery(query)
            .withSearchType(SearchType.QUERY_THEN_FETCH)
            .withIndices("customers")
            .withTypes("customer")
            .addAggregation(aggregation)
            .build();

    Aggregations aggregations = operations.query(searchQuery, SearchResponse::getAggregations);
    StringTerms byStateAggregation = aggregations.get("by_state");
    assertEquals(2, byStateAggregation.getBuckets().size());
    assertEquals("CA", byStateAggregation.getBucketByKey("CA").getKeyAsString());
    assertEquals(1, byStateAggregation.getBucketByKey("CA").getDocCount());
    assertEquals("TX", byStateAggregation.getBucketByKey("TX").getKeyAsString());
    assertEquals(1, byStateAggregation.getBucketByKey("TX").getDocCount());
}
```

# Conclusion

In this post, we've shown how to integrate Spring Boot with Elasticsearch for search and analytics. We've first created a Spring Boot application and added the required dependencies. Then we've created an Elasticsearch index and added some data to it. Finally, we've written a Spring Boot application that uses the Elasticsearch APIs to search and aggregate data from the index.