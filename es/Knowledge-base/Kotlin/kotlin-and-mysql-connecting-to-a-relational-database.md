---
title: Kotlin y MySQL: conexión a una base de datos relacional
description: 
published: true
date: 2023-02-17T03:17:43.997Z
tags: 
editor: markdown
dateCreated: 2023-02-17T03:17:42.074Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin and MySQL: Connecting to a Relational Database***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-mysql-connecting-to-a-relational-database)
{.links-list}


# Kotlin y MySQL: conexión a una base de datos relacional

En este artículo, exploraremos cómo conectarse a una base de datos MySQL desde Kotlin. Veremos cómo configurar la base de datos, escribir código para realizar varias operaciones y manejar errores.

## Configuración de MySQL

Antes de que podamos comenzar a escribir código, necesitamos configurar nuestra base de datos. Asumiremos que tiene MySQL instalado y ejecutándose en su máquina local. Si no, puede descargarlo [aquí] (https://dev.mysql.com/doc/refman/8.0/en/installing.html).

Una vez que MySQL esté funcionando, necesitamos crear una base de datos y un usuario que nuestro código Kotlin pueda usar. Podemos hacer esto iniciando sesión en la consola de MySQL:

```mysql
mysql> CREATE DATABASE kotlindb;
Query OK, 1 row affected (0.01 sec)

mysql> CREATE USER 'kotlinuser'@'localhost' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON kotlindb.* TO 'kotlinuser'@'localhost';
Query OK, 0 rows affected (0.00 sec)
```

## Conexión a la base de datos

Ahora que nuestra base de datos está configurada, podemos escribir algo de código Kotlin para conectarnos a ella. Usaremos el [controlador JDBC](https://dev.mysql.com/doc/connector-j/8.0/en/) para MySQL, que puede agregar a su proyecto al incluir la siguiente dependencia en su compilación Archivo .gradle`:

```groovy
dependencies {
    implementation 'mysql:mysql-connector-java:8.0.21'
}
```

Con el controlador JDBC en su lugar, podemos escribir una función de Kotlin para conectarnos a la base de datos:

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

Esta función intenta conectarse a la base de datos utilizando la `url`, el `usuario` y la `contraseña` que configuramos anteriormente. Si la conexión es exitosa, devuelve el objeto `Conexión`. Si la conexión falla, devuelve `null`.

## Realización de operaciones de base de datos

Ahora que tenemos una forma de conectarnos a la base de datos, podemos comenzar a escribir código para realizar varias operaciones. Comenzaremos con un ejemplo simple: consultar la base de datos para obtener una lista de todos los usuarios.

Primero, necesitaremos escribir una consulta SQL:

```sql
SELECT * FROM users
```

A continuación, escribiremos una función de Kotlin para ejecutar esta consulta:

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

Esta función toma un objeto `Conexión` como parámetro. Luego crea un objeto `Declaración` y lo usa para ejecutar la consulta SQL. El método `executeQuery` devuelve un objeto `ResultSet`, que contiene los resultados de la consulta.

Podemos usar el método `siguiente` del objeto `ResultSet` para recorrer los resultados. Para cada resultado, creamos un objeto 'Usuario' y lo agregamos a la lista de 'usuarios'. Finalmente, devolvemos la lista de `usuarios`.

## Manejo de errores

Hasta ahora hemos visto cómo conectarse a la base de datos y realizar varias operaciones. Pero, ¿qué pasa si algo sale mal? Por ejemplo, ¿qué sucede si la base de datos está inactiva o la consulta SQL no es válida?

En Kotlin, podemos usar el mecanismo `try`/`catch` para manejar los errores. Modifiquemos nuestra función `getAllUsers` para usar `try`/`catch`:

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

En esta versión de la función `getAllUsers`, hemos envuelto el código en un bloque `try`. Si se lanza una `SQLException`, se ejecutará el código en el bloque `catch`. En este caso, simplemente estamos imprimiendo un mensaje de error.

Es importante tener en cuenta que el mecanismo `try`/`catch` solo es adecuado para manejar errores de los que se puede recuperar. Por ejemplo, si la base de datos no funciona, no podemos hacer nada para recuperarnos del error, por lo que `try`/`catch` no será de ninguna utilidad.

## Conclusión

En este artículo hemos visto cómo conectarse a una base de datos MySQL desde Kotlin. Hemos visto cómo configurar la base de datos, escribir código para realizar varias operaciones y manejar errores.