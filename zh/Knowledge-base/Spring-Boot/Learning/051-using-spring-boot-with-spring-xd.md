---
title: 051：将 Spring Boot 与 Spring XD 结合使用
description: 
published: true
date: 2023-02-04T17:32:31.246Z
tags: 
editor: markdown
dateCreated: 2023-02-04T17:32:29.566Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [051: Using Spring Boot with Spring XD***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/051-using-spring-boot-with-spring-xd)
{.links-list}


# 将 Spring Boot 与 Spring XD 结合使用

Spring Boot 是快速启动和运行 Spring 应用程序的好方法。它提供了许多开箱即用的功能，包括自动配置、嵌入式服务器和启动器依赖项。

Spring XD 是一个构建数据管道的工具。它可以从多个来源摄取数据，以各种方式处理数据，并将其输出到多个接收器。

在本文中，我们将学习如何将 Spring Boot 与 Spring XD 结合使用。我们将从一个简单的示例开始，该示例从文件中获取数据并将其输出到数据库。然后我们将探索 Spring XD 的一些更高级的特性。

## 先决条件

在我们开始之前，我们需要安装一些东西：

* [Java 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [Maven 3](https://maven.apache.org/download.cgi)
* [Spring Boot CLI](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/# getting-started-installing-the-cli)
* [春季 XD](https://spring.io/projects/spring-xd)

## 你好世界

让我们从一个简单的例子开始。我们将创建一个名为“data.txt”的文件，其中包含以下内容：

```
Hello, world!
```

接下来，我们将创建一个 Spring XD 流，从该文件中获取数据并将其输出到控制台。我们可以使用以下命令执行此操作：

```
xd:>stream create --name hello --definition "file --dir=./ --pattern=data.txt | log" --deploy
```

此流有两个组件：文件源和日志接收器。文件源配置为从 ./ 目录（当前目录）读取并查找具有 data.txt 模式的文件。日志接收器只是将数据输出到控制台。

我们可以看到使用以下命令运行的流：

```
xd:>stream list
```

我们可以使用以下命令查看流的输出：

```
xd:>log hello
```

## 数据库输出

在前面的示例中，我们将数据输出到控制台。但在许多情况下，我们希望将数据输出到数据库中。 Spring XD 使用 `jdbc` sink 使这变得容易。

首先，我们需要创建一个数据库。我们将使用 [H2](http://www.h2database.com/html/main.html)，这是一个可以在内存中运行的轻量级数据库。我们可以使用以下命令创建数据库：

```
xd:>jdbc create --name mydb --url jdbc:h2:mem:mydb
```

这将在内存中创建一个名为“mydb”的数据库。

接下来，我们需要在这个数据库中创建一个表。我们将使用以下 SQL：

```sql
CREATE TABLE messages (
  id IDENTITY,
  message VARCHAR(255)
);
```

我们可以使用以下命令执行此 SQL：

```
xd:>jdbc execute --name mydb --sql "CREATE TABLE messages (id IDENTITY, message VARCHAR(255))"
```

现在我们有一个数据库和一个表，我们可以创建一个流将数据输出到这个表。我们可以使用以下命令执行此操作：

```
xd:>stream create --name db --definition "file --dir=./ --pattern=data.txt | jdbc --name=mydb --tableName=messages --columns=message" --deploy
```

此流与前一个流类似，但它有一个 `jdbc` 接收器而不是 `log` 接收器。 `jdbc` 接收器配置为写入 `mydb` 数据库中的 `messages` 表。 `columns` 属性指定表中的哪些列应该用流中的数据填充。

我们可以使用以下 SQL 验证数据是否已插入数据库：

```sql
SELECT * FROM messages;
```

## 处理器

在前面的示例中，我们已经了解了如何从文件中获取数据并将其输出到控制台或数据库。但在许多情况下，我们希望在输出数据之前以某种方式对其进行处理。 Spring XD 使用处理器让这一切变得简单。

处理器可以以我们想要的任何方式转换数据。在此示例中，我们将创建一个将数据转换为大写的处理器。我们可以使用以下命令执行此操作：

```
xd:>processor create --name uppercase --definition "transform --expression=payload.toUpperCase()" --deploy
```

这个处理器有一个单一的“转换”模块。 `transform` 模块采用一个表达式，该表达式针对流中的每条数据进行评估。在这种情况下，表达式是 `payload.toUpperCase()`，它将数据转换为大写。

现在我们可以修改我们的 db 流来使用这个处理器：

```
xd:>stream create --name db --definition "file --dir=./ --pattern=data.txt | uppercase | jdbc --name=mydb --tableName=messages --columns=message" --deploy
```

我们可以使用以下 SQL 验证数据是否已插入数据库：

```sql
SELECT * FROM messages;
```

## 概括

在本文中，我们学习了如何将 Spring Boot 与 Spring XD 结合使用。我们已经了解了如何创建从文件中获取数据并将其输出到控制台或数据库的流。我们已经了解了如何使用处理器在数据输出之前对其进行转换。