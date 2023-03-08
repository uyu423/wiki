---
title: Transacciones Spring Boot e Hibernate
description: 
published: true
date: 2023-02-07T23:32:35.330Z
tags: 
editor: markdown
dateCreated: 2023-02-07T23:32:29.485Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot and Hibernate Transactions***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-hibernate-transactions)
{.links-list}


# Transacciones Spring Boot e Hibernate

Las transacciones son una parte fundamental de cualquier aplicación respaldada por una base de datos. En pocas palabras, una transacción es una forma de agrupar una o más operaciones de base de datos en una unidad atómica. O todas las operaciones tienen éxito, o ninguna.

Hay muchos beneficios al usar transacciones, incluyendo:

- Garantizar la consistencia de los datos: si alguna de las operaciones de una transacción falla, se revierte toda la transacción y la base de datos permanece en su estado original.
- Permitir un mejor rendimiento: las operaciones de la base de datos dentro de una transacción se pueden agrupar en lotes, lo que reduce la cantidad de viajes de ida y vuelta a la base de datos y puede mejorar el rendimiento.
- Mejora de la concurrencia: al aislar las transacciones entre sí, es posible evitar que una transacción interfiera con otra.

En este artículo, veremos cómo usar transacciones con Spring Boot e Hibernate. Comenzaremos con una descripción general rápida de los diferentes tipos de transacciones y luego nos sumergiremos en algunos ejemplos de código.

## Tipos de Transacciones

Hay dos tipos principales de transacciones: locales y globales.

Una transacción local es aquella que es administrada por un solo recurso, como una base de datos. En una transacción local, todas las operaciones deben realizarse en la misma base de datos. Si alguna de las operaciones falla, se revierte toda la transacción y la base de datos se deja en su estado original.

Una transacción global es aquella que es administrada por múltiples recursos, como una base de datos y una cola de mensajes. Las transacciones globales son más complejas que las transacciones locales, pero ofrecen la ventaja de poder revertir toda la transacción incluso si falla uno de los recursos.

## Uso de transacciones con Spring Boot

Spring Boot proporciona soporte de primera clase para transacciones. De hecho, las transacciones son tan importantes que la aplicación Spring Boot no se iniciará si detecta que la base de datos no está configurada para transacciones.

Al configurar transacciones en Spring Boot, hay tres cosas a tener en cuenta:

- La anotación @Transactional: esta anotación se utiliza para marcar métodos que deben ejecutarse en una transacción.
- El PlatformTransactionManager: este es el componente que realmente gestiona la transacción. Spring Boot configurará automáticamente un bean PlatformTransactionManager si detecta que está utilizando una base de datos.
- El nivel de aislamiento de la transacción: este es el nivel de aislamiento que desea para sus transacciones. Los diferentes niveles de aislamiento ofrecen diferentes garantías sobre la consistencia de sus datos.

La forma más común de configurar transacciones en Spring Boot es usar la anotación @Transactional. Esta anotación se puede agregar a una clase o un método. Cuando se agrega a una clase, se aplica a todos los métodos de la clase. Cuando se agrega a un método, solo se aplica a ese método.

La anotación @Transactional tiene algunos parámetros opcionales que se pueden usar para personalizar su comportamiento. El más importante de ellos es el nivel de aislamiento. El nivel de aislamiento se usa para controlar cuán estrictamente la base de datos aplica las propiedades ACID.

Hay cuatro niveles de aislamiento que se utilizan comúnmente:

- LEER SIN COMPROMISO: Este es el nivel de aislamiento menos estricto. Permite que las transacciones concurrentes lean datos que no han sido confirmados por otras transacciones. Esto puede generar inconsistencias en los datos, pero ofrece el mejor rendimiento.
- LECTURA COMPROMETIDA: Este nivel de aislamiento es más estricto que LECTURA NO COMPROMETIDA. Solo permite transacciones concurrentes para leer datos que han sido confirmados por otras transacciones. Esto evita la incoherencia de los datos, pero puede provocar problemas de rendimiento.
- LECTURA REPETIBLE: Este nivel de aislamiento es aún más estricto que la LECTURA COMPROMETIDA. Solo permite que las transacciones concurrentes lean datos que hayan sido comprometidos por otras transacciones, y también evita que lean datos que hayan sido modificados por otras transacciones. Esto ofrece la mejor coherencia de datos, pero puede provocar problemas de rendimiento.
- SERIALIZABLE: Es el nivel de aislamiento más estricto. Evita que las transacciones concurrentes lean o escriban datos que hayan sido modificados por otras transacciones. Esto ofrece la mejor coherencia de datos, pero puede provocar problemas de rendimiento.

Es importante elegir el nivel de aislamiento adecuado para su aplicación. Si elige un nivel de aislamiento demasiado estricto, es posible que experimente problemas de rendimiento. Si elige un nivel de aislamiento demasiado laxo, es posible que observe incoherencias en los datos.

## Uso de transacciones con Hibernate

Hibernate es una herramienta ORM popular que a menudo se usa junto con Spring. Hibernate también admite transacciones y ofrece algunas formas diferentes de configurarlas.

La forma más común de configurar transacciones en Hibernate es usar la anotación @Transactional. Esta anotación se puede agregar a una clase o un método. Cuando se agrega a una clase, se aplica a todos los métodos de la clase. Cuando se agrega a un método, solo se aplica a ese método.

La anotación @Transactional tiene algunos parámetros opcionales que se pueden usar para personalizar su comportamiento. El más importante de ellos es el nivel de aislamiento. El nivel de aislamiento se usa para controlar cuán estrictamente la base de datos aplica las propiedades ACID.

Hibernate también admite transacciones programáticas. Esto significa que puede configurar la transacción en código, en lugar de usar una anotación. Por lo general, esto no se recomienda, ya que hace que el código sea más difícil de entender y mantener.

## Conclusión

En este artículo, hemos visto cómo usar transacciones con Spring Boot e Hibernate. Hemos visto cómo configurar transacciones usando la anotación @Transactional, y también hemos visto cómo elegir el nivel de aislamiento adecuado para nuestras necesidades.