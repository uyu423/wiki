---
title: Kotlin 및 MySQL: 관계형 데이터베이스에 연결
description: 
published: true
date: 2023-02-17T03:17:43.798Z
tags: 
editor: markdown
dateCreated: 2023-02-17T03:17:42.070Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and MySQL: Connecting to a Relational Database***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-mysql-connecting-to-a-relational-database)
{.links-list}


# Kotlin과 MySQL: 관계형 데이터베이스에 연결하기

이 문서에서는 Kotlin에서 MySQL 데이터베이스에 연결하는 방법을 살펴보겠습니다. 데이터베이스를 구성하고 다양한 작업을 수행하는 코드를 작성하고 오류를 처리하는 방법을 살펴보겠습니다.

## MySQL 구성

코드 작성을 시작하기 전에 데이터베이스를 구성해야 합니다. 로컬 컴퓨터에 MySQL이 설치되어 실행 중이라고 가정합니다. 그렇지 않은 경우 [여기](https://dev.mysql.com/doc/refman/8.0/en/installing.html)에서 다운로드할 수 있습니다.

MySQL이 실행되고 나면 Kotlin 코드에서 사용할 수 있는 데이터베이스와 사용자를 생성해야 합니다. MySQL 콘솔에 로그인하여 이를 수행할 수 있습니다.

```mysql
mysql> CREATE DATABASE kotlindb;
Query OK, 1 row affected (0.01 sec)

mysql> CREATE USER 'kotlinuser'@'localhost' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON kotlindb.* TO 'kotlinuser'@'localhost';
Query OK, 0 rows affected (0.00 sec)
```

## 데이터베이스에 연결

이제 데이터베이스가 구성되었으므로 여기에 연결할 Kotlin 코드를 작성할 수 있습니다. MySQL용 [JDBC 드라이버](https://dev.mysql.com/doc/connector-j/8.0/en/)를 사용하겠습니다. `빌드에 다음 종속성을 포함하여 프로젝트에 추가할 수 있습니다. .gradle` 파일:

```groovy
dependencies {
    implementation 'mysql:mysql-connector-java:8.0.21'
}
```

JDBC 드라이버가 있으면 Kotlin 함수를 작성하여 데이터베이스에 연결할 수 있습니다.

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

이 함수는 앞에서 설정한 `url`, `user` 및 `password`를 사용하여 데이터베이스에 연결을 시도합니다. 연결에 성공하면 `Connection` 개체를 반환합니다. 연결에 실패하면 `null`을 반환합니다.

## 데이터베이스 작업 수행

이제 데이터베이스에 연결할 방법이 있으므로 다양한 작업을 수행하는 코드 작성을 시작할 수 있습니다. 모든 사용자 목록에 대해 데이터베이스를 쿼리하는 간단한 예부터 시작하겠습니다.

먼저 SQL 쿼리를 작성해야 합니다.

```sql
SELECT * FROM users
```

다음으로 이 쿼리를 실행하는 Kotlin 함수를 작성합니다.

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

이 함수는 `Connection` 개체를 매개변수로 사용합니다. 그런 다음 'Statement' 객체를 생성하고 이를 사용하여 SQL 쿼리를 실행합니다. `executeQuery` 메서드는 쿼리 결과를 포함하는 `ResultSet` 개체를 반환합니다.

`ResultSet` 개체의 `next` 메서드를 사용하여 결과를 반복할 수 있습니다. 각 결과에 대해 `User` 객체를 생성하고 `users` 목록에 추가합니다. 마지막으로 `users` 목록을 반환합니다.

## 오류 처리

지금까지 데이터베이스에 연결하고 다양한 작업을 수행하는 방법을 살펴보았습니다. 하지만 문제가 발생하면 어떻게 됩니까? 예를 들어 데이터베이스가 다운되었거나 SQL 쿼리가 유효하지 않은 경우 어떻게 됩니까?

Kotlin에서는 `try`/`catch` 메커니즘을 사용하여 오류를 처리할 수 있습니다. `try`/`catch`를 사용하도록 `getAllUsers` 함수를 수정해 보겠습니다.

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

이 버전의 `getAllUsers` 함수에서는 `try` 블록에 코드를 래핑했습니다. `SQLException`이 발생하면 `catch` 블록의 코드가 실행됩니다. 이 경우에는 단순히 오류 메시지를 인쇄하는 것입니다.

`try`/`catch` 메커니즘은 복구할 수 있는 오류를 처리하는 데만 적합하다는 점에 유의하는 것이 중요합니다. 예를 들어 데이터베이스가 다운되면 오류를 복구하기 위해 아무것도 할 수 없으므로 `try`/`catch`는 아무 소용이 없습니다.

## 결론

이 기사에서는 Kotlin에서 MySQL 데이터베이스에 연결하는 방법을 살펴보았습니다. 데이터베이스를 구성하는 방법, 다양한 작업을 수행하는 코드를 작성하는 방법, 오류를 처리하는 방법을 살펴보았습니다.