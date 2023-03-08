---
title: MySQL 05：SQL 中的分析函数：SUM、AVG、MIN、MAX 和 COUNT
description: 
published: true
date: 2023-02-06T11:32:24.829Z
tags: 
editor: markdown
dateCreated: 2023-02-06T11:32:23.270Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [MySQL 05: Analytical functions in SQL: SUM, AVG, MIN, MAX, and COUNT***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-05-analytical-functions-in-sql-sum-avg-min-max-and-count)
{.links-list}


# MySQL 05：SQL 中的分析函数：SUM、AVG、MIN、MAX 和 COUNT

分析函数是 SQL 中用于处理数据的强大工具。在本文中，我们将了解如何使用 SUM、AVG、MIN、MAX 和 COUNT 函数来处理 MySQL 中的数据。

## 总和

SUM 函数用于返回一列数据的总和。例如，如果我们有一个包含数字列的数据表，我们可以使用 SUM 函数来获取该列中所有数字的总和：

```mysql
SELECT SUM(number_column)
FROM table_name;
```

## 平均值

AVG 函数用于返回一列数据的平均值。例如，如果我们有一个包含数字列的数据表，我们可以使用 AVG 函数来获取该列中所有数字的平均值：

```mysql
SELECT AVG(number_column)
FROM table_name;
```

## 分钟

MIN 函数用于返回一列数据的最小值。例如，如果我们有一个包含数字列的数据表，我们可以使用 MIN 函数来获取该列中的最小数字：

```mysql
SELECT MIN(number_column)
FROM table_name;
```

## 最大限度

MAX 函数用于返回一列数据的最大值。例如，如果我们有一个包含数字列的数据表，我们可以使用 MAX 函数来获取该列中的最大数字：

```mysql
SELECT MAX(number_column)
FROM table_name;
```

## 数数

COUNT 函数用于返回表中的行数。例如，如果我们有一个数据表，我们可以使用 COUNT 函数来获取该表中的行数：

```mysql
SELECT COUNT(*)
FROM table_name;
```

这些只是您可以在 SQL 中使用分析函数来处理数据的几种方法。有关更多信息，请查看以下资源。

## 资源

- [MySQL 文档：分析函数](https://dev.mysql.com/doc/refman/8.0/en/group-by-functions.html)
- [Stack Overflow：count(*)、count(1) 和 count(columnName) 之间有什么区别](https://stackoverflow.com/questions/3696867/what-is-the-difference-between-count- 1-and-count-columnname)
- [W3Schools：SQL 计数](https://www.w3schools.com/sql/sql_count.asp)