---
title: 061：将 Spring Boot 与 NoSQL 数据库集成
description: 
published: true
date: 2023-02-05T00:32:21.319Z
tags: 
editor: markdown
dateCreated: 2023-02-05T00:32:19.642Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [061: Integrating Spring Boot with NoSQL Databases***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/061-integrating-spring-boot-with-nosql-databases)
{.links-list}


# 061：将 Spring Boot 与 NoSQL 数据库集成

在本文中，我们将学习如何将 Spring Boot 应用程序与 NoSQL 数据库集成。

## 什么是 NoSQL？

NoSQL 是用于描述非关系数据库的术语。 NoSQL 数据库不使用大多数关系数据库使用的传统的基于表的关系模型。

NoSQL 数据库通常比关系数据库更具可扩展性和更易于使用。它们也非常适合存储大量数据，这些数据不容易构造成传统的基于表的模式。

## 为什么在 Spring Boot 中使用 NoSQL？

NoSQL 数据库是许多 Spring Boot 应用程序的不错选择。它们通常比关系数据库更具可扩展性和更易于使用。 Spring Boot 为 NoSQL 数据库提供了良好的支持，使您可以轻松地在应用程序中使用它们。

## 如何将 NoSQL 与 Spring Boot 集成

 Spring Boot 为 NoSQL 数据库提供了良好的支持。您可以将任何流行的 NoSQL 数据库与 Spring Boot 一起使用。在本文中，我们将使用 MongoDB 作为我们的 NoSQL 数据库。

MongoDB 是一种流行的 NoSQL 数据库，易于与 Spring Boot 一起使用。 Spring Boot 为 MongoDB 提供了一个启动器模块，使您可以轻松地在应用程序中使用 MongoDB。

要将 MongoDB 与 Spring Boot 一起使用，您需要将 spring-boot-starter-data-mongodb 启动模块添加到您的项目中。您可以使用以下 Maven 依赖项将此模块添加到您的项目中：

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

您还需要为您的应用程序配置 MongoDB。您可以通过将 MongoDB 配置文件添加到您的应用程序来完成此操作。下面是一个基本的 MongoDB 配置文件：

```properties
spring.data.mongodb.uri=mongodb://localhost/test
```

此配置文件告诉 Spring Boot 在默认端口 (27017) 上连接到本地主机上的 MongoDB 数据库。数据库名称是测试。

## 概括

在本文中，我们学习了如何将 Spring Boot 应用程序与 NoSQL 数据库集成。我们还了解了为什么您可能希望将 NoSQL 数据库与 Spring Boot 一起使用，以及如何使用 Spring Boot 配置 MongoDB。