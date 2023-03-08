---
title: Puntos finales del actuador Spring Boot
description: 
published: true
date: 2023-02-07T06:32:15.526Z
tags: 
editor: markdown
dateCreated: 2023-02-07T06:32:13.920Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Actuator Endpoints***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-actuator-endpoints)
{.links-list}


# Puntos finales del actuador Spring Boot

Spring Boot Actuator Endpoints nos permite monitorear y administrar nuestra aplicación Spring Boot. En este artículo, veremos qué son estos puntos finales y cómo podemos usarlos.

## ¿Qué es un punto final de actuador?

Un Actuator Endpoint es una URL expuesta por una aplicación Spring Boot que se puede usar para monitorear y administrar la aplicación. Estos puntos finales proporcionan información sobre la aplicación, como el estado de la aplicación, la versión de la aplicación, etc.

## Puntos finales

Hay varios Actuator Endpoints que están disponibles en Spring Boot. Algunos de estos puntos finales son:

### /información

Este punto final proporciona información sobre la aplicación. Esta información se configura en el archivo `application.properties`.

### /salud

Este extremo proporciona información sobre el estado de la aplicación. Esta información la recopilan los beans HealthIndicator que están registrados en la aplicación.

### /métricas

Este punto final proporciona información sobre las métricas de la aplicación. Esta información la recopilan los beans Metrics que están registrados en la aplicación.

### /rastro

Este punto final proporciona información sobre los rastros de la aplicación. Esta información la recopilan los beans TraceRepository que están registrados en la aplicación.

## Habilitación de puntos finales del actuador

Actuator Endpoints no están habilitados de forma predeterminada en Spring Boot. Podemos habilitarlos agregando la dependencia `spring-boot-actuator` a nuestro proyecto.

## Seguridad

Podemos asegurar nuestros puntos finales de actuador agregando Spring Security a nuestro proyecto. Podemos hacer esto agregando la dependencia `spring-boot-starter-security` a nuestro proyecto.

## Conclusión

En este artículo, analizamos qué son los puntos finales de Spring Boot Actuator y cómo podemos usarlos. También hemos visto cómo podemos habilitar y asegurar estos puntos finales.