---
title: MySQL 06: manipulación de datos en SQL: INSERTAR, ACTUALIZAR, ELIMINAR y ALTERAR
description: 
published: true
date: 2023-02-06T12:32:55.384Z
tags: 
editor: markdown
dateCreated: 2023-02-06T12:32:53.739Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [MySQL 06: Data manipulation in SQL: INSERT, UPDATE, DELETE, and ALTER***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-06-data-manipulation-in-sql-insert-update-delete-and-alter)
{.links-list}


MySQL 06: manipulación de datos en SQL: INSERTAR, ACTUALIZAR, ELIMINAR y ALTERAR
================================================== ==========

En esta publicación, cubriremos la manipulación de datos en SQL usando las declaraciones INSERT, UPDATE, DELETE y ALTER.

### INSERTAR

La declaración INSERT se utiliza para insertar datos en una tabla de base de datos. La sintaxis para INSERTAR es la siguiente:

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

Aquí, ```table_name``` es el nombre de la tabla en la que desea insertar datos, y ```(column1, column2, column3, ...)``` es una lista de las columnas en las que desea insertar datos. desea insertar datos. ```VALUES (valor1, valor2, valor3, ...)``` es una lista de los valores que desea insertar.

Tenga en cuenta que no tiene que especificar un valor para cada columna de la tabla. Si no especifica un valor para una columna, se utilizará el valor predeterminado para esa columna.

Aquí hay un ejemplo de cómo insertar datos en una tabla:

```sql
INSERT INTO products (name, price)
VALUES ('Widget', 9.99);
```

Esto insertará una fila en la tabla ```products``` con el nombre ```Widget``` y el precio ```9.99```.

También puede insertar varias filas en una tabla a la vez:

```sql
INSERT INTO products (name, price)
VALUES ('Widget', 9.99),
       ('Gadget', 19.99),
       ('Doohickey', 29.99);
```

Esto insertará tres filas en la tabla ```products```.

### ACTUALIZAR

La instrucción UPDATE se utiliza para actualizar datos en una tabla de base de datos. La sintaxis para ACTUALIZAR es la siguiente:

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, column3 = value3, ...
WHERE condition;
```

Aquí, ```table_name``` es el nombre de la tabla que desea actualizar, ```SET columna1 = valor1, columna2 = valor2, columna3 = valor3, ...``` es una lista de las columnas que desea para actualizar y los nuevos valores para esas columnas, y ```WHERE condition``` es una condición que especifica qué filas actualizar.

Por ejemplo, la siguiente declaración actualizará la columna ```price``` para todas las filas en la tabla ```products``` donde ```name``` es ```Widget```:

```sql
UPDATE products
SET price = 11.99
WHERE name = 'Widget';
```

También puede actualizar varias columnas a la vez:

```sql
UPDATE products
SET price = 11.99,
    name = 'NewWidget'
WHERE name = 'Widget';
```

### BORRAR

La declaración DELETE se utiliza para eliminar datos de una tabla de base de datos. La sintaxis para DELETE es la siguiente:

```sql
DELETE FROM table_name
WHERE condition;
```

Aquí, ```table_name``` es el nombre de la tabla de la que desea eliminar datos, y ```WHERE condition``` es una condición que especifica qué filas eliminar.

Por ejemplo, la siguiente instrucción eliminará todas las filas de la tabla ```products``` donde ```name``` es ```Widget```:

```sql
DELETE FROM products
WHERE name = 'Widget';
```

### ALTERAR

La declaración ALTER se utiliza para modificar la estructura de una tabla de base de datos. La sintaxis para ALTER es la siguiente:

```sql
ALTER TABLE table_name
ADD column_name data_type;

ALTER TABLE table_name
MODIFY column_name data_type;

ALTER TABLE table_name
DROP column_name;
```

Aquí, ```table_name``` es el nombre de la tabla que desea modificar, ```ADD column_name data_type``` agrega una nueva columna a la tabla con el tipo de datos especificado, ```MODIFY column_name data_type`` ` cambia el tipo de datos de una columna existente, y ```DROP column_name``` elimina una columna de la tabla.

Por ejemplo, la siguiente instrucción agregará una nueva columna ```precio``` a la tabla ```productos```:

```sql
ALTER TABLE products
ADD price decimal(5,2);
```

Y la siguiente declaración cambiará el tipo de datos de la columna ```price``` a ```integer```:

```sql
ALTER TABLE products
MODIFY price integer;
```

información adicional
-------------------------------------

Aquí hay algunas cosas adicionales a tener en cuenta cuando se trabaja con la manipulación de datos en SQL:

* Si está insertando datos en una tabla que tiene una columna ```AUTO_INCREMENT```, puede especificar el valor ```NULL``` para esa columna y MySQL generará automáticamente un nuevo valor para ella.

* Si está actualizando o eliminando datos, la cláusula ```WHERE``` es opcional. Si omite la cláusula ```WHERE```, todas las filas de la tabla se actualizarán o eliminarán.

* Puede usar las cláusulas ```ORDER BY``` y ```LIMIT``` con las declaraciones ```UPDATE``` y ```DELETE``` para especificar qué filas actualizar o eliminar.

* La instrucción ```ALTER TABLE``` se puede usar para agregar, modificar o eliminar columnas en una tabla, así como para agregar o eliminar índices.

* Puede usar la sentencia ```ALTER TABLE``` para cambiar el nombre de una tabla.

Recursos externos
------------------

Aquí hay algunos recursos externos para leer más sobre la manipulación de datos en SQL:

* [Tutorial de MySQL](https://dev.mysql.com/doc/refman/5.7/en/sql-tutorial.html)
* [Instrucción SQL INSERT](https://www.w3schools.com/sql/sql_insert.asp)
* [Declaración de ACTUALIZACIÓN de SQL] (https://www.w3schools.com/sql/sql_update.asp)
* [Declaración SQL DELETE](https://www.w3schools.com/sql/sql_delete.asp)
* [Declaración SQL ALTER TABLE](https://www.w3schools.com/sql/sql_alter.asp)