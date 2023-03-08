---
title: 078：将 Spring Boot 与 Apache Cassandra 集成以进行分布式数据管理
description: 
published: true
date: 2023-02-05T09:32:41.412Z
tags: 
editor: markdown
dateCreated: 2023-02-05T09:32:39.730Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [078: Integrating Spring Boot with Apache Cassandra for Distributed Data Management***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/078-integrating-spring-boot-with-apache-cassandra-for-distributed-data-management)
{.links-list}


# 078：将 Spring Boot 与 Apache Cassandra 集成以进行分布式数据管理

## 介绍

在本文中，我们将探讨如何将 [Spring Boot](https://spring.io/projects/spring-boot) 与 [Apache Cassandra](http://cassandra.apache.org/) 集成以实现分布式数据管理。

Cassandra 是一个高度可扩展的 NoSQL 数据库，非常适合大规模数据存储和管理。 Spring Boot 是一种流行的 Java 框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序。

## 卡桑德拉概述

Cassandra 是一种 NoSQL 数据库，专为实现高可用性和可扩展性而设计。它是大规模数据存储和管理的流行选择。

Cassandra 是一个[无主](https://en.wikipedia.org/wiki/Masterless_architecture) 数据库，这意味着没有单点故障。数据在 Cassandra 集群中的多个节点之间进行复制，每个节点都可以作为一个[种子节点](http://docs.datastax.com/en/cassandra/3.x/cassandra/initialize/initializeSingleDS.html)用于其他节点。

Cassandra 也是[线性可扩展](https://en.wikipedia.org/wiki/Linear_scalability)，这意味着它可以通过向集群添加更多节点来处理不断增加的负载。

## 卡桑德拉数据模型

Cassandra 使用[面向列](https://en.wikipedia.org/wiki/Column-oriented_DBMS) 数据模型。数据被组织成[列族](http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlAboutDataModels.html)，类似于关系数据库中的表。

每个列族都有一个[主键](http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlPrimaryKeyConcept.html)，用于唯一标识一行数据。主键由一个或多个 [列](http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlColumns.html) 组成。

Cassandra还支持[二级索引](http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlIndexesConcept.html)，可用于通过列来查询列族中的数据不是主键的一部分。

## Cassandra 查询语言

Cassandra 使用一种称为 CQL（Cassandra 查询语言）的[类 SQL 查询语言](http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlSelect.html)，用于查询和更新 Cassandra 数据库中的数据。

CQL 类似于 SQL，但它不是完全兼容 SQL 的数据库。在使用 Cassandra 时，您应该注意 CQL 和 SQL 之间的一些[差异](http://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlCommandsTOC.html)。

## Spring 引导概述

[Spring Boot](https://spring.io/projects/spring-boot) 是一种流行的 Java 框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序。

Spring Boot基于[Spring框架](https://spring.io/projects/spring-framework)，这是一个流行的Java应用程序框架。 Spring Boot 通过提供 [默认配置](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html ) 和 [入门依赖项](https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started-maven-guides.html# getting-started-with-maven-dependency-management ) 可用于创建各种应用程序。

## Spring Boot 和 Cassandra

Spring Boot 使 [集成](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-nosql.html# boot-features-nosql-cassandra) 与 Cassandra 变得容易. Spring Boot 提供了一个 [Cassandra 自动配置](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-nosql.html#boot-features-nosql-cassandra)可用于配置和连接到 Cassandra 数据库。

Spring Boot 还提供了一个 [CassandraTemplate](https://docs.spring.io/spring-data/cassandra/docs/current/api/org/springframework/data/cassandra/core/CassandraTemplate.html) 对象，可以使用查询和更新 Cassandra 数据库中的数据。

## 入门

在本节中，我们将了解如何开始使用 Spring Boot 和 Cassandra。我们将首先使用 [Spring Initializr](https://start.spring.io/) 创建一个新的 Spring Boot 项目。

我们需要将以下依赖项添加到我们的项目中：

- Web - 用于向我们的应用程序添加 Web 服务器
- Cassandra - 用于连接到 Cassandra 数据库

我们还需要将以下 Maven 依赖项添加到我们的项目中：

- [Cassandra Driver](https://mvnrepository.com/artifact/org.apache.cassandra/cassandra-driver-core) - 用于连接到 Cassandra 数据库
- [Cassandra 单元](https://mvnrepository.com/artifact/org.cassandraunit/cassandra-unit) - 用于单元测试我们的 Cassandra 代码

## 配置卡桑德拉

在本节中，我们将了解如何为我们的 Spring Boot 应用程序配置 Cassandra。

我们将首先向我们的项目添加一个 [Cassandra 配置](https://docs.spring.io/spring-data/cassandra/docs/current/reference/html/# cassandra-configuration) 文件。该文件将用于配置我们的 Cassandra 连接。

我们需要在配置文件中设置以下属性：

- `cassandra.contact-points` - 我们的应用程序将用于连接到 Cassandra 集群的 Cassandra 联系点
- `cassandra.port` - 我们的 Cassandra 集群运行的端口
- `cassandra.keyspace-name` - 我们的应用程序将使用的键空间的名称
- `cassandra.username` - 我们的应用程序将用于连接到 Cassandra 的用户名
- `cassandra.password` - 我们的应用程序将用于连接到 Cassandra 的密码

## 创建一个 Cassandra 实体

在本节中，我们将了解如何创建 [Cassandra 实体](https://docs.spring.io/spring-data/cassandra/docs/current/reference/html/# cassandra-mapping-entity) 类.

Cassandra 实体类似于 [JPA 实体](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/# orm-support.jpa.entity)。它们用于将 Cassandra 表映射到 Java 类。

我们需要使用 @Table 注释来注释我们的 Cassandra 实体类。此注释用于指定我们的实体将映射到的 Cassandra 表的名称。

我们还需要使用 @PrimaryKeyClass 注释来注释我们的实体类。此注释用于指定我们实体的主键类。

我们的主键类需要为每个主键列添加“@PrimaryKeyColumn”注解。此注释用于指定列的名称以及列在主键中的使用顺序。

## 创建 Cassandra 存储库

在本节中，我们将了解如何创建 [Cassandra 存储库](https://docs.spring.io/spring-data/cassandra/docs/current/reference/html/# repositories.query-methods.details ） 界面。

Cassandra 存储库类似于 [JPA 存储库](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/# repositories)。它们用于访问 Cassandra 数据库中的数据。

我们需要使用“@Repository”注释来注释我们的 Cassandra 存储库接口。此注释用于将我们的接口标记为 Spring Data 存储库。

我们还需要使用 @CassandraRepository 注释来注释我们的存储库接口。此注释用于将我们的界面标记为 Cassandra 存储库。

我们可以在我们的存储库方法上使用“@Query”注释来指定 CQL 查询。我们还可以使用 @Param 注释将方法参数绑定到 CQL 查询参数。

## 单元测试 Cassandra 代码

在本节中，我们将了解如何对 Cassandra 代码进行单元测试。

我们将首先使用 @RunWith(CassandraUnitRunner.class) 注释来注释我们的测试类。此注释用于使用 Cassandra 单元运行器运行我们的单元测试。

我们还需要使用 @CassandraDataSet 注释来注释我们的测试类。此注释用于将 Cassandra 数据集加载到我们的测试环境中。

我们可以使用“@EmbeddedCassandra”注解启动嵌入式 Cassandra 服务器进行单元测试。我们还可以使用“@SharedEmbeddedCassandra”注解为我们的单元测试启动一个共享的嵌入式 Cassandra 服务器。

## 结论

在本文中，我们研究了如何将 Spring Boot 与 Cassandra 集成以进行分布式数据管理。我们首先了解了 Cassandra 数据模型和查询语言。然后我们研究了如何开始使用 Spring Boot 和 Cassandra。

然后我们研究了如何为我们的 Spring Boot 应用程序配置 Cassandra。我们还了解了如何创建 Cassandra 实体类和 Cassandra 存储库接口。

最后，我们了解了如何对 Cassandra 代码进行单元测试。