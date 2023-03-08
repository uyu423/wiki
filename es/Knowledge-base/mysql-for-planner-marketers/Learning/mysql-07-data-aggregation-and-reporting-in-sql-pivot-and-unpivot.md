---
title: MySQL 07: Agregación de datos y generación de informes en SQL: PIVOT y UNPIVOT
description: 
published: true
date: 2023-02-06T13:32:37.509Z
tags: 
editor: markdown
dateCreated: 2023-02-06T13:32:35.890Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [MySQL 07: Data aggregation and reporting in SQL: PIVOT and UNPIVOT***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-07-data-aggregation-and-reporting-in-sql-pivot-and-unpivot)
{.links-list}


MySQL 07: Agregación de datos y generación de informes en SQL: PIVOT y UNPIVOT

En los negocios, los datos a menudo se agregan y se informan para tomar decisiones. Por ejemplo, una empresa podría querer saber cuántos productos se vendieron en cada región para comprender mejor dónde asignar los recursos.

En esta publicación, aprenderemos cómo usar los operadores SQL PIVOT y UNPIVOT para agregar e informar datos en MySQL.

PIVOTE

El operador PIVOT se utiliza para convertir filas en columnas. Toma como entrada una tabla con datos en filas y genera una tabla con datos en columnas.

Para usar PIVOT, primero debemos especificar las columnas que queremos convertir en filas. Podemos hacer esto usando la cláusula FOR. Por ejemplo, la siguiente consulta convierte las columnas Región y Producto en filas:

```sql
SELECT *
FROM mytable
PIVOT (
  SUM(Sales)
  FOR Region IN ('East', 'West', 'North', 'South')
) AS pvt;
```

En la consulta anterior, usamos la función SUMA para agregar la columna Ventas. También estamos usando la cláusula IN para especificar los valores que queremos convertir en columnas.

El resultado de la consulta se verá así:

| | Este | Oeste | Norte | Sur |
| --- | --- | --- | --- | --- |
| Producto A | 10 | 20 | 30 | 40 |
| Producto B | 50 | 60 | 70 | 80 |

Si queremos, también podemos especificar el nombre de las columnas de salida usando la cláusula AS. En el ejemplo anterior, hemos usado el alias pvt para la tabla de salida.

UNPIVOT

El operador UNPIVOT se utiliza para convertir columnas en filas. Toma como entrada una tabla con datos en columnas y genera una tabla con datos en filas.

Para usar UNPIVOT, primero debemos especificar las columnas que queremos convertir en filas. Podemos hacer esto usando la cláusula FOR. Por ejemplo, la siguiente consulta convierte las columnas Este, Oeste, Norte y Sur en filas:

```sql
SELECT *
FROM mytable
UNPIVOT (
  Sales
  FOR Region IN ('East', 'West', 'North', 'South')
) AS upvt;
```

En la consulta anterior, usamos la columna Ventas como entrada para UNPIVOT. También estamos usando la cláusula IN para especificar los valores que queremos convertir en filas.

El resultado de la consulta se verá así:

| Región | Ventas |
| --- | --- |
| Este | 10 |
| Oeste | 20 |
| Norte | 30 |
| Sur | 40 |

Si queremos, también podemos especificar el nombre de las columnas de salida usando la cláusula AS. En el ejemplo anterior, hemos usado el alias upvt para la tabla de salida.

información adicional

Los operadores PIVOT y UNPIVOT son muy potentes y se pueden utilizar para realizar una variedad de tareas de agregación e informes.

Si está interesado en obtener más información sobre PIVOT y UNPIVOT, le recomiendo consultar los siguientes recursos:

- La documentación de MySQL sobre PIVOT y UNPIVOT
- Esta excelente publicación de blog sobre PIVOT y UNPIVOT
- Esta respuesta de desbordamiento de pila en PIVOT y UNPIVOT