---
title: MySQL 07：SQL 中的数据聚合和报告：PIVOT 和 UNPIVOT
description: 
published: true
date: 2023-02-06T13:32:37.530Z
tags: 
editor: markdown
dateCreated: 2023-02-06T13:32:35.887Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [MySQL 07: Data aggregation and reporting in SQL: PIVOT and UNPIVOT***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-07-data-aggregation-and-reporting-in-sql-pivot-and-unpivot)
{.links-list}


MySQL 07：SQL 中的数据聚合和报告：PIVOT 和 UNPIVOT

在业务中，数据通常被汇总和报告以做出决策。例如，一家公司可能想知道每个地区销售了多少产品，以便更好地了解将资源分配到哪里。

在本文中，我们将学习如何使用 SQL PIVOT 和 UNPIVOT 运算符在 MySQL 中聚合和报告数据。

枢

PIVOT 运算符用于将行转换为列。它以一个包含行数据的表作为输入，并输出一个包含列数据的表。

要使用 PIVOT，我们首先需要指定要转换为行的列。我们可以使用 FOR 子句来做到这一点。例如，以下查询将 Region 和 Product 列转换为行：

```sql
SELECT *
FROM mytable
PIVOT (
  SUM(Sales)
  FOR Region IN ('East', 'West', 'North', 'South')
) AS pvt;
```

在上面的查询中，我们使用 SUM 函数来聚合 Sales 列。我们还使用 IN 子句指定要转换为列的值。

查询的输出将如下所示：

| |东 |西 |北 |南 |
| --- | --- | --- | --- | --- |
|产品A | 10 | 20 | 30 | 40 |
|产品B | 50 | 60 | 70 | 80 |

如果需要，我们还可以使用 AS 子句指定输出列的名称。在上面的示例中，我们为输出表使用了别名 pvt。

逆轴

UNPIVOT 运算符用于将列转换为行。它将包含列中数据的表作为输入，并输出包含行中数据的表。

要使用 UNPIVOT，我们首先需要指定要转换为行的列。我们可以使用 FOR 子句来做到这一点。例如，以下查询将 East、West、North 和 South 列转换为行：

```sql
SELECT *
FROM mytable
UNPIVOT (
  Sales
  FOR Region IN ('East', 'West', 'North', 'South')
) AS upvt;
```

在上面的查询中，我们使用 Sales 列作为 UNPIVOT 的输入。我们还使用 IN 子句指定要转换为行的值。

查询的输出将如下所示：

|地区 |销售 |
| --- | --- |
|东 | 10 |
|西 | 20 |
|北 | 30 |
|南 | 40 |

如果需要，我们还可以使用 AS 子句指定输出列的名称。在上面的示例中，我们为输出表使用了别名 upvt。

附加信息

PIVOT 和 UNPIVOT 运算符非常强大，可用于执行各种聚合和报告任务。

如果您有兴趣了解有关 PIVOT 和 UNPIVOT 的更多信息，我建议您查看以下资源：

- 关于 PIVOT 和 UNPIVOT 的 MySQL 文档
- 这篇关于 PIVOT 和 UNPIVOT 的优秀博文
- 关于 PIVOT 和 UNPIVOT 的 Stack Overflow 答案