---
title: MySQL 08: SQL para problemas empresariales del mundo real: segmentación de clientes y análisis de productos
description: 
published: true
date: 2023-02-06T14:32:48.807Z
tags: 
editor: markdown
dateCreated: 2023-02-06T14:32:47.103Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [MySQL 08: SQL for real-world business problems: Customer segmentation and product analysis***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-08-sql-for-real-world-business-problems-customer-segmentation-and-product-analysis)
{.links-list}


MySQL 08: SQL para problemas empresariales del mundo real: segmentación de clientes y análisis de productos

En esta publicación, aprenderemos cómo usar SQL para resolver problemas comerciales del mundo real. Cubriremos la segmentación de clientes y el análisis de productos, dos problemas comunes que enfrentan las empresas.

La segmentación de clientes es el proceso de dividir a los clientes en grupos en función de características compartidas. Esto es importante porque permite a las empresas adaptar sus esfuerzos de marketing y ventas a grupos específicos de clientes.

El análisis de productos es el proceso de comprender los datos de ventas de un producto. Esto es importante porque permite a las empresas tomar decisiones informadas sobre el desarrollo de productos, la fijación de precios y la gestión de inventario.

Usaremos la base de datos MySQL para esta publicación. MySQL es un sistema de gestión de bases de datos gratuito y de código abierto. Es una opción popular para aplicaciones web y es utilizada por algunos de los sitios web más grandes del mundo, incluidos Facebook, Twitter y YouTube.

Para comenzar, necesitaremos crear una base de datos. Podemos hacer esto usando la consola MySQL o una herramienta GUI como phpMyAdmin. Llamaremos a nuestra base de datos "negocio".

A continuación, necesitaremos crear dos tablas: "clientes" y "productos".

La tabla "clientes" almacenará información sobre nuestros clientes. Tendremos que incluir las siguientes columnas:

* customer_id: la identificación única del cliente.
* nombre: El nombre del cliente.
* email: la dirección de correo electrónico del cliente.
* date_of_birth: La fecha de nacimiento del cliente.
*sexo: El sexo del cliente.

La tabla de "productos" almacenará información sobre nuestros productos. Tendremos que incluir las siguientes columnas:

* product_id: la identificación única del producto.
* nombre: El nombre del producto.
* precio: El precio del producto.
*categoría: La categoría del producto.
* release_date: la fecha de lanzamiento del producto.

Ahora que tenemos nuestra base de datos y tablas configuradas, podemos comenzar a agregar datos.

Comenzaremos con la tabla "clientes". Añadiremos tres clientes a nuestra base de datos:

* id_cliente: 1
* nombre: Juan Smith
* correo electrónico: john@example.com
* fecha_de_nacimiento: 01/01/2000
* género masculino

* id_cliente: 2
* nombre: Jane Doe
* correo electrónico: jane@example.com
* fecha_de_nacimiento: 02/02/2001
* género femenino

* id_cliente: 3
* nombre: John Doe
* correo electrónico: john@example.com
* fecha_de_nacimiento: 01/01/2000
* género masculino

A continuación, agregaremos datos a la tabla "productos". Agregaremos tres productos a nuestra base de datos:

* id_producto: 1
* nombre: producto 1
* precio: 10
* categoría: categoría 1
* fecha_de_lanzamiento: 01/01/2020

* id_producto: 2
* nombre: producto 2
* precio: 20
* categoría: categoría 2
* fecha_de_lanzamiento: 02/02/2021

* id_producto: 3
* nombre: producto 3
* precio: 30
* categoría: categoría 3
* fecha_de_lanzamiento: 03/03/2022

Ahora que tenemos nuestros datos, podemos comenzar a consultarlos.

Comenzaremos con una consulta simple para obtener todos los datos de la tabla "clientes":

```mysql
SELECT * FROM customers;
```

Esta consulta devolverá todas las columnas y filas de la tabla "clientes".

A continuación, escribiremos una consulta para obtener datos específicos de la tabla "clientes". Por ejemplo, podríamos querer obtener todos los clientes que son mujeres:

```mysql
SELECT * FROM customers
WHERE gender = "Female";
```

Esta consulta devolverá todas las columnas y filas de la tabla "clientes" donde el género es igual a "Mujer".

También podemos usar la cláusula GROUP BY de MySQL para agrupar nuestros datos. Por ejemplo, podríamos querer agrupar a nuestros clientes por género:

```mysql
SELECT gender, COUNT(*) FROM customers
GROUP BY gender;
```

Esta consulta devolverá el número de clientes para cada género.

También podemos usar la cláusula ORDER BY de MySQL para ordenar nuestros datos. Por ejemplo, podríamos querer ordenar a nuestros clientes por nombre:

```mysql
SELECT * FROM customers
ORDER BY name;
```

Esta consulta devolverá todas las columnas y filas de la tabla "clientes", ordenadas por nombre.

Ahora que hemos aprendido a consultar la tabla "clientes", pasemos a la tabla "productos".

Comenzaremos con una consulta simple para obtener todos los datos de la tabla "productos":

```mysql
SELECT * FROM products;
```

Esta consulta devolverá todas las columnas y filas de la tabla "productos".

A continuación, escribiremos una consulta para obtener datos específicos de la tabla "productos". Por ejemplo, podríamos querer obtener todos los productos en la categoría "categoría 1":

```mysql
SELECT * FROM products
WHERE category = "category 1";
```

Esta consulta devolverá todas las columnas y filas de la tabla "productos" donde la categoría es igual a "categoría 1".

También podemos usar la cláusula GROUP BY de MySQL para agrupar nuestros datos. Por ejemplo, podríamos querer agrupar nuestros productos por categoría:

```mysql
SELECT category, COUNT(*) FROM products
GROUP BY category;
```

Esta consulta devolverá el número de productos en cada categoría.

También podemos usar la cláusula ORDER BY de MySQL para ordenar nuestros datos. Por ejemplo, podríamos querer ordenar nuestros productos por precio:

```mysql
SELECT * FROM products
ORDER BY price;
```

Esta consulta devolverá todas las columnas y filas de la tabla "productos", ordenadas por precio.

Finalmente, escribiremos una consulta para obtener el precio promedio de los productos en cada categoría:

```mysql
SELECT category, AVG(price) FROM products
GROUP BY category;
```

Esta consulta devolverá el precio promedio de los productos en cada categoría.

¡Eso es todo! Ahora hemos aprendido a usar SQL para resolver problemas comerciales del mundo real.