---
title: MySQL 04: Advanced SQL techniques: JOIN, UNION, and subqueries
description: 
published: true
date: 2023-02-06T10:32:19.636Z
tags: 
editor: markdown
dateCreated: 2023-02-06T10:32:14.013Z
---

- [MySQL 04: Técnicas avanzadas de SQL: JOIN, UNION y subconsultas***Spanish** document is available*](/es/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-04-advanced-sql-techniques-join-union-and-subqueries)
{.links-list}
- [MySQL 04：高级 SQL 技术：JOIN、UNION 和子查询***Chinese Simplified** document is available*](/zh/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-04-advanced-sql-techniques-join-union-and-subqueries)
{.links-list}
- [MySQL 04: 고급 SQL 기술: JOIN, UNION 및 하위 쿼리***Korean** document is available*](/ko/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-04-advanced-sql-techniques-join-union-and-subqueries)
{.links-list}


MySQL is a powerful database management system used by millions of websites and applications. It offers a wide range of features and options to make working with data easy and efficient.

In this post, we'll take a look at some advanced SQL techniques that can be used to work with data in MySQL. We'll cover topics such as joins, unions, and subqueries. By the end of this post, you should have a good understanding of how to use these techniques to work with data in MySQL.

## Joins

A join is a way of combining data from two or more tables into a single result set. Joins are used to retrieve data from multiple tables.

There are different types of joins, but the most common type is the inner join. An inner join returns all rows from both tables that match the join condition.

Here's an example of an inner join:

```sql
SELECT *
FROM table1
INNER JOIN table2
ON table1.id = table2.id
```

In this example, we're joining two tables, table1 and table2, on the id column. The result of this query will be all rows from both tables that have the same id.

## Unions

A union is a way of combining data from two or more tables into a single result set. Unlike a join, a union does not require a join condition.

Here's an example of a union:

```sql
SELECT *
FROM table1
UNION
SELECT *
FROM table2
```

In this example, we're unioning two tables, table1 and table2. The result of this query will be all rows from both tables.

## Subqueries

A subquery is a query that is nested inside another query. A subquery is used to return data that is used by the outer query.

Here's an example of a subquery:

```sql
SELECT *
FROM table1
WHERE id IN (SELECT id
            FROM table2)
```

In this example, we're using a subquery to return all rows from table1 that have an id that is also in table2.