---
title: MySQL 03：基本 SQL 语法和操作：SELECT、FROM、WHERE、GROUP BY 和 HAVING
description: 
published: true
date: 2023-02-06T09:32:26.350Z
tags: 
editor: markdown
dateCreated: 2023-02-06T09:32:20.852Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [MySQL 03: Basic SQL syntax and operations: SELECT, FROM, WHERE, GROUP BY, and HAVING***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-03-basic-sql-syntax-and-operations-select-from-where-group-by-and-having)
{.links-list}


# MySQL 03：基本 SQL 语法和操作：SELECT、FROM、WHERE、GROUP BY 和 HAVING

## 介绍

在本文中，我们将介绍在 MySQL 中处理数据的基本 SQL 语法和操作。我们将学习如何使用 `SELECT`、`FROM`、`WHERE`、`GROUP BY` 和 `HAVING` 子句从 MySQL 数据库中查询数据。

## 选择

`SELECT` 子句用于指定要从数据库表中检索的列。例如，以下“SELECT”语句从“employees”表中检索“first_name”和“last_name”列：

```sql
SELECT first_name, last_name
FROM employees
```

如果要从表中检索所有列，可以使用“*”字符代替列列表：

```sql
SELECT *
FROM employees
```

## 从

`FROM` 子句用于指定要从中检索数据的一个或多个表。例如，以下 SELECT 语句从 employees 表中检索数据：

```sql
SELECT first_name, last_name
FROM employees
```

您可以在“FROM”子句中指定多个表，方法是用逗号分隔它们：

```sql
SELECT first_name, last_name
FROM employees, departments
```

## 在哪里

`WHERE` 子句用于指定从数据库表中检索数据的条件。例如，以下 SELECT 语句从 employees 表中检索数据，其中 employee_id 为 1：

```sql
SELECT first_name, last_name
FROM employees
WHERE employee_id = 1
```

您可以使用 `AND` 和 `OR` 运算符在 `WHERE` 子句中指定多个条件：

```sql
SELECT first_name, last_name
FROM employees
WHERE employee_id = 1 OR employee_id = 2
```

## 通过...分组

`GROUP BY` 子句用于对数据库表中的数据进行分组。例如，以下“SELECT”语句从“employees”表中检索数据并按“department_id”对其进行分组：

```sql
SELECT department_id, count(*)
FROM employees
GROUP BY department_id
```

## 有

`HAVING` 子句用于指定从数据库表中检索数据的条件。例如，以下“SELECT”语句从“department_id”为“1”的“employees”表中检索数据：

```sql
SELECT department_id, count(*)
FROM employees
GROUP BY department_id
HAVING department_id = 1
```

## 结论

在本文中，我们介绍了在 MySQL 中处理数据的基本 SQL 语法和操作。我们已经学习了如何使用 `SELECT`、`FROM`、`WHERE`、`GROUP BY` 和 `HAVING` 子句从 MySQL 数据库中查询数据。