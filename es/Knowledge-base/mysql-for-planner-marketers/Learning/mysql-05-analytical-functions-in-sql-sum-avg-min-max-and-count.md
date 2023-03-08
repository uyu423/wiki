---
title: MySQL 05: Funciones analíticas en SQL: SUM, AVG, MIN, MAX y COUNT
description: 
published: true
date: 2023-02-06T11:32:24.845Z
tags: 
editor: markdown
dateCreated: 2023-02-06T11:32:23.304Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [MySQL 05: Analytical functions in SQL: SUM, AVG, MIN, MAX, and COUNT***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-05-analytical-functions-in-sql-sum-avg-min-max-and-count)
{.links-list}


# MySQL 05: Funciones analíticas en SQL: SUM, AVG, MIN, MAX y COUNT

Las funciones analíticas son una poderosa herramienta en SQL para trabajar con datos. En esta publicación, veremos cómo usar las funciones SUM, AVG, MIN, MAX y COUNT para trabajar con datos en MySQL.

## SUMA

La función SUMA se utiliza para devolver la suma de una columna de datos. Por ejemplo, si tenemos una tabla de datos con una columna para números, podemos usar la función SUMA para obtener la suma de todos los números en esa columna:

```mysql
SELECT SUM(number_column)
FROM table_name;
```

## PROMEDIO

La función AVG se utiliza para devolver el promedio de una columna de datos. Por ejemplo, si tenemos una tabla de datos con una columna para números, podemos usar la función AVG para obtener el promedio de todos los números en esa columna:

```mysql
SELECT AVG(number_column)
FROM table_name;
```

## MÍN.

La función MIN se utiliza para devolver el valor mínimo de una columna de datos. Por ejemplo, si tenemos una tabla de datos con una columna para números, podemos usar la función MIN para obtener el número mínimo en esa columna:

```mysql
SELECT MIN(number_column)
FROM table_name;
```

## MÁX.

La función MAX se utiliza para devolver el valor máximo de una columna de datos. Por ejemplo, si tenemos una tabla de datos con una columna para números, podemos usar la función MAX para obtener el número máximo en esa columna:

```mysql
SELECT MAX(number_column)
FROM table_name;
```

## CONTAR

La función COUNT se usa para devolver el número de filas en una tabla. Por ejemplo, si tenemos una tabla de datos, podemos usar la función CONTAR para obtener el número de filas en esa tabla:

```mysql
SELECT COUNT(*)
FROM table_name;
```

Estas son solo algunas de las formas en que puede usar funciones analíticas en SQL para trabajar con datos. Para obtener más información, consulte los recursos a continuación.

## Recursos

- [Documentación MySQL: Funciones Analíticas](https://dev.mysql.com/doc/refman/8.0/en/group-by-functions.html)
- [Desbordamiento de pila: ¿Cuál es la diferencia entre contar (*), contar (1) y contar (nombre de columna)] (https://stackoverflow.com/questions/3696867/cuál-es-la-diferencia-entre-cuenta- 1-y-cuenta-nombre-de-columna)
- [W3Schools: CUENTA SQL](https://www.w3schools.com/sql/sql_count.asp)