---
title: Kotlin con Spring Boot: configuración automática y actuador
description: 
published: true
date: 2023-02-02T18:23:16.632Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:23:15.020Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin with Spring Boot: Auto-configuration and Actuator***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-with-spring-boot-auto-configuration-and-actuator)
{.links-list}


# Kotlin con Spring Boot: Autoconfiguración y Actuador

Kotlin es un lenguaje de programación de tipo estático que se ejecuta en JVM y se puede usar para desarrollar aplicaciones de Android. Spring Boot es un marco que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción que puede "simplemente ejecutar".

El proyecto Kotlin con Spring Boot proporciona configuración automática y compatibilidad con Actuator para las aplicaciones Kotlin y Spring Boot.

## Configuración automática

La configuración automática es una característica de Spring Boot que configura automáticamente su aplicación Spring en función de las dependencias que tiene en el classpath. Por ejemplo, si incluye la dependencia spring-boot-starter-data-jpa en el classpath, Spring Boot configurará automáticamente un DataSource y JPA EntityManagerFactory para usted.

El proyecto Kotlin con Spring Boot proporciona configuración automática para las aplicaciones Kotlin y Spring Boot. Esto significa que, por ejemplo, si incluye la dependencia spring-boot-starter-data-jpa en el classpath, Kotlin con Spring Boot configurará automáticamente un DataSource y JPA EntityManagerFactory para usted.

Para usar la configuración automática de Kotlin con Spring Boot, debe agregar el módulo kotlin-spring-boot-autoconfigure a su classpath.

## Actuador

Actuator es una característica de Spring Boot que le permite monitorear y administrar su aplicación. Por ejemplo, Actuator proporciona un punto final HTTP que puede usar para monitorear el estado de su aplicación.

El proyecto Kotlin con Spring Boot brinda compatibilidad con Actuator para las aplicaciones Kotlin y Spring Boot. Esto significa que, por ejemplo, puede usar Actuator para monitorear el estado de su aplicación Kotlin y Spring Boot.

Para usar Kotlin con Spring Boot Actuator, debe agregar el módulo kotlin-spring-boot-actuator a su classpath.

## Empezando

Para comenzar con Kotlin y Spring Boot, puede usar Spring Initializr para generar un proyecto con las dependencias que necesita. Por ejemplo, para generar un proyecto con las dependencias kotlin-spring-boot-autoconfigure y kotlin-spring-boot-actuator, haría lo siguiente:

1. Vaya a https://start.spring.io/.
2. Seleccione Kotlin en el menú desplegable Idioma.
3. Seleccione Spring Boot 2.0.0 en el menú desplegable Versión de arranque.
4. Ingrese kotlin-spring-boot-example en el campo Artefacto.
5. Seleccione las dependencias kotlin-spring-boot-autoconfigure y kotlin-spring-boot-actuator.
6. Haga clic en Generar proyecto.

¡Luego puede importar el proyecto generado a su IDE favorito y comenzar a codificar!

## Conclusión

En este artículo, analizamos el proyecto Kotlin con Spring Boot, que proporciona configuración automática y compatibilidad con Actuator para las aplicaciones Kotlin y Spring Boot. También hemos visto cómo comenzar con Kotlin y Spring Boot, utilizando Spring Initializr para generar un proyecto con las dependencias necesarias.