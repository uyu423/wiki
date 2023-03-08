---
title: MySQL 03: sintaxis y operaciones básicas de SQL: SELECT, FROM, WHERE, GROUP BY y HAVING
description: 
published: true
date: 2023-02-06T09:32:26.350Z
tags: 
editor: markdown
dateCreated: 2023-02-06T09:32:20.860Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [MySQL 03: Basic SQL syntax and operations: SELECT, FROM, WHERE, GROUP BY, and HAVING***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-03-basic-sql-syntax-and-operations-select-from-where-group-by-and-having)
{.links-list}


# MySQL 03: Sintaxis y operaciones básicas de SQL: SELECT, FROM, WHERE, GROUP BY y HAVING

## Introducción

En esta publicación, cubriremos la sintaxis y las operaciones básicas de SQL para trabajar con datos en MySQL. Aprenderemos a usar las cláusulas `SELECT`, `FROM`, `WHERE`, `GROUP BY` y `HAVING` para consultar datos de una base de datos MySQL.

## SELECCIONAR

La cláusula `SELECT` se utiliza para especificar las columnas que desea recuperar de una tabla de base de datos. Por ejemplo, la siguiente instrucción `SELECT` recupera las columnas `first_name` y `last_name` de la tabla `employees`:

```sql
SELECT first_name, last_name
FROM employees
```

Si desea recuperar todas las columnas de una tabla, puede usar el carácter `*` en lugar de la lista de columnas:

```sql
SELECT *
FROM employees
```

## DE

La cláusula `FROM` se utiliza para especificar la tabla o tablas de las que desea recuperar datos. Por ejemplo, la siguiente sentencia `SELECT` recupera datos de la tabla `empleados`:

```sql
SELECT first_name, last_name
FROM employees
```

Puede especificar varias tablas en la cláusula `FROM` separándolas con una coma:

```sql
SELECT first_name, last_name
FROM employees, departments
```

## DÓNDE

La cláusula `WHERE` se usa para especificar condiciones para recuperar datos de una tabla de base de datos. Por ejemplo, la siguiente declaración `SELECT` recupera datos de la tabla `employees` donde `employee_id` es `1`:

```sql
SELECT first_name, last_name
FROM employees
WHERE employee_id = 1
```

Puede utilizar los operadores `AND` y `OR` para especificar varias condiciones en la cláusula `WHERE`:

```sql
SELECT first_name, last_name
FROM employees
WHERE employee_id = 1 OR employee_id = 2
```

## AGRUPAR POR

La cláusula `GROUP BY` se utiliza para agrupar datos de una tabla de base de datos. Por ejemplo, la siguiente instrucción `SELECT` recupera datos de la tabla `employees` y los agrupa por `department_id`:

```sql
SELECT department_id, count(*)
FROM employees
GROUP BY department_id
```

## TENER

La cláusula `HAVING` se usa para especificar condiciones para recuperar datos de una tabla de base de datos. Por ejemplo, la siguiente sentencia `SELECT` recupera datos de la tabla `empleados` donde `department_id` es `1`:

```sql
SELECT department_id, count(*)
FROM employees
GROUP BY department_id
HAVING department_id = 1
```

## Conclusión

En esta publicación, hemos cubierto la sintaxis y las operaciones básicas de SQL para trabajar con datos en MySQL. Hemos aprendido a usar las cláusulas `SELECT`, `FROM`, `WHERE`, `GROUP BY` y `HAVING` para consultar datos de una base de datos MySQL.