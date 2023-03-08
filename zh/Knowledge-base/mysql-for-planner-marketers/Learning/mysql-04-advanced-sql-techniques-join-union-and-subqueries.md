---
title: MySQL 04：高级 SQL 技术：JOIN、UNION 和子查询
description: 
published: true
date: 2023-02-06T10:32:15.516Z
tags: 
editor: markdown
dateCreated: 2023-02-06T10:32:14.010Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [MySQL 04: Advanced SQL techniques: JOIN, UNION, and subqueries***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-04-advanced-sql-techniques-join-union-and-subqueries)
{.links-list}


MySQL 是一个强大的数据库管理系统，被数以百万计的网站和应用程序使用。它提供了广泛的功能和选项，使数据处理变得简单高效。

在本文中，我们将了解一些可用于在 MySQL 中处理数据的高级 SQL 技术。我们将涵盖连接、联合和子查询等主题。到本文结束时，您应该很好地理解如何使用这些技术来处理 MySQL 中的数据。

## 加入

联接是一种将两个或多个表中的数据组合到单个结果集中的方法。连接用于从多个表中检索数据。

联接有多种类型，但最常见的类型是内部联接。内部联接返回两个表中与联接条件匹配的所有行。

下面是一个内部连接的例子：

```sql
SELECT *
FROM table1
INNER JOIN table2
ON table1.id = table2.id
```

在此示例中，我们在 id 列上连接两个表，table1 和 table2。此查询的结果将是两个表中具有相同 ID 的所有行。

## 联盟

联合是一种将来自两个或多个表的数据组合成单个结果集的方法。与连接不同，联合不需要连接条件。

这是联合的示例：

```sql
SELECT *
FROM table1
UNION
SELECT *
FROM table2
```

在这个例子中，我们合并了两个表，table1 和 table2。此查询的结果将是两个表中的所有行。

## 子查询

子查询是嵌套在另一个查询中的查询。子查询用于返回外部查询使用的数据。

下面是一个子查询的例子：

```sql
SELECT *
FROM table1
WHERE id IN (SELECT id
            FROM table2)
```

在此示例中，我们使用子查询返回表 1 中具有也在表 2 中的 ID 的所有行。