---
title: MySQL 04: Técnicas avanzadas de SQL: JOIN, UNION y subconsultas
description: 
published: true
date: 2023-02-06T10:32:15.572Z
tags: 
editor: markdown
dateCreated: 2023-02-06T10:32:14.010Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [MySQL 04: Advanced SQL techniques: JOIN, UNION, and subqueries***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-04-advanced-sql-techniques-join-union-and-subqueries)
{.links-list}


MySQL es un poderoso sistema de administración de bases de datos utilizado por millones de sitios web y aplicaciones. Ofrece una amplia gama de características y opciones para que trabajar con datos sea fácil y eficiente.

En esta publicación, veremos algunas técnicas avanzadas de SQL que se pueden usar para trabajar con datos en MySQL. Cubriremos temas como uniones, uniones y subconsultas. Al final de esta publicación, debe tener una buena comprensión de cómo usar estas técnicas para trabajar con datos en MySQL.

## Uniones

Una combinación es una forma de combinar datos de dos o más tablas en un único conjunto de resultados. Las uniones se utilizan para recuperar datos de varias tablas.

Hay diferentes tipos de uniones, pero el tipo más común es la unión interna. Una unión interna devuelve todas las filas de ambas tablas que coinciden con la condición de unión.

Aquí hay un ejemplo de una unión interna:

```sql
SELECT *
FROM table1
INNER JOIN table2
ON table1.id = table2.id
```

En este ejemplo, estamos uniendo dos tablas, table1 y table2, en la columna id. El resultado de esta consulta serán todas las filas de ambas tablas que tengan la misma identificación.

## Sindicatos

Una unión es una forma de combinar datos de dos o más tablas en un único conjunto de resultados. A diferencia de una unión, una unión no requiere una condición de unión.

He aquí un ejemplo de una unión:

```sql
SELECT *
FROM table1
UNION
SELECT *
FROM table2
```

En este ejemplo, estamos uniendo dos tablas, table1 y table2. El resultado de esta consulta serán todas las filas de ambas tablas.

## Subconsultas

Una subconsulta es una consulta anidada dentro de otra consulta. Una subconsulta se usa para devolver datos que usa la consulta externa.

He aquí un ejemplo de una subconsulta:

```sql
SELECT *
FROM table1
WHERE id IN (SELECT id
            FROM table2)
```

En este ejemplo, usamos una subconsulta para devolver todas las filas de la tabla 1 que tienen una identificación que también está en la tabla 2.