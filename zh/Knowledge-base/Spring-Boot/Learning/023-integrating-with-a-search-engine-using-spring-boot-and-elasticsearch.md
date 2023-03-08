---
title: 023：使用 Spring Boot 和 Elasticsearch 与搜索引擎集成
description: 
published: true
date: 2023-02-03T15:32:38.215Z
tags: 
editor: markdown
dateCreated: 2023-02-03T15:32:36.511Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [023: Integrating with a search engine using Spring Boot and Elasticsearch***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/023-integrating-with-a-search-engine-using-spring-boot-and-elasticsearch)
{.links-list}


# 使用 Spring Boot 和 Elasticsearch 与搜索引擎集成

在本文中，我们将学习如何使用 Elasticsearch 将 Spring Boot 应用程序与搜索引擎集成。

## 什么是弹性搜索？

Elasticsearch 是一个基于 Apache Lucene 构建的分布式 RESTful 搜索和分析引擎。它提供了一组强大的功能，用于在大型数据集上实施全文搜索和分析。

## 为什么要使用 Elasticsearch？

Elasticsearch 因其易用性、可扩展性和性能而成为实现搜索引擎的热门选择。

## 设置弹性搜索

在开始使用 Elasticsearch 之前，我们需要对其进行设置。

有两种设置 Elasticsearch 的方法：

1. 从【官网】(https://www.elastic.co/downloads/elasticsearch)下载并安装Elasticsearch。
2. 使用[Docker镜像](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html)。

我们将在本文中使用 Docker 镜像。

## 运行 Elasticsearch

要运行 Elasticsearch Docker 镜像，请使用以下命令：

```
$ docker run -d -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.4.0
```

这将在端口 9200 上启动一个运行 Elasticsearch 7.4.0 的容器。

## 连接到弹性搜索

现在 Elasticsearch 已启动并运行，我们可以开始在我们的 Spring Boot 应用程序中使用它。

要从 Spring Boot 连接到 Elasticsearch，我们需要将以下依赖项添加到我们的 `pom.xml`：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-elasticsearch</artifactId>
</dependency>
```

此依赖项将添加必要的库，以便在我们的应用程序中连接和使用 Elasticsearch。

## 配置弹性搜索

一旦我们的项目中有了 spring-boot-starter-data-elasticsearch 依赖项，我们就需要配置 Elasticsearch。

我们可以通过将以下属性添加到我们的 application.properties 文件来配置 Elasticsearch：

```properties
spring.data.elasticsearch.cluster-nodes=localhost:9300
spring.data.elasticsearch.cluster-name=docker-cluster
```

这将配置我们的应用程序以连接到在 localhost:9300 上运行的 Elasticsearch 集群。

## 创建一个 Spring Boot 应用程序

现在我们已经设置和配置了 Elasticsearch，我们可以创建一个使用它的 Spring Boot 应用程序。

我们将从创建一个“User”类开始：

```java
@Document(indexName = "user", type = "user")
public class User {

    @Id
    private String id;

    private String name;

    private Integer age;

    // getters and setters
}
```

此类代表我们应用程序中的用户。请注意，我们已经用“@Document”对其进行了注释。这告诉 Spring Data Elasticsearch 这是一个应该在 Elasticsearch 中建立索引的文档。

我们还用 `@Id` 注释了 `id` 字段。这告诉 Spring Data Elasticsearch 这是该文档的唯一标识符。

接下来，我们将创建一个 `UserRepository` 接口：

```java
public interface UserRepository extends ElasticsearchRepository<User, String> {

}
```

这个接口扩展了 `ElasticsearchRepository`，它为我们提供了一组强大的方法来与 Elasticsearch 进行交互。

最后，我们将创建一个 UserService 类：

```java
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public void saveUser(User user) {
        userRepository.save(user);
    }

    public void deleteUser(User user) {
        userRepository.delete(user);
    }

    public Iterable<User> getAllUsers() {
        return userRepository.findAll();
    }

    public User getUserById(String id) {
        return userRepository.findById(id).orElse(null);
    }
}
```

此类提供在我们的应用程序中创建、检索和删除用户的方法。请注意，我们已经用“@Service”对其进行了注释。这告诉 Spring 这是一个应该由 Spring 容器管理的服务 bean。

我们还用 `@Autowired` 注释了 `userRepository` 字段。这告诉 Spring 在创建 bean 时将 `UserRepository` 的实例注入到该字段中。

## 创建和索引文档

现在我们已经设置了 Spring Boot 应用程序，我们可以开始在 Elasticsearch 中创建和索引文档。

我们将从创建一个 `User` 实例开始：

```java
User user = new User();
user.setId("1");
user.setName("John Doe");
user.setAge(20);
```

接下来，我们将把这个用户保存到我们的数据库中：

```java
userService.saveUser(user);
```

这会将用户保存到我们的数据库中，并在 Elasticsearch 中为文档编制索引。

## 搜索文档

一旦我们在 Elasticsearch 中索引了文档，我们就可以开始搜索它们了。

Elasticsearch 提供了一种强大的查询 DSL（领域特定语言）来搜索文档。

我们可以在我们的 UserRepository 上使用 search() 方法来执行搜索查询：

```java
SearchQuery searchQuery = new NativeSearchQueryBuilder()
        .withQuery(QueryBuilders.queryStringQuery("John Doe"))
        .build();

List<User> users = userRepository.search(searchQuery).getContent();
```

此查询将搜索包含短语“John Doe”的所有文档。

`search()` 方法返回一个 `SearchResponse` 对象，其中包含搜索查询的结果。我们可以使用 `getContent()` 方法获取与搜索查询匹配的 `User` 对象列表。

## 更新文件

我们也可以使用 Elasticsearch 来更新文档。

要更新文档，我们首先需要从数据库中检索它：

```java
User user = userService.getUserById("1");
```

接下来，我们将更新文档：

```java
user.setAge(21);
```

最后，我们将更新后的文档保存到数据库中：

```java
userService.saveUser(user);
```

这将更新数据库和 Elasticsearch 中的文档。

## 删除文档

我们也可以使用 Elasticsearch 来删除文档。

要删除文档，我们首先需要从数据库中检索它：

```java
User user = userService.getUserById("1");
```

接下来，我们将删除文档：

```java
userService.deleteUser(user);
```

这将从数据库和 Elasticsearch 中删除文档。

## 结论

在本文中，我们学习了如何使用 Elasticsearch 将 Spring Boot 应用程序与搜索引擎集成。我们还学习了如何在 Elasticsearch 中创建、索引、更新和删除文档。