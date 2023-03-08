---
title: 061: Integración de Spring Boot con bases de datos NoSQL
description: 
published: true
date: 2023-02-05T00:32:21.220Z
tags: 
editor: markdown
dateCreated: 2023-02-05T00:32:19.645Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [061: Integrating Spring Boot with NoSQL Databases***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/061-integrating-spring-boot-with-nosql-databases)
{.links-list}


# 061: Integrando Spring Boot con Bases de Datos NoSQL

En esta publicación, aprenderemos cómo integrar una aplicación Spring Boot con una base de datos NoSQL.

## ¿Qué es NoSQL?

NoSQL es un término utilizado para describir una base de datos no relacional. Una base de datos NoSQL es aquella que no utiliza el modelo relacional tradicional basado en tablas que utilizan la mayoría de las bases de datos relacionales.

Las bases de datos NoSQL suelen ser más escalables y fáciles de usar que las bases de datos relacionales. También son adecuados para almacenar grandes cantidades de datos que no se estructuran fácilmente en un esquema tradicional basado en tablas.

## ¿Por qué usar NoSQL con Spring Boot?

Las bases de datos NoSQL son una buena opción para muchas aplicaciones Spring Boot. Suelen ser más escalables y fáciles de usar que las bases de datos relacionales. Spring Boot brinda un buen soporte para las bases de datos NoSQL, lo que facilita el trabajo con ellas en su aplicación.

## Cómo integrar NoSQL con Spring Boot

 Spring Boot proporciona un buen soporte para bases de datos NoSQL. Puede usar cualquiera de las bases de datos NoSQL populares con Spring Boot. En esta publicación, usaremos MongoDB como nuestra base de datos NoSQL.

MongoDB es una base de datos NoSQL popular que es fácil de usar con Spring Boot. Spring Boot proporciona un módulo de inicio para MongoDB que facilita el trabajo con MongoDB en su aplicación.

Para usar MongoDB con Spring Boot, deberá agregar el módulo de inicio spring-boot-starter-data-mongodb a su proyecto. Puede agregar este módulo a su proyecto utilizando la siguiente dependencia de Maven:

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

También deberá configurar MongoDB con su aplicación. Puede hacerlo agregando un archivo de configuración de MongoDB a su aplicación. El siguiente es un archivo de configuración básico de MongoDB:

```properties
spring.data.mongodb.uri=mongodb://localhost/test
```

Este archivo de configuración le dice a Spring Boot que se conecte a una base de datos MongoDB en localhost en el puerto predeterminado (27017). El nombre de la base de datos es prueba.

## Resumen

En esta publicación, aprendimos cómo integrar una aplicación Spring Boot con una base de datos NoSQL. También aprendimos por qué es posible que desee utilizar una base de datos NoSQL con Spring Boot y cómo configurar MongoDB con Spring Boot.