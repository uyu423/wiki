---
title: MySQL 06: Data manipulation in SQL: INSERT, UPDATE, DELETE, and ALTER
description: 
published: true
date: 2023-02-06T12:32:59.348Z
tags: 
editor: markdown
dateCreated: 2023-02-06T12:32:53.744Z
---

- [MySQL 06: manipulación de datos en SQL: INSERTAR, ACTUALIZAR, ELIMINAR y ALTERAR***Spanish** document is available*](/es/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-06-data-manipulation-in-sql-insert-update-delete-and-alter)
{.links-list}
- [MySQL 06：SQL 中的数据操作：INSERT、UPDATE、DELETE 和 ALTER***Chinese Simplified** document is available*](/zh/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-06-data-manipulation-in-sql-insert-update-delete-and-alter)
{.links-list}
- [MySQL 06: SQL에서 데이터 조작: INSERT, UPDATE, DELETE 및 ALTER***Korean** document is available*](/ko/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-06-data-manipulation-in-sql-insert-update-delete-and-alter)
{.links-list}


MySQL 06: Data manipulation in SQL: INSERT, UPDATE, DELETE, and ALTER
============================================================

In this post, we'll cover data manipulation in SQL using the INSERT, UPDATE, DELETE, and ALTER statements.

### INSERT

The INSERT statement is used to insert data into a database table. The syntax for INSERT is as follows:

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

Here, ```table_name``` is the name of the table into which you want to insert data, and ```(column1, column2, column3, ...)``` is a list of the columns into which you want to insert data. ```VALUES (value1, value2, value3, ...)``` is a list of the values you want to insert.

Note that you don't have to specify a value for every column in the table. If you don't specify a value for a column, the default value for that column will be used.

Here's an example of inserting data into a table:

```sql
INSERT INTO products (name, price)
VALUES ('Widget', 9.99);
```

This will insert a row into the ```products``` table with the name ```Widget``` and the price ```9.99```.

You can also insert multiple rows into a table at once:

```sql
INSERT INTO products (name, price)
VALUES ('Widget', 9.99),
       ('Gadget', 19.99),
       ('Doohickey', 29.99);
```

This will insert three rows into the ```products``` table.

### UPDATE

The UPDATE statement is used to update data in a database table. The syntax for UPDATE is as follows:

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, column3 = value3, ...
WHERE condition;
```

Here, ```table_name``` is the name of the table you want to update, ```SET column1 = value1, column2 = value2, column3 = value3, ...``` is a list of the columns you want to update and the new values for those columns, and ```WHERE condition``` is a condition that specifies which rows to update.

For example, the following statement will update the ```price``` column for all rows in the ```products``` table where the ```name``` is ```Widget```:

```sql
UPDATE products
SET price = 11.99
WHERE name = 'Widget';
```

You can also update multiple columns at once:

```sql
UPDATE products
SET price = 11.99,
    name = 'NewWidget'
WHERE name = 'Widget';
```

### DELETE

The DELETE statement is used to delete data from a database table. The syntax for DELETE is as follows:

```sql
DELETE FROM table_name
WHERE condition;
```

Here, ```table_name``` is the name of the table from which you want to delete data, and ```WHERE condition``` is a condition that specifies which rows to delete.

For example, the following statement will delete all rows from the ```products``` table where the ```name``` is ```Widget```:

```sql
DELETE FROM products
WHERE name = 'Widget';
```

### ALTER

The ALTER statement is used to modify the structure of a database table. The syntax for ALTER is as follows:

```sql
ALTER TABLE table_name
ADD column_name data_type;

ALTER TABLE table_name
MODIFY column_name data_type;

ALTER TABLE table_name
DROP column_name;
```

Here, ```table_name``` is the name of the table you want to modify, ```ADD column_name data_type``` adds a new column to the table with the specified data type, ```MODIFY column_name data_type``` changes the data type of an existing column, and ```DROP column_name``` deletes a column from the table.

For example, the following statement will add a new ```price``` column to the ```products``` table:

```sql
ALTER TABLE products
ADD price decimal(5,2);
```

And the following statement will change the data type of the ```price``` column to ```integer```:

```sql
ALTER TABLE products
MODIFY price integer;
```

Additional Information
----------------------

Here are some additional things to keep in mind when working with data manipulation in SQL:

* If you're inserting data into a table that has an ```AUTO_INCREMENT``` column, you can specify the ```NULL``` value for that column and MySQL will automatically generate a new value for it.

* If you're updating or deleting data, the ```WHERE``` clause is optional. If you omit the ```WHERE``` clause, all rows in the table will be updated or deleted.

* You can use the ```ORDER BY``` and ```LIMIT``` clauses with the ```UPDATE``` and ```DELETE``` statements to specify which rows to update or delete.

* The ```ALTER TABLE``` statement can be used to add, modify, or delete columns in a table, as well as to add or delete indexes.

* You can use the ```ALTER TABLE``` statement to change the name of a table.

External Resources
------------------

Here are some external resources for further reading on data manipulation in SQL:

* [MySQL Tutorial](https://dev.mysql.com/doc/refman/5.7/en/sql-tutorial.html)
* [SQL INSERT Statement](https://www.w3schools.com/sql/sql_insert.asp)
* [SQL UPDATE Statement](https://www.w3schools.com/sql/sql_update.asp)
* [SQL DELETE Statement](https://www.w3schools.com/sql/sql_delete.asp)
* [SQL ALTER TABLE Statement](https://www.w3schools.com/sql/sql_alter.asp)