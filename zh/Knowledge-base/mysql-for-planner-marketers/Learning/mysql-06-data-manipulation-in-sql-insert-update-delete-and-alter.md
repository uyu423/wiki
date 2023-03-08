---
title: MySQL 06：SQL 中的数据操作：INSERT、UPDATE、DELETE 和 ALTER
description: 
published: true
date: 2023-02-06T12:32:55.410Z
tags: 
editor: markdown
dateCreated: 2023-02-06T12:32:53.731Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [MySQL 06: Data manipulation in SQL: INSERT, UPDATE, DELETE, and ALTER***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-06-data-manipulation-in-sql-insert-update-delete-and-alter)
{.links-list}


MySQL 06：SQL 中的数据操作：INSERT、UPDATE、DELETE 和 ALTER
================================================ ==========

在本文中，我们将介绍使用 INSERT、UPDATE、DELETE 和 ALTER 语句在 SQL 中进行的数据操作。

### 插入

INSERT 语句用于将数据插入数据库表。 INSERT 的语法如下：

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

这里，```table_name``` 是要插入数据的表的名称，```(column1, column2, column3, ...)``` 是要插入数据的列的列表想插入数据。 ```VALUES (value1, value2, value3, ...)``` 是您要插入的值的列表。

请注意，您不必为表中的每一列都指定一个值。如果您没有为列指定值，则将使用该列的默认值。

下面是向表中插入数据的示例：

```sql
INSERT INTO products (name, price)
VALUES ('Widget', 9.99);
```

这将在“产品”表中插入一行，名称为“小部件”，价格为“9.99”。

您还可以一次将多行插入到表中：

```sql
INSERT INTO products (name, price)
VALUES ('Widget', 9.99),
       ('Gadget', 19.99),
       ('Doohickey', 29.99);
```

这将在 ```products``` 表中插入三行。

### 更新

UPDATE 语句用于更新数据库表中的数据。 UPDATE 的语法如下：

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, column3 = value3, ...
WHERE condition;
```

在这里，```table_name``` 是您要更新的表的名称，```SET column1 = value1, column2 = value2, column3 = value3, ...``` 是您想要的列的列表更新这些列的新值，而```WHERE 条件``` 是指定要更新哪些行的条件。

例如，以下语句将更新 ```products``` 表中所有行的 ```price``` 列，其中 ```name``` 是 ```Widget```：

```sql
UPDATE products
SET price = 11.99
WHERE name = 'Widget';
```

您还可以一次更新多个列：

```sql
UPDATE products
SET price = 11.99,
    name = 'NewWidget'
WHERE name = 'Widget';
```

### 删除

DELETE 语句用于从数据库表中删除数据。 DELETE 的语法如下：

```sql
DELETE FROM table_name
WHERE condition;
```

这里，```table_name``` 是要从中删除数据的表的名称，```WHERE 条件``` 是指定要删除哪些行的条件。

例如，以下语句将从 ```products``` 表中删除所有行，其中 ```name``` 是 ```Widget```：

```sql
DELETE FROM products
WHERE name = 'Widget';
```

### 改变

ALTER 语句用于修改数据库表的结构。 ALTER 的语法如下：

```sql
ALTER TABLE table_name
ADD column_name data_type;

ALTER TABLE table_name
MODIFY column_name data_type;

ALTER TABLE table_name
DROP column_name;
```

这里，```table_name``` 是要修改的表的名称，```ADD column_name data_type``` 向具有指定数据类型的表添加一个新列，```MODIFY column_name data_type`` ` 更改现有列的数据类型，而 ```DROP column_name``` 从表中删除一列。

例如，以下语句将向 ```products``` 表添加一个新的 ```price``` 列：

```sql
ALTER TABLE products
ADD price decimal(5,2);
```

以下语句会将 ```price``` 列的数据类型更改为 ```integer```：

```sql
ALTER TABLE products
MODIFY price integer;
```

附加信息
----------------------

在 SQL 中进行数据操作时，还需要注意以下几点：

* 如果您要将数据插入到具有```AUTO_INCREMENT``` 列的表中，您可以为该列指定```NULL``` 值，MySQL 将自动为其生成一个新值。

* 如果您要更新或删除数据，```WHERE``` 子句是可选的。如果省略```WHERE``` 子句，表中的所有行都将被更新或删除。

* 您可以将```ORDER BY``` 和```LIMIT``` 子句与```UPDATE``` 和```DELETE``` 语句一起使用，以指定要更新或删除的行。

* ```ALTER TABLE``` 语句可用于添加、修改或删除表中的列，以及添加或删除索引。

* 您可以使用 ```ALTER TABLE``` 语句更改表的名称。

外部资源
------------------

以下是一些外部资源，可用于进一步阅读 SQL 中的数据操作：

* [MySQL教程](https://dev.mysql.com/doc/refman/5.7/en/sql-tutorial.html)
* [SQL INSERT 语句](https://www.w3schools.com/sql/sql_insert.asp)
* [SQL更新语句](https://www.w3schools.com/sql/sql_update.asp)
* [SQL DELETE 语句](https://www.w3schools.com/sql/sql_delete.asp)
* [SQL ALTER TABLE 语句](https://www.w3schools.com/sql/sql_alter.asp)