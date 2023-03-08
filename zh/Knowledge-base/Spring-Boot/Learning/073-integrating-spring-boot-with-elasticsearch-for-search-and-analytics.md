---
title: 073：将 Spring Boot 与 Elasticsearch 集成以进行搜索和分析
description: 
published: true
date: 2023-02-02T04:43:40.683Z
tags: 
editor: markdown
dateCreated: 2023-02-02T04:43:39.048Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [073: Integrating Spring Boot with Elasticsearch for Search and Analytics***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/073-integrating-spring-boot-with-elasticsearch-for-search-and-analytics)
{.links-list}


# 介绍

Elasticsearch 是一款功能强大的开源搜索和分析引擎，可让您轻松探索数据。 Spring Boot 是一种流行的 Java 应用程序框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序。

在本文中，我们将展示如何将 Spring Boot 与 Elasticsearch 集成以进行搜索和分析。我们将首先创建一个 Spring Boot 应用程序并添加所需的依赖项。然后我们将创建一个 Elasticsearch 索引并向其中添加一些数据。最后，我们将编写一个 Spring Boot 应用程序，它使用 Elasticsearch API 从索引中搜索和聚合数据。

# 先决条件

要跟进这篇文章，您需要具备以下条件：

- JDK 8 或更高版本
-摇篮4.0或更高版本

# 创建一个 Spring Boot 应用程序

我们将从创建一个 Spring Boot 应用程序开始。我们将使用 Spring Initializr 生成一个基本的项目结构。导航到 http://start.spring.io/ 并选择以下选项：

- 项目：摇篮项目
- 语言：Java
- 春季启动版本：2.0.3
- 项目元数据：
  - 组：com.example
  - 神器：spring-boot-elasticsearch
  - 名称：Spring Boot Elasticsearch
  - 描述：一个与Elasticsearch集成的Spring Boot应用
  - 包名：com.example.springbootelasticsearch
  - 包装：罐
  - Java 版本：8
  - 依赖：网络，龙目岛

单击“生成项目”以下载项目存档。提取存档并将项目导入您最喜欢的 IDE。

# 添加依赖

接下来，我们需要将所需的依赖项添加到我们的项目中。我们需要以下依赖项：

- Spring Data Elasticsearch：在Spring应用中提供对Elasticsearch的支持
- Elasticsearch：Elasticsearch 引擎本身
- Lombok：一个可以为我们生成样板代码的库

将以下依赖项添加到 `build.gradle` 文件的 `dependencies` 部分：

```groovy
dependencies {
    compile('org.springframework.boot:spring-boot-starter-data-elasticsearch')
    compile('org.elasticsearch:elasticsearch:6.3.2')
    compileOnly('org.projectlombok:lombok')
    testCompile('org.springframework.boot:spring-boot-starter-test')
}
```

# 配置弹性搜索

接下来，我们需要配置 Elasticsearch。默认情况下，Spring Boot 将在“http://localhost:9200”中查找 Elasticsearch 实例。如果您在不同的主机或端口上运行 Elasticsearch，您可以通过在 application.properties 中设置 spring.data.elasticsearch.cluster-nodes 和 spring.data.elasticsearch.cluster-name 属性来配置它文件。例如：

```properties
spring.data.elasticsearch.cluster-nodes=localhost:9300
spring.data.elasticsearch.cluster-name=my-cluster
```

# 创建弹性搜索索引

Elasticsearch 索引是具有相似特征的文档的集合。我们可以将索引视为关系数据库中的表。正如我们需要先创建一个表才能向其中插入数据一样，我们需要先创建一个索引才能向其中添加文档。

我们可以使用 Elasticsearch API 来创建索引。以下示例创建一个名为“customers”的索引，其中包含“name”和“address”字段：

```java
@Autowired
private ElasticsearchOperations operations;

@Test
public void testCreateIndex() {
    operations.createIndex(Customer.class);
}
```

# 添加数据到索引

创建索引后，我们可以向其中添加文档。文档是一个 JSON 对象，其中包含我们要索引的数据。在我们的示例中，我们将索引客户记录。每个客户记录都有一个“姓名”和一个“地址”。

我们可以使用 Elasticsearch API 来索引文档。以下示例为客户记录编制索引：

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

# 搜索索引

现在我们已经将一些数据添加到我们的索引中，我们可以搜索它了。我们可以使用 Elasticsearch API 来搜索文档。以下示例搜索名称为“John Smith”的客户记录：

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

# 聚合数据

除了搜索文档，我们还可以从索引中聚合数据。我们可以使用 Elasticsearch API 来运行聚合。以下示例按州聚合客户记录：

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

# 结论

在本文中，我们展示了如何将 Spring Boot 与 Elasticsearch 集成以进行搜索和分析。我们首先创建了一个 Spring Boot 应用程序并添加了所需的依赖项。然后我们创建了一个 Elasticsearch 索引并向其中添加了一些数据。最后，我们编写了一个 Spring Boot 应用程序，它使用 Elasticsearch API 从索引中搜索和聚合数据。