---
title: 085：使用 Spring Boot 和 Solr 构建搜索引擎
description: 
published: true
date: 2023-02-05T15:33:30.480Z
tags: 
editor: markdown
dateCreated: 2023-02-05T15:33:24.896Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [085: Building a Search Engine with Spring Boot and Solr***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/085-building-a-search-engine-with-spring-boot-and-solr)
{.links-list}


# 085：使用 Spring Boot 和 Solr 构建搜索引擎

在本文中，我们将向您展示如何使用 [Spring Boot](https://spring.io/projects/spring-boot) 和 [Apache Solr](https://lucene.apache.org) 构建搜索引擎/ 解决方案 /)。

## 什么是搜索引擎？

搜索引擎是一种基于 Web 的工具，使用户能够在 Internet 上查找信息。搜索引擎使用算法来抓取和索引网页，并使用启发式方法为用户提供相关的搜索结果。

有许多不同类型的搜索引擎，但最流行的是通用搜索引擎，如 Google、Yahoo 和 Bing。这些搜索引擎允许用户在 Internet 上搜索任何内容。

## 什么是 Apache Solr？

[Apache Solr](https://lucene.apache.org/solr/) 是一个流行的开源企业搜索平台，它建立在 [Apache Lucene](https://lucene.apache.org/) 之上。许多大型组织都在使用 Solr，包括 Adobe、CNET 和 eBay。

Solr 是一个独立的搜索服务器，它提供了一个类似 REST 的 API 来管理索引和搜索。 Solr 具有高度可扩展性，可以以分布式方式部署。

## 为什么使用 Solr？

使用 Solr 的原因有很多，但一些最流行的原因是：

- **Solr 是快速的**：Solr 旨在快速、低延迟和高吞吐量。
- **Solr 是可扩展的**：Solr 具有高度可扩展性，可以以分布式方式部署。
- **Solr 功能丰富**：Solr 提供了许多开箱即用的功能，包括全文搜索、分面搜索和命中突出显示。

## 先决条件

在我们开始之前，为了跟上这篇文章，您需要具备一些条件：

- **Java 8** 或更高版本：您可以从 [Oracle 网站](https://www.oracle.com/java/technologies/javase-downloads.html) 下载 Java。
- **Maven**：您可以从 [Apache Maven 网站](https://maven.apache.org/install.html) 安装 Maven。
- **Git**：您可以从 [Git 网站](https://git-scm.com/downloads) 安装 Git。

## 入门

在本节中，我们将逐步完成启动和运行搜索引擎所需的步骤。

### 第一步：创建一个Spring Boot项目

我们需要做的第一件事是创建一个新的 Spring Boot 项目。我们可以使用 [Spring Initializr](https://start.spring.io/) 来做到这一点。

我们需要指定以下信息：

- **Group**：这是我们项目的组 ID。我们将使用 com.example。
- **Artifact**：这是我们项目的工件 ID。我们将使用“搜索引擎”。
- **名称**：这是我们项目的名称。我们将使用“搜索引擎”。
- **描述**：这是我们项目的描述。我们将使用“使用 Spring Boot 和 Solr 构建的搜索引擎”。
- **包名称**：这是我们项目的包名称。我们将使用 com.example.search。
- **Packaging**：这是我们项目的包装类型。我们将使用 `jar`。
- **Java 版本**：这是我们项目的 Java 版本。我们将使用“8”。
- **Dependencies**：这些是我们项目的依赖项。我们需要添加以下依赖项：
  - `Web`：此依赖项增加了对 Web 开发的支持。
  - `Solr`：此依赖项增加了对 Apache Solr 的支持。

填写完所有信息后，我们可以单击“生成项目”按钮下载我们的项目。

### 第二步：配置Solr

接下来，我们需要配置 Solr。我们可以通过在我们项目的 `src/main/resources` 目录中创建一个名为 `solr.xml` 的文件来做到这一点。

`solr.xml` 文件应该如下所示：

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

在 `solr.xml` 文件中，我们将 Solr 配置为使用 [ZooKeeper](https://zookeeper.apache.org/) 进行协调，并且我们定义了具有单个副本的单个分片。

### 第 3 步：创建 Solr 核心

接下来，我们需要创建一个 Solr 核心。 Solr 核心是包含文档集合的 Solr 运行实例。

我们可以通过运行以下命令来创建 Solr 核心：

```
solr create -c <corename>
```

对于我们的示例，我们将使用名称“search-engine”。

### 第 4 步：配置 Spring Boot

现在我们已经创建了 Solr 核心，我们需要配置 Spring Boot 来使用它。我们可以通过将以下配置添加到 application.properties 文件来做到这一点：

```properties
spring.data.solr.host=http://localhost:8983/solr/search-engine
```

在配置中，我们指定了 Solr 核心的 URL。

### 第 5 步：创建文档

现在我们已经配置了 Solr 核心，我们可以向其中添加文档。文档是可以由 Solr 索引的信息单元。

我们将通过在 com.example.search.document 包中创建一个名为 SearchDocument 的新 Java 类来创建文档。 `SearchDocument` 类应该如下所示：

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

在“SearchDocument”类中，我们使用“@SolrDocument”注解对该类进行注解，以表明它是一个 Solr 文档。我们还使用“@Field”注释对“id”、“title”和“content”字段进行了注释，以指示它们应由 Solr 索引。

### 第 6 步：创建服务

现在我们已经创建了文档，我们需要创建一个可以索引它的服务。我们将在 com.example.search.service 包中创建一个名为 SearchService 的新 Java 接口。 `SearchService` 界面应该是这样的：

```java
package com.example.search.service;

import com.example.search.document.SearchDocument;

public interface SearchService {

    void indexDocument(SearchDocument document);

}
```

在“SearchService”接口中，我们定义了一个名为“indexDocument”的方法，它接受一个“SearchDocument”对象并为其编制索引。

接下来，我们将创建名为“SearchServiceImpl”的“SearchService”接口的实现。 `SearchServiceImpl` 类应该如下所示：

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

在 SearchServiceImpl 类中，我们注入了一个 SolrClient 对象。 `SolrClient` 对象用于与 Solr 服务器交互。

我们还实现了 indexDocument 方法。在 `indexDocument` 方法中，我们创建了一个 `SolrInputDocument` 对象并将 `SearchDocument` 对象中的字段添加到它。

最后，我们将 SolrInputDocument 添加到 SolrClient 并提交更改。

### 第 7 步：创建控制器

现在我们已经创建了我们的服务，我们需要创建一个可以索引文档的控制器。我们将在 com.example.search.controller 包中创建一个名为 SearchController 的新 Java 类。 `SearchController` 类应该如下所示：

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

在“SearchController”类中，我们注入了一个“SearchService”对象。我们还创建了一个名为“indexDocument”的“@PostMapping”注释方法，它接受一个“SearchDocument”对象。

在 indexDocument 方法中，我们调用了 SearchService 对象的 indexDocument 方法来索引文档。

### 第 8 步：构建并运行应用程序

现在我们已经创建了应用程序，我们可以构建并运行它。我们可以通过运行以下命令来完成此操作：

```
mvn spring-boot:run
```

应用程序启动并运行后，我们可以通过在请求正文中使用 `SearchDocument` 对象向 `/search` 端点发送 POST 请求来索引文档。

## 结论

在本文中，我们向您展示了如何使用 Spring Boot 和 Solr 构建搜索引擎。我们还向您展示了如何配置 Solr 以及如何索引文档。