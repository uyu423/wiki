---
title: Los principios SOLID en el desarrollo de Spring Boot
description: 
published: true
date: 2023-02-08T08:32:44.347Z
tags: 
editor: markdown
dateCreated: 2023-02-08T08:32:38.404Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [The SOLID Principles in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-solid-principles-in-spring-boot-development)
{.links-list}


# Los principios SOLID en el desarrollo de Spring Boot

Los desarrolladores siempre están buscando formas de escribir mejor código. Una forma de lograr esto es siguiendo los principios SOLID.

SOLID es un acrónimo de los cinco principios de diseño orientado a objetos desarrollados por Robert C. Martin:

- Principio de responsabilidad única
- Principio abierto-cerrado
- Principio de sustitución de Liskov
- Principio de segregación de interfaz
- Principio de inversión de dependencia

En este artículo, veremos cómo se pueden aplicar estos principios en el desarrollo de Spring Boot.

## Principio de responsabilidad única

El principio de responsabilidad única establece que una clase debe tener una sola razón para cambiar. En otras palabras, una clase solo debe tener una responsabilidad.

Por ejemplo, supongamos que tenemos una clase que maneja tanto el acceso a la base de datos como la lógica empresarial. Si necesitamos cambiar el código de acceso a la base de datos, también necesitaremos cambiar el código de lógica de negocios, aunque no queramos. Esto viola el principio de responsabilidad única.

Una mejor manera de diseñar esto sería crear dos clases separadas, una para el acceso a la base de datos y otra para la lógica empresarial. De esta manera, podemos cambiar el código de acceso a la base de datos sin tener que tocar el código de lógica de negocios.

## Principio abierto-cerrado

El principio abierto-cerrado establece que una clase debe estar abierta a la extensión pero cerrada a la modificación. En otras palabras, deberíamos poder extender una clase sin tener que modificar el código de la clase.

Por ejemplo, digamos que tenemos una clase que maneja pedidos de clientes. Es posible que deseemos agregar una nueva función que permita a los clientes cancelar sus pedidos. Si la clase no está diseñada de manera que nos permita agregar esta función sin modificar el código existente, violamos el principio abierto-cerrado.

Una mejor manera de diseñar esto sería crear una clase Orden abstracta con un método cancel() abstracto. Entonces podemos crear una clase CustomerOrder concreta que amplíe Order y proporcione una implementación concreta del método cancel(). De esta manera, podemos agregar la función de cancelar sin tener que modificar el código existente.

## Principio de sustitución de Liskov

El principio de sustitución de Liskov establece que un subtipo debe ser sustituible por su supertipo. En otras palabras, deberíamos poder usar un subtipo en lugar de su supertipo sin romper el código.

Por ejemplo, digamos que tenemos una clase que representa un rectángulo. Es posible que queramos crear una subclase que represente un cuadrado. Sin embargo, si la clase cuadrada no está diseñada de manera que pueda usarse en lugar de la clase rectangular, violamos el principio de sustitución de Liskov.

Una mejor manera de diseñar esto sería hacer que el ancho y el alto de la clase de rectángulo sean invariantes. Es decir, no podemos cambiar el ancho sin cambiar también la altura, y viceversa. De esta forma, la clase cuadrada se puede usar en lugar de la clase rectangular sin romper el código.

## Principio de segregación de interfaz

El principio de segregación de interfaces establece que no se debe obligar a un cliente a implementar una interfaz que no utiliza. En otras palabras, no debemos crear interfaces con demasiados métodos.

Por ejemplo, supongamos que tenemos una interfaz que define métodos para procesar pedidos. Es posible que deseemos crear una subclase que solo maneje pedidos de clientes. Sin embargo, si la interfaz define métodos para procesar pedidos de clientes y proveedores, la subclase se verá obligada a implementar métodos que no utiliza. Esto viola el principio de segregación de interfaces.

Una mejor manera de diseñar esto sería crear dos interfaces separadas, una para procesar pedidos de clientes y otra para procesar pedidos de proveedores. De esta forma, la subclase puede implementar la interfaz que necesita sin verse obligada a implementar la otra interfaz.

## Principio de inversión de dependencia

El principio de inversión de dependencia establece que una clase no debe depender de clases concretas, sino de abstracciones. En otras palabras, no debemos crear dependencias sobre clases específicas, sino sobre interfaces o clases abstractas.

Por ejemplo, digamos que tenemos una clase que depende de una clase de base de datos concreta. Si necesitamos cambiar la base de datos, también necesitaremos cambiar el código de la clase. Esto viola el principio de inversión de dependencia.

Una mejor manera de diseñar esto sería crear una dependencia en una clase de base de datos abstracta. Entonces podemos crear una clase MysqlDatabase concreta que amplíe la base de datos. De esta forma, podemos cambiar la base de datos sin tener que cambiar el código de la clase.

## Conclusión

En este artículo, analizamos cómo se pueden aplicar los principios SOLID en el desarrollo de Spring Boot. Estos principios pueden ayudarnos a escribir mejor código al hacer que nuestro código sea más mantenible y extensible.