---
title: MySQL 05: Analytical functions in SQL: SUM, AVG, MIN, MAX, and COUNT
description: 
published: true
date: 2023-02-06T11:32:28.899Z
tags: 
editor: markdown
dateCreated: 2023-02-06T11:32:23.305Z
---

- [MySQL 05: Funciones analíticas en SQL: SUM, AVG, MIN, MAX y COUNT***Spanish** document is available*](/es/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-05-analytical-functions-in-sql-sum-avg-min-max-and-count)
{.links-list}
- [MySQL 05：SQL 中的分析函数：SUM、AVG、MIN、MAX 和 COUNT***Chinese Simplified** document is available*](/zh/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-05-analytical-functions-in-sql-sum-avg-min-max-and-count)
{.links-list}
- [MySQL 05: SQL의 분석 함수: SUM, AVG, MIN, MAX 및 COUNT***Korean** document is available*](/ko/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-05-analytical-functions-in-sql-sum-avg-min-max-and-count)
{.links-list}


# MySQL 05: Analytical functions in SQL: SUM, AVG, MIN, MAX, and COUNT

Analytical functions are a powerful tool in SQL for working with data. In this post, we'll take a look at how to use the SUM, AVG, MIN, MAX, and COUNT functions to work with data in MySQL.

## SUM

The SUM function is used to return the sum of a column of data. For example, if we have a table of data with a column for numbers, we can use the SUM function to get the sum of all the numbers in that column:

```mysql
SELECT SUM(number_column)
FROM table_name;
```

## AVG

The AVG function is used to return the average of a column of data. For example, if we have a table of data with a column for numbers, we can use the AVG function to get the average of all the numbers in that column:

```mysql
SELECT AVG(number_column)
FROM table_name;
```

## MIN

The MIN function is used to return the minimum value of a column of data. For example, if we have a table of data with a column for numbers, we can use the MIN function to get the minimum number in that column:

```mysql
SELECT MIN(number_column)
FROM table_name;
```

## MAX

The MAX function is used to return the maximum value of a column of data. For example, if we have a table of data with a column for numbers, we can use the MAX function to get the maximum number in that column:

```mysql
SELECT MAX(number_column)
FROM table_name;
```

## COUNT

The COUNT function is used to return the number of rows in a table. For example, if we have a table of data, we can use the COUNT function to get the number of rows in that table:

```mysql
SELECT COUNT(*)
FROM table_name;
```

These are just a few of the ways you can use analytical functions in SQL to work with data. For more information, check out the resources below.

## Resources

- [MySQL Documentation: Analytical Functions](https://dev.mysql.com/doc/refman/8.0/en/group-by-functions.html)
- [Stack Overflow: What is the difference between count(*), count(1) and count(columnName)](https://stackoverflow.com/questions/3696867/what-is-the-difference-between-count-1-and-count-columnname)
- [W3Schools: SQL COUNT](https://www.w3schools.com/sql/sql_count.asp)