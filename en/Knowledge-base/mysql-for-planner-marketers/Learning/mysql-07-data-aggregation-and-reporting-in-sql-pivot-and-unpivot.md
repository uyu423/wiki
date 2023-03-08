---
title: MySQL 07: Data aggregation and reporting in SQL: PIVOT and UNPIVOT
description: 
published: true
date: 2023-02-06T13:32:41.487Z
tags: 
editor: markdown
dateCreated: 2023-02-06T13:32:35.890Z
---

- [MySQL 07: Agregación de datos y generación de informes en SQL: PIVOT y UNPIVOT***Spanish** document is available*](/es/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-07-data-aggregation-and-reporting-in-sql-pivot-and-unpivot)
{.links-list}
- [MySQL 07：SQL 中的数据聚合和报告：PIVOT 和 UNPIVOT***Chinese Simplified** document is available*](/zh/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-07-data-aggregation-and-reporting-in-sql-pivot-and-unpivot)
{.links-list}
- [MySQL 07: SQL의 데이터 집계 및 보고: PIVOT 및 UNPIVOT***Korean** document is available*](/ko/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-07-data-aggregation-and-reporting-in-sql-pivot-and-unpivot)
{.links-list}


MySQL 07: Data aggregation and reporting in SQL: PIVOT and UNPIVOT

In business, data is often aggregated and reported on in order to make decisions. For example, a company might want to know how many products were sold in each region in order to better understand where to allocate resources.

In this post, we'll learn how to use the SQL PIVOT and UNPIVOT operators to aggregate and report on data in MySQL.

PIVOT

The PIVOT operator is used to convert rows into columns. It takes as input a table with data in rows and outputs a table with data in columns.

To use PIVOT, we first need to specify the columns that we want to convert into rows. We can do this by using the FOR clause. For example, the following query converts the Region and Product columns into rows:

```sql
SELECT *
FROM mytable
PIVOT (
  SUM(Sales)
  FOR Region IN ('East', 'West', 'North', 'South')
) AS pvt;
```

In the query above, we're using the SUM function to aggregate the Sales column. We're also using the IN clause to specify the values that we want to convert into columns.

The output of the query will look like this:

| | East | West | North | South |
| --- | --- | --- | --- | --- |
| Product A | 10 | 20 | 30 | 40 |
| Product B | 50 | 60 | 70 | 80 |

If we want to, we can also specify the name of the output columns using the AS clause. In the example above, we've used the alias pvt for the output table.

UNPIVOT

The UNPIVOT operator is used to convert columns into rows. It takes as input a table with data in columns and outputs a table with data in rows.

To use UNPIVOT, we first need to specify the columns that we want to convert into rows. We can do this by using the FOR clause. For example, the following query converts the East, West, North, and South columns into rows:

```sql
SELECT *
FROM mytable
UNPIVOT (
  Sales
  FOR Region IN ('East', 'West', 'North', 'South')
) AS upvt;
```

In the query above, we're using the Sales column as the input for UNPIVOT. We're also using the IN clause to specify the values that we want to convert into rows.

The output of the query will look like this:

| Region | Sales |
| --- | --- |
| East | 10 |
| West | 20 |
| North | 30 |
| South | 40 |

If we want to, we can also specify the name of the output columns using the AS clause. In the example above, we've used the alias upvt for the output table.

Additional Information

The PIVOT and UNPIVOT operators are very powerful and can be used to perform a variety of aggregations and reporting tasks.

If you're interested in learning more about PIVOT and UNPIVOT, I recommend checking out the following resources:

- The MySQL documentation on PIVOT and UNPIVOT
- This excellent blog post on PIVOT and UNPIVOT
- This Stack Overflow answer on PIVOT and UNPIVOT