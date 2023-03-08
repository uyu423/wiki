---
title: 085: Building a Search Engine with Spring Boot and Solr
description: 
published: true
date: 2023-02-05T15:33:26.678Z
tags: 
editor: markdown
dateCreated: 2023-02-05T15:33:24.904Z
---

- [085: Construcción de un motor de búsqueda con Spring Boot y Solr***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/085-building-a-search-engine-with-spring-boot-and-solr)
{.links-list}
- [085：使用 Spring Boot 和 Solr 构建搜索引擎***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/085-building-a-search-engine-with-spring-boot-and-solr)
{.links-list}
- [085: Spring Boot와 Solr로 검색 엔진 구축하기***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/085-building-a-search-engine-with-spring-boot-and-solr)
{.links-list}


# 085: Building a Search Engine with Spring Boot and Solr

In this post, we'll show you how to build a search engine using [Spring Boot](https://spring.io/projects/spring-boot) and [Apache Solr](https://lucene.apache.org/solr/).

## What is a Search Engine?

A search engine is a web-based tool that enables users to find information on the Internet. Search engines use algorithms to crawl and index web pages, and they use heuristics to provide relevant search results to users.

There are many different types of search engines, but the most popular ones are general-purpose search engines like Google, Yahoo, and Bing. These search engines allow users to search for anything on the Internet.

## What is Apache Solr?

[Apache Solr](https://lucene.apache.org/solr/) is a popular open source enterprise search platform that is built on top of [Apache Lucene](https://lucene.apache.org/). Solr is used by many large organizations, including Adobe, CNET, and eBay.

Solr is a stand-alone search server that provides a REST-like API for managing indexes and searching. Solr is highly scalable and can be deployed in a distributed fashion.

## Why Use Solr?

There are many reasons to use Solr, but some of the most popular ones are:

- **Solr is fast**: Solr is designed to be fast, with low latency and high throughput.
- **Solr is scalable**: Solr is highly scalable and can be deployed in a distributed fashion.
- **Solr is feature-rich**: Solr provides many features out of the box, including full-text search, faceted search, and hit highlighting.

## Prerequisites

Before we get started, there are a few things that you need to have in order to follow along with this post:

- **Java 8** or higher: You can download Java from the [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).
- **Maven**: You can install Maven from the [Apache Maven website](https://maven.apache.org/install.html).
- **Git**: You can install Git from the [Git website](https://git-scm.com/downloads).

## Getting Started

In this section, we'll walk through the steps necessary to get our search engine up and running.

### Step 1: Create a Spring Boot Project

The first thing we need to do is create a new Spring Boot project. We can do this using the [Spring Initializr](https://start.spring.io/).

We'll need to specify the following information:

- **Group**: This is the group ID for our project. We'll use `com.example`.
- **Artifact**: This is the artifact ID for our project. We'll use `search-engine`.
- **Name**: This is the name of our project. We'll use `Search Engine`.
- **Description**: This is the description of our project. We'll use `A search engine built with Spring Boot and Solr`.
- **Package Name**: This is the package name for our project. We'll use `com.example.search`.
- **Packaging**: This is the packaging type for our project. We'll use `jar`.
- **Java Version**: This is the Java version for our project. We'll use `8`.
- **Dependencies**: These are the dependencies for our project. We'll need to add the following dependencies:
  - `Web`: This dependency adds support for web development.
  - `Solr`: This dependency adds support for Apache Solr.

Once we have all of the information filled out, we can click the `Generate Project` button to download our project.

### Step 2: Configure Solr

Next, we need to configure Solr. We can do this by creating a file called `solr.xml` in the `src/main/resources` directory of our project.

The `solr.xml` file should look like this:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<solr>
  <solrcloud>
    <solrcloud>
      <zkHost>localhost:9983</zkHost>
    </solrcloud>
  </solrcloud>
  <shards>
    <shard>
      <name>shard1</name>
      <replicas>
        <replica>
          <name>replica1</name>
          <nodeName>node1</nodeName>
          <dataDir>data/shard1/replica1</dataDir>
        </replica>
      </replicas>
    </shard>
  </shards>
</solr>
```

In the `solr.xml` file, we've configured Solr to use [ZooKeeper](https://zookeeper.apache.org/) for coordination and we've defined a single shard with a single replica.

### Step 3: Create a Solr Core

Next, we need to create a Solr core. A Solr core is a running instance of Solr that contains a collection of documents.

We can create a Solr core by running the following command:

```
solr create -c <corename>
```

For our example, we'll use the name `search-engine`.

### Step 4: Configure Spring Boot

Now that we have our Solr core created, we need to configure Spring Boot to use it. We can do this by adding the following configuration to the `application.properties` file:

```properties
spring.data.solr.host=http://localhost:8983/solr/search-engine
```

In the configuration, we've specified the URL of our Solr core.

### Step 5: Create a Document

Now that we have our Solr core configured, we can add documents to it. A document is a unit of information that can be indexed by Solr.

We'll create a document by creating a new Java class called `SearchDocument` in the `com.example.search.document` package. The `SearchDocument` class should look like this:

```java
package com.example.search.document;

import org.apache.solr.client.solrj.beans.Field;
import org.springframework.data.annotation.Id;
import org.springframework.data.solr.core.mapping.SolrDocument;

@SolrDocument(solrCoreName = "search-engine")
public class SearchDocument {

    @Id
    @Field
    private String id;

    @Field
    private String title;

    @Field
    private String content;

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
    }
}
```

In the `SearchDocument` class, we've annotated the class with the `@SolrDocument` annotation to indicate that it is a Solr document. We've also annotated the `id`, `title`, and `content` fields with the `@Field` annotation to indicate that they should be indexed by Solr.

### Step 6: Create a Service

Now that we have our document created, we need to create a service that can index it. We'll create a new Java interface called `SearchService` in the `com.example.search.service` package. The `SearchService` interface should look like this:

```java
package com.example.search.service;

import com.example.search.document.SearchDocument;

public interface SearchService {

    void indexDocument(SearchDocument document);

}
```

In the `SearchService` interface, we've defined a single method called `indexDocument` that accepts a `SearchDocument` object and indexes it.

Next, we'll create an implementation of the `SearchService` interface called `SearchServiceImpl`. The `SearchServiceImpl` class should look like this:

```java
package com.example.search.service;

import com.example.search.document.SearchDocument;
import org.apache.solr.client.solrj.SolrClient;
import org.apache.solr.client.solrj.SolrServerException;
import org.apache.solr.common.SolrInputDocument;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.io.IOException;

@Service
public class SearchServiceImpl implements SearchService {

    @Autowired
    private SolrClient solrClient;

    @Override
    public void indexDocument(SearchDocument document) {
        SolrInputDocument solrInputDocument = new SolrInputDocument();
        solrInputDocument.addField("id", document.getId());
        solrInputDocument.addField("title", document.getTitle());
        solrInputDocument.addField("content", document.getContent());

        try {
            solrClient.add(solrInputDocument);
            solrClient.commit();
        } catch (SolrServerException | IOException e) {
            // log error
        }
    }
}
```

In the `SearchServiceImpl` class, we've injected a `SolrClient` object. The `SolrClient` object is used to interact with a Solr server.

We've also implemented the `indexDocument` method. In the `indexDocument` method, we've created a `SolrInputDocument` object and added the fields from the `SearchDocument` object to it.

Finally, we've added the `SolrInputDocument` to the `SolrClient` and committed the changes.

### Step 7: Create a Controller

Now that we have our service created, we need to create a controller that can index documents. We'll create a new Java class called `SearchController` in the `com.example.search.controller` package. The `SearchController` class should look like this:

```java
package com.example.search.controller;

import com.example.search.document.SearchDocument;
import com.example.search.service.SearchService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/search")
public class SearchController {

    @Autowired
    private SearchService searchService;

    @PostMapping
    public void indexDocument(@RequestBody SearchDocument document) {
        searchService.indexDocument(document);
    }

}
```

In the `SearchController` class, we've injected a `SearchService` object. We've also created a `@PostMapping` annotated method called `indexDocument` that accepts a `SearchDocument` object.

In the `indexDocument` method, we've called the `indexDocument` method on the `SearchService` object to index the document.

### Step 8: Build and Run the Application

Now that we have our application created, we can build and run it. We can do this by running the following command:

```
mvn spring-boot:run
```

Once the application is up and running, we can index a document by sending a POST request to the `/search` endpoint with a `SearchDocument` object in the request body.

## Conclusion

In this post, we've shown you how to build a search engine using Spring Boot and Solr. We've also shown you how to configure Solr and how to index documents.