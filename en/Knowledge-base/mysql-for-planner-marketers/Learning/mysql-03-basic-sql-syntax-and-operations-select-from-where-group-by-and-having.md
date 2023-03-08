---
title: MySQL 03: Basic SQL syntax and operations: SELECT, FROM, WHERE, GROUP BY, and HAVING
description: 
published: true
date: 2023-02-06T09:32:22.552Z
tags: 
editor: markdown
dateCreated: 2023-02-06T09:32:20.863Z
---

- [MySQL 03: sintaxis y operaciones básicas de SQL: SELECT, FROM, WHERE, GROUP BY y HAVING***Spanish** document is available*](/es/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-03-basic-sql-syntax-and-operations-select-from-where-group-by-and-having)
{.links-list}
- [MySQL 03：基本 SQL 语法和操作：SELECT、FROM、WHERE、GROUP BY 和 HAVING***Chinese Simplified** document is available*](/zh/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-03-basic-sql-syntax-and-operations-select-from-where-group-by-and-having)
{.links-list}
- [MySQL 03: 기본 SQL 구문 및 작업: SELECT, FROM, WHERE, GROUP BY 및 HAVING***Korean** document is available*](/ko/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-03-basic-sql-syntax-and-operations-select-from-where-group-by-and-having)
{.links-list}


# MySQL 03: Basic SQL syntax and operations: SELECT, FROM, WHERE, GROUP BY, and HAVING

## Introduction

In this post, we'll cover the basic SQL syntax and operations for working with data in MySQL. We'll learn how to use the `SELECT`, `FROM`, `WHERE`, `GROUP BY`, and `HAVING` clauses to query data from a MySQL database.

## SELECT

The `SELECT` clause is used to specify the columns that you want to retrieve from a database table. For example, the following `SELECT` statement retrieves the `first_name` and `last_name` columns from the `employees` table:

```sql
SELECT first_name, last_name
FROM employees
```

If you want to retrieve all columns from a table, you can use the `*` character in place of the column list:

```sql
SELECT *
FROM employees
```

## FROM

The `FROM` clause is used to specify the table or tables that you want to retrieve data from. For example, the following `SELECT` statement retrieves data from the `employees` table:

```sql
SELECT first_name, last_name
FROM employees
```

You can specify multiple tables in the `FROM` clause by separating them with a comma:

```sql
SELECT first_name, last_name
FROM employees, departments
```

## WHERE

The `WHERE` clause is used to specify conditions for retrieving data from a database table. For example, the following `SELECT` statement retrieves data from the `employees` table where the `employee_id` is `1`:

```sql
SELECT first_name, last_name
FROM employees
WHERE employee_id = 1
```

You can use the `AND` and `OR` operators to specify multiple conditions in the `WHERE` clause:

```sql
SELECT first_name, last_name
FROM employees
WHERE employee_id = 1 OR employee_id = 2
```

## GROUP BY

The `GROUP BY` clause is used to group data from a database table. For example, the following `SELECT` statement retrieves data from the `employees` table and groups it by `department_id`:

```sql
SELECT department_id, count(*)
FROM employees
GROUP BY department_id
```

## HAVING

The `HAVING` clause is used to specify conditions for retrieving data from a database table. For example, the following `SELECT` statement retrieves data from the `employees` table where the `department_id` is `1`:

```sql
SELECT department_id, count(*)
FROM employees
GROUP BY department_id
HAVING department_id = 1
```

## Conclusion

In this post, we've covered the basic SQL syntax and operations for working with data in MySQL. We've learned how to use the `SELECT`, `FROM`, `WHERE`, `GROUP BY`, and `HAVING` clauses to query data from a MySQL database.