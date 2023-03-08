---
title: 098: Acceso a la base de datos en Kotlin: conexión y consulta de bases de datos con Kotlin
description: 
published: true
date: 2023-02-09T06:17:13.867Z
tags: 
editor: markdown
dateCreated: 2023-02-09T06:17:12.239Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [098: Database Access in Kotlin: Connecting to and Querying Databases with Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/Learning/098-database-access-in-kotlin-connecting-to-and-querying-databases-with-kotlin)
{.links-list}


# Acceso a la base de datos en Kotlin: conexión y consulta de bases de datos con Kotlin

En esta publicación, veremos cómo conectarse y consultar bases de datos usando Kotlin. Cubriremos los siguientes temas:

- Conexión a una base de datos
- Creación y ejecución de sentencias SQL
- Recuperación de resultados de una base de datos.

## Conexión a una base de datos

Para conectarnos a una base de datos, necesitamos usar un controlador JDBC. Kotlin viene con un controlador JDBC incorporado, que podemos usar para conectarnos a bases de datos.

Para conectarnos a una base de datos, primero debemos crear una conexión JDBC. Podemos hacer esto usando la clase JDBC DriverManager. La clase DriverManager proporciona métodos estáticos para obtener una conexión JDBC.

Una vez que tengamos una conexión JDBC, podemos usarla para crear un objeto de declaración. Un objeto Statement se utiliza para ejecutar sentencias SQL.

## Creando y Ejecutando Sentencias SQL

Una vez que tenemos un objeto Statement, podemos usarlo para ejecutar sentencias SQL. Hay dos métodos que podemos usar para ejecutar sentencias SQL:

- ejecutar (): este método ejecuta una declaración SQL y devuelve un valor booleano que indica si la declaración es una consulta o no.
- executeQuery(): este método ejecuta una consulta SQL y devuelve un objeto ResultSet que contiene los resultados de la consulta.

## Recuperando resultados de una base de datos

Si usamos el método executeQuery() para ejecutar una consulta SQL, obtendremos un objeto ResultSet que contiene los resultados de la consulta.

Un objeto ResultSet contiene una lista de registros. Cada registro contiene los valores de las columnas de la consulta.

Podemos usar el objeto ResultSet para recuperar los registros de la base de datos. Podemos usar el método next() para pasar al siguiente registro en el ResultSet. Podemos usar el método getString() para recuperar el valor de una columna del registro actual.

Una vez que hemos recuperado los registros de la base de datos, podemos cerrar los objetos ResultSet y Statement. Finalmente, podemos cerrar la conexión JDBC.