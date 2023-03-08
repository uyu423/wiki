---
title: 009：将 Spring Boot 与 NoSQL 数据库 (MongoDB) 结合使用
description: 
published: true
date: 2023-02-03T08:36:55.375Z
tags: 
editor: markdown
dateCreated: 2023-02-03T08:36:50.432Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [009: Using Spring Boot with NoSQL databases (MongoDB)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/009-using-spring-boot-with-nosql-databases-mongodb)
{.links-list}


# 将 Spring Boot 与 NoSQL 数据库 (MongoDB) 结合使用

在本文中，我们将了解如何将 Spring Boot 与流行的 NoSQL 数据库 MongoDB 结合使用。

我们将涵盖以下主题：

* 什么是 MongoDB？
* 为什么在 Spring Boot 中使用 MongoDB？
* 设置 MongoDB
* 使用 MongoDB 创建 Spring Boot 应用程序
* 结论

## 什么是 MongoDB？

MongoDB 是一个功能强大的面向文档的 NoSQL 数据库。它具有基于索引的搜索功能和灵活的模式。 MongoDB 易于扩展，并因其高性能和可扩展性而广受欢迎。

## 为什么在 Spring Boot 中使用 MongoDB？

Spring Boot 是一种用于构建 Web 应用程序的流行 Java 框架。它建立在 Spring 框架之上，可以轻松创建独立的、生产级的基于 Spring 的应用程序。

MongoDB 是与 Spring Boot 一起使用的不错选择，因为它易于设置和使用。 MongoDB 还易于扩展，这对于预期增长的应用程序很重要。

## 设置 MongoDB

在我们可以将 MongoDB 与 Spring Boot 一起使用之前，我们需要对其进行设置。

设置 MongoDB 有两种方式：

* 使用像 MongoDB Atlas 这样的托管服务
* 在本地安装MongoDB

我们将在下面介绍这两个选项。

### 使用像 MongoDB Atlas 这样的托管服务

设置 MongoDB 的最简单方法是使用托管服务，如 MongoDB Atlas。 MongoDB Atlas 是一种云托管的 MongoDB 服务。它易于设置和使用。

要使用 MongoDB Atlas，您需要创建一个帐户并设置一个集群。集群是一组用于存储数据的 MongoDB 服务器。

创建帐户并设置集群后，您将需要创建用户。 Spring Boot 应用程序将使用该用户连接到 MongoDB 数据库。

创建用户后，您需要获取连接字符串。连接字符串用于将 Spring Boot 应用程序连接到 MongoDB 数据库。

### 在本地安装 MongoDB

如果您想在本地安装 MongoDB，可以按照 MongoDB 网站上的说明进行操作。

安装 MongoDB 后，您需要创建一个数据库。 Spring Boot 应用程序将使用该数据库来存储数据。

创建数据库后，您需要创建一个用户。 Spring Boot 应用程序将使用该用户连接到 MongoDB 数据库。

创建用户后，您需要获取连接字符串。连接字符串用于将 Spring Boot 应用程序连接到 MongoDB 数据库。

## 使用 MongoDB 创建 Spring Boot 应用程序

现在我们已经设置了 MongoDB，我们可以创建一个使用 MongoDB 的 Spring Boot 应用程序。

我们将从创建一个新的 Spring Boot 应用程序开始。我们称之为“spring-boot-mongodb”。

接下来，我们将以下依赖项添加到我们的项目中：

* spring-boot-starter-data-mongodb：此依赖项用于连接到 MongoDB 数据库。
* spring-boot-starter-web：这个依赖用于创建一个web应用。

我们还需要将以下属性添加到我们的 application.properties 文件中：

spring.data.mongodb.uri=mongodb://localhost/spring-boot-mongodb

此属性用于配置与我们的 MongoDB 数据库的连接。

接下来，我们将创建一个模型类。此类将用于表示我们的数据。我们称之为“用户”。

User 类将具有以下字段：

* id: 用户的id。该字段将由 MongoDB 生成。
* 名称：用户的名称。
* 电子邮件：用户的电子邮件。

接下来，我们将创建一个存储库接口。该接口将用于访问我们的数据。我们将其称为“UserRepository”。

UserRepository 接口将扩展 MongoRepository 接口。 MongoRepository 接口提供了 CRUD 操作的方法。

接下来，我们将创建一个控制器。该控制器将用于处理网络请求。我们称它为“UserController”。

UserController 类将具有以下方法：

* getAllUsers：此方法将用于获取所有用户。
* createUser：此方法将用于创建用户。
* getUser：此方法将用于通过 id 获取用户。
* updateUser：此方法将用于更新用户。
* deleteUser：此方法将用于删除用户。

最后，我们将创建一个服务类。此类将用于业务逻辑。我们将其称为“UserService”。

UserService 类将具有以下方法：

* getAllUsers：此方法将用于获取所有用户。
* createUser：此方法将用于创建用户。
* getUser：此方法将用于通过 id 获取用户。
* updateUser：此方法将用于更新用户。
* deleteUser：此方法将用于删除用户。

## 结论

在这篇文章中，我们研究了将 Spring Boot 与 MongoDB 结合使用。我们涵盖了以下主题：

* 什么是 MongoDB？
* 为什么在 Spring Boot 中使用 MongoDB？
* 设置 MongoDB
* 使用 MongoDB 创建 Spring Boot 应用程序