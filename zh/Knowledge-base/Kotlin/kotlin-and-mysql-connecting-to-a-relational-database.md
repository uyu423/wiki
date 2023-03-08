---
title: Kotlin 和 MySQL：连接到关系数据库
description: 
published: true
date: 2023-02-17T03:17:44.522Z
tags: 
editor: markdown
dateCreated: 2023-02-17T03:17:42.071Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kotlin and MySQL: Connecting to a Relational Database***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-mysql-connecting-to-a-relational-database)
{.links-list}


# Kotlin 和 MySQL：连接到关系数据库

在本文中，我们将探讨如何从 Kotlin 连接到 MySQL 数据库。我们将了解如何配置数据库、编写代码来执行各种操作以及处理错误。

## 配置 MySQL

在开始编写代码之前，我们需要配置数据库。我们假设您已经在本地机器上安装并运行了 MySQL。如果没有，您可以在 [此处](https://dev.mysql.com/doc/refman/8.0/en/installing.html) 下载它。

MySQL 启动并运行后，我们需要创建一个数据库和一个 Kotlin 代码可以使用的用户。我们可以通过登录 MySQL 控制台来完成此操作：

```mysql
mysql> CREATE DATABASE kotlindb;
Query OK, 1 row affected (0.01 sec)

mysql> CREATE USER 'kotlinuser'@'localhost' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON kotlindb.* TO 'kotlinuser'@'localhost';
Query OK, 0 rows affected (0.00 sec)
```

## 连接到数据库

现在我们的数据库已经配置好了，我们可以编写一些 Kotlin 代码来连接它。我们将为 MySQL 使用 [JDBC 驱动程序](https://dev.mysql.com/doc/connector-j/8.0/en/)，您可以通过在构建中包含以下依赖项来将其添加到您的项目中.gradle` 文件：

```groovy
dependencies {
    implementation 'mysql:mysql-connector-java:8.0.21'
}
```

有了 JDBC 驱动程序，我们可以编写一个 Kotlin 函数来连接数据库：

```kotlin
fun connectToDatabase(): Connection? {
    val url = "jdbc:mysql://localhost:3306/kotlindb"
    val user = "kotlinuser"
    val password = "password"

    return try {
        DriverManager.getConnection(url, user, password)
    } catch (e: SQLException) {
        null
    }
}
```

此函数尝试使用我们之前配置的“url”、“user”和“password”连接到数据库。如果连接成功，它返回 `Connection` 对象。如果连接失败，它返回 `null`。

## 执行数据库操作

现在我们有了连接数据库的方法，我们可以开始编写代码来执行各种操作了。我们将从一个简单的示例开始：查询数据库以获取所有用户的列表。

首先，我们需要编写一个 SQL 查询：

```sql
SELECT * FROM users
```

接下来，我们将编写一个 Kotlin 函数来执行此查询：

```kotlin
fun getAllUsers(connection: Connection): List<User> {
    val sql = "SELECT * FROM users"
    val statement = connection.createStatement()
    val resultSet = statement.executeQuery(sql)

    val users = ArrayList<User>()

    while (resultSet.next()) {
        val id = resultSet.getInt("id")
        val name = resultSet.getString("name")
        val email = resultSet.getString("email")

        val user = User(id, name, email)
        users.add(user)
    }

    return users
}
```

此函数将“Connection”对象作为参数。然后它创建一个“Statement”对象并使用它来执行 SQL 查询。 `executeQuery` 方法返回一个 `ResultSet` 对象，其中包含查询的结果。

我们可以使用 ResultSet 对象的 next 方法来遍历结果。对于每个结果，我们创建一个 User 对象并将其添加到 users 列表中。最后，我们返回 `users` 列表。

## 处理错误

到目前为止，我们已经了解了如何连接到数据库并执行各种操作。但是，如果出现问题怎么办？例如，如果数据库宕机或 SQL 查询无效怎么办？

在 Kotlin 中，我们可以使用 `try`/`catch` 机制来处理错误。让我们修改 `getAllUsers` 函数以使用 `try`/`catch`：

```kotlin
fun getAllUsers(connection: Connection): List<User> {
    val sql = "SELECT * FROM users"

    return try {
        val statement = connection.createStatement()
        val resultSet = statement.executeQuery(sql)

        val users = ArrayList<User>()

        while (resultSet.next()) {
            val id = resultSet.getInt("id")
            val name = resultSet.getString("name")
            val email = resultSet.getString("email")

            val user = User(id, name, email)
            users.add(user)
        }

        users
    } catch (e: SQLException) {
        println("An error occurred while executing the SQL query: $sql")
        println(e.message)

        ArrayList()
    }
}
```

在这个版本的 getAllUsers 函数中，我们将代码包装在一个 try 块中。如果抛出 `SQLException`，将执行 `catch` 块中的代码。在这种情况下，我们只是打印一条错误消息。

需要注意的是，`try`/`catch` 机制只适用于处理可以恢复的错误。例如，如果数据库宕机了，我们无法从错误中恢复，所以 `try`/`catch` 将没有任何用处。

## 结论

在本文中，我们了解了如何从 Kotlin 连接到 MySQL 数据库。我们已经了解了如何配置数据库、编写代码来执行各种操作以及处理错误。