---
title: 098: Database Access in Kotlin: Connecting to and Querying Databases with Kotlin
description: 
published: true
date: 2023-02-09T06:17:18.302Z
tags: 
editor: markdown
dateCreated: 2023-02-09T06:17:12.240Z
---

- [098: Acceso a la base de datos en Kotlin: conexión y consulta de bases de datos con Kotlin***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/098-database-access-in-kotlin-connecting-to-and-querying-databases-with-kotlin)
{.links-list}
- [098：Kotlin 中的数据库访问：使用 Kotlin 连接和查询数据库***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/098-database-access-in-kotlin-connecting-to-and-querying-databases-with-kotlin)
{.links-list}
- [098: Kotlin의 데이터베이스 액세스: Kotlin으로 데이터베이스 연결 및 쿼리***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/098-database-access-in-kotlin-connecting-to-and-querying-databases-with-kotlin)
{.links-list}


# Database Access in Kotlin: Connecting to and Querying Databases with Kotlin

In this post, we'll take a look at how to connect to and query databases using Kotlin. We'll cover the following topics:

- Connecting to a database
- Creating and executing SQL statements
- Retrieving results from a database

## Connecting to a Database

In order to connect to a database, we need to use a JDBC driver. Kotlin comes with a built-in JDBC driver, which we can use to connect to databases.

To connect to a database, we first need to create a JDBC connection. We can do this by using the JDBC DriverManager class. The DriverManager class provides static methods for getting a JDBC connection.

Once we have a JDBC connection, we can use it to create a Statement object. A Statement object is used to execute SQL statements.

## Creating and Executing SQL Statements

Once we have a Statement object, we can use it to execute SQL statements. There are two methods that we can use to execute SQL statements:

- execute(): This method executes an SQL statement and returns a boolean value that indicates whether the statement is a query or not.
- executeQuery(): This method executes an SQL query and returns a ResultSet object that contains the results of the query.

## Retrieving Results from a Database

If we use the executeQuery() method to execute an SQL query, we'll get a ResultSet object that contains the results of the query.

A ResultSet object contains a list of records. Each record contains the values of the columns in the query.

We can use the ResultSet object to retrieve the records from the database. We can use the next() method to move to the next record in the ResultSet. We can use the getString() method to retrieve the value of a column from the current record.

Once we've retrieved the records from the database, we can close the ResultSet and the Statement objects. Finally, we can close the JDBC connection.