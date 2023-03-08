---
title: 软件开发005：数据库管理
description: 
published: true
date: 2023-02-05T07:17:48.994Z
tags: 
editor: markdown
dateCreated: 2023-02-05T07:17:47.348Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Software Development 005: Database Management***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-005-database-management)
{.links-list}


## 软件开发 005：数据库管理

作为软件开发人员，对数据库管理有基本的了解很重要。在这篇文章中，我们将介绍数据库管理的基础知识，包括数据库类型的概述以及如何使用 SQL 编程语言查询数据库。

### 什么是数据库？

数据库是计算机可以访问的数据集合。数据库用于存储客户记录、产品库存和财务数据等信息。

有许多不同类型的数据库，但最常见的两种是关系数据库和非关系数据库。

关系数据库，例如 MySQL、Oracle 和 Microsoft SQL Server，将数据存储在表中。表类似于文件系统中的文件夹，其中每个表存储一组信息。

例如，客户表可能存储客户信息，如姓名、地址和电话号码。产品表可能存储产品信息，例如名称、价格和描述。

非关系数据库（例如 MongoDB 和 Cassandra）以未组织成表的格式存储数据。相反，非关系数据库以更灵活且更易于扩展的格式存储数据。

### 如何查询数据库

SQL 编程语言用于查询数据库。 SQL 是一种标准语言，被许多不同的数据库管理系统使用。

要查询数据库，您可以使用 SELECT 语句。 SELECT 语句用于从数据库中检索数据。

例如，以下 SQL 语句将从数据库中检索所有客户记录：

```sql
SELECT * FROM customers;
```

上述 SQL 语句中的星号 (\*) 是一个通配符，代表“全部”。因此，上面的 SQL 语句相当于说“从客户表中选择所有列和所有行”。

您还可以使用 SELECT 语句从数据库表中检索特定列。例如，以下 SQL 语句将从客户表中检索客户的姓名和地址：

```sql
SELECT name, address FROM customers;
```

您还可以在 SELECT 语句中使用 WHERE 子句来指定检索数据的条件。例如，以下 SQL 语句将检索客户所在州为“加利福尼亚”的所有客户记录：

```sql
SELECT * FROM customers WHERE state = 'California';
```

WHERE 子句通常与 ORDER BY 子句一起使用来对数据进行排序。例如，以下 SQL 语句将从客户表中检索所有客户记录，并按客户的姓氏对记录进行排序：

```sql
SELECT * FROM customers ORDER BY last_name;
```

ORDER BY 子句也可用于按相反顺序对数据进行排序。例如，以下 SQL 语句将从客户表中检索所有客户记录，并按客户姓氏倒序对记录进行排序：

```sql
SELECT * FROM customers ORDER BY last_name DESC;
```

上面 SQL 语句中的 DESC 关键字代表“降序”。因此，上面的 SQL 语句相当于说“从客户表中选择所有列和所有行，并按客户姓氏倒序对记录进行排序”。

您还可以在 SELECT 语句中使用 LIMIT 子句来指定要检索的记录数。例如，以下 SQL 语句将从客户表中检索前 10 条记录：

```sql
SELECT * FROM customers LIMIT 10;
```

LIMIT 子句通常与 OFFSET 子句一起使用来指定起始记录。例如，以下 SQL 语句将从 customers 表中的第 11 条记录开始检索 10 条记录：

```sql
SELECT * FROM customers LIMIT 10 OFFSET 10;
```

OFFSET 子句指定要跳过的记录数。因此，在上面的 SQL 语句中，OFFSET 子句表示跳过前 10 条记录并从第 11 条记录开始。

您还可以在 SELECT 语句中使用 LIKE 子句来搜索数据。 LIKE 子句通常与 % 通配符一起使用。 % 通配符可用于匹配任意数量的字符。

例如，以下 SQL 语句将检索客户姓氏以字母“S”开头的所有客户记录：

```sql
SELECT * FROM customers WHERE last_name LIKE 'S%';
```

上面的 SQL 语句表示从客户表中选择客户姓氏以字母“S”开头的所有列和所有行。

您还可以在 SELECT 语句中使用 IN 子句来指定值列表。例如，以下 SQL 语句将检索客户所在州为“加利福尼亚”或“德克萨斯”的所有客户记录：

```sql
SELECT * FROM customers WHERE state IN ('California', 'Texas');
```

上面的 SQL 语句表示从客户表中选择所有列和所有行，其中客户所在的州是“加利福尼亚”或“德克萨斯”。

您还可以在 SELECT 语句中使用 BETWEEN 子句来指定值的范围。例如，以下 SQL 语句将检索客户 ID 介于 1 和 10 之间的所有客户记录：

```sql
SELECT * FROM customers WHERE id BETWEEN 1 AND 10;
```

上面的 SQL 语句是说从客户表中选择客户 ID 在 1 到 10 之间的所有列和所有行。

您还可以在 SELECT 语句中使用 AND 和 OR 运算符来组合条件。例如，以下 SQL 语句将检索客户所在州为“加利福尼亚”且客户 ID 介于 1 和 10 之间的所有客户记录：

```sql
SELECT * FROM customers WHERE state = 'California' AND id BETWEEN 1 AND 10;
```

上面的 SQL 语句是说从 customers 表中选择所有列和所有行，其中客户的状态是“加利福尼亚”并且客户的 id 介于 1 和 10 之间。

您还可以在 SELECT 语句中使用 GROUP BY 子句对数据进行分组。例如，以下 SQL 语句将从客户表中检索所有客户记录，并按客户的状态对记录进行分组：

```sql
SELECT * FROM customers GROUP BY state;
```

上面的 SQL 语句是说从客户表中选择所有列和所有行，并按客户的状态对记录进行分组。

您还可以在 SELECT 语句中使用 HAVING 子句来指定分组数据的条件。例如，以下 SQL 语句将从客户表中检索所有客户记录，按客户所在的州对记录进行分组，并且仅包括拥有 10 个以上客户的州：

```sql
SELECT * FROM customers GROUP BY state HAVING count(*) > 10;
```

上面的 SQL 语句是说从 customers 表中选择所有列和所有行，按客户所在的州对记录进行分组，并且只包括拥有超过 10 个客户的州。

您还可以在 SELECT 语句中使用 COUNT 函数来统计记录数。例如，以下 SQL 语句将检索客户表中的客户记录数：

```sql
SELECT COUNT(*) FROM customers;
```

上面的 SQL 语句是说要选择 customers 表中的客户记录数。

您还可以在 SELECT 语句中使用 SUM 函数对列的值求和。例如，以下 SQL 语句将检索客户表中客户 ID 列的总和：

```sql
SELECT SUM(id) FROM customers;
```

上面的 SQL 语句是说选择 customers 表中 customer's id 列的总和。

您还可以在 SELECT 语句中使用 MIN 和 MAX 函数来查找列的最小值和最大值。例如，以下 SQL 语句将检索 customers 表中客户 id 列的最小值和最大值：

```sql
SELECT MIN(id), MAX(id) FROM customers;
```

上面的 SQL 语句是说选择 customers 表中 customer's id 列的最小值和最大值。

您还可以在 SELECT 语句中使用 AVG 函数来查找列的平均值。例如，以下 SQL 语句将检索 customers 表中客户 id 列的平均值：

```sql
SELECT AVG(id) FROM customers;
```

上面的 SQL 语句是说选择 customers 表中 customer's id 列的平均值。

### 附加信息

- [数据库管理系统](https://en.wikipedia.org/wiki/Database)
- [关系数据库管理系统](https://en.wikipedia.org/wiki/Relational_database_management_system)
- [非关系数据库管理系统](https://en.wikipedia.org/wiki/NoSQL)
- [SQL](https://en.wikipedia.org/wiki/SQL)
- [MySQL](https://www.mysql.com/)
- [甲骨文](https://www.oracle.com/database/)
- [Microsoft SQL Server](https://www.microsoft.com/en-us/sql-server/)
- [MongoDB](https://www.mongodb.com/)
- [卡桑德拉](https://cassandra.apache.org/)