---
title: 如何优化 SQL 查询以提高性能
description: 
published: true
date: 2023-02-01T15:57:43.155Z
tags: 
editor: markdown
dateCreated: 2023-02-01T15:57:41.548Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [How to Optimize SQL Queries for Improved Performance***English** version of this document is available*](/en/Knowledge-base/Common/how-to-optimize-sql-queries-for-improved-performance)
{.links-list}



# 如何优化 SQL 查询以提高性能

SQL 是一种功能强大的数据库查询语言，可用于检索、插入、更新和删除数据。但是，编写不当的 SQL 查询可能会导致性能问题。在本文中，我们将讨论如何优化 SQL 查询以提高性能。

## 为什么要优化 SQL 查询？

您想要优化 SQL 查询的原因有多种：

- 减少执行查询所需的时间
- 减少查询使用的资源量（例如 CPU、内存）
- 提高数据库的可扩展性

## 如何优化 SQL 查询

有多种技术可用于优化 SQL 查询。

### 使用正确的数据类型

设计数据库时，为列使用正确的数据类型很重要。这将确保数据被高效存储并且查询运行得更快。例如，如果您有一个存储日期的列，则应使用“DATE”数据类型而不是“VARCHAR”数据类型。

### 使用索引

索引可用于提高 SQL 查询的性能。索引是一种数据结构，用于按排序顺序将数据存储在表中。这使数据库更容易找到您要查找的数据。

要在表上创建索引，可以使用“CREATE INDEX”语句。例如，要在 `users` 表的 `id` 列上创建索引，您可以使用以下语句：

```sql
CREATE INDEX idx_users_id ON users(id);
```

您还可以在多个列上创建索引。例如，要在 `users` 表的 `first_name` 和 `last_name` 列上创建索引，您可以使用以下语句：

```sql
CREATE INDEX idx_users_first_name_last_name ON users(first_name, last_name);
```

请务必注意，您应该只在“WHERE”、“ORDER BY”和“GROUP BY”子句中经常使用的列上创建索引。在太多列上创建索引实际上会降低数据库的性能。

### 避免在 `WHERE` 子句中使用通配符

在 SQL 查询中使用 `WHERE` 子句时，应避免使用通配符（例如 `%`、`_`）。这是因为数据库必须扫描整个表才能找到您要查找的数据。例如，下面的查询将比没有通配符的查询花费更长的时间来执行：

```sql
SELECT * FROM users WHERE first_name LIKE '%John%';
```

### 避免在 `WHERE` 子句中使用 `OR`

在 SQL 查询中使用 WHERE 子句时，应避免使用 OR 运算符。这是因为数据库必须分别检查每个条件，这会减慢查询速度。例如，下面的查询将比没有 `OR` 运算符的查询花费更长的时间来执行：

```sql
SELECT * FROM users WHERE first_name = 'John' OR last_name = 'Smith';
```

### 使用 `LIMIT` 子句

从数据库中检索数据时，应使用“LIMIT”子句指定要检索的行数。这将有助于提高查询的性能，因为数据库不必从表中检索所有行。例如，以下查询只会从 `users` 表中检索 10 行：

```sql
SELECT * FROM users LIMIT 10;
```

### 使用 `EXPLAIN` 语句

`EXPLAIN` 语句可用于查看数据库将如何执行查询。这对于理解查询缓慢的原因以及找到优化查询的方法很有用。例如，以下查询将显示上面“SELECT”查询的执行计划：

```sql
EXPLAIN SELECT * FROM users LIMIT 10;
```

## 结论

在本文中，我们讨论了如何优化 SQL 查询以提高性能。我们已经看到，使用正确的数据类型、使用索引、避免在 WHERE 子句中使用通配符和 OR 运算符可以帮助提高 SQL 查询的性能。