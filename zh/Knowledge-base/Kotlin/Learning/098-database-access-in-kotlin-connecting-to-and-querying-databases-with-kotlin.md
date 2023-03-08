---
title: 098：Kotlin 中的数据库访问：使用 Kotlin 连接和查询数据库
description: 
published: true
date: 2023-02-09T06:17:13.885Z
tags: 
editor: markdown
dateCreated: 2023-02-09T06:17:12.237Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [098: Database Access in Kotlin: Connecting to and Querying Databases with Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/Learning/098-database-access-in-kotlin-connecting-to-and-querying-databases-with-kotlin)
{.links-list}


# Kotlin 中的数据库访问：使用 Kotlin 连接和查询数据库

在本文中，我们将了解如何使用 Kotlin 连接和查询数据库。我们将涵盖以下主题：

- 连接到数据库
- 创建和执行 SQL 语句
- 从数据库中检索结果

## 连接到数据库

为了连接到数据库，我们需要使用 JDBC 驱动程序。 Kotlin 带有一个内置的 JDBC 驱动程序，我们可以使用它来连接数据库。

要连接到数据库，我们首先需要创建一个 JDBC 连接。我们可以使用 JDBC DriverManager 类来做到这一点。 DriverManager 类提供了用于获取 JDBC 连接的静态方法。

一旦我们有了 JDBC 连接，我们就可以用它来创建一个 Statement 对象。 Statement 对象用于执行 SQL 语句。

## 创建和执行 SQL 语句

一旦我们有了一个 Statement 对象，我们就可以用它来执行 SQL 语句。我们可以使用两种方法来执行 SQL 语句：

- execute()：此方法执行 SQL 语句并返回一个布尔值，指示该语句是否为查询。
- executeQuery()：此方法执行 SQL 查询并返回包含查询结果的 ResultSet 对象。

## 从数据库中检索结果

如果我们使用 executeQuery() 方法执行 SQL 查询，我们将获得一个包含查询结果的 ResultSet 对象。

ResultSet 对象包含记录列表。每条记录都包含查询中列的值。

我们可以使用 ResultSet 对象从数据库中检索记录。我们可以使用 next() 方法移动到 ResultSet 中的下一条记录。我们可以使用 getString() 方法从当前记录中检索列的值。

一旦我们从数据库中检索到记录，我们就可以关闭 ResultSet 和 Statement 对象。最后，我们可以关闭 JDBC 连接。