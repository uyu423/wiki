---
title: 003: comprensión de la configuración automática de Spring Boot
description: 
published: true
date: 2023-02-03T07:17:17.044Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:17:15.502Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [003: Understanding Spring Boot auto-configuration***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/003-understanding-spring-boot-auto-configuration)
{.links-list}


## Comprender la configuración automática de Spring Boot

La configuración automática de Spring Boot es una característica que configura automáticamente las aplicaciones de Spring en función de las dependencias presentes en el proyecto. Esto significa que, por ejemplo, si Hibernate está en el classpath, Spring Boot configurará automáticamente una fuente de datos y una fábrica de administradores de entidades.

La función de configuración automática está habilitada de forma predeterminada en Spring Boot. Sin embargo, se puede deshabilitar configurando la propiedad spring.boot.autoconfigure.EnableAutoConfiguration en falso.

Cuando la configuración automática está habilitada, Spring Boot intentará configurar la aplicación en función de las dependencias presentes en el proyecto. Por ejemplo, si Hibernate está en el classpath, Spring Boot configurará automáticamente una fuente de datos y una fábrica de administradores de entidades.

La configuración automática puede ser una característica útil cuando comienza a usar Spring Boot. Sin embargo, a medida que crezca su aplicación, es probable que desee desactivar la configuración automática para ciertas partes de la aplicación.

Para obtener más información sobre la configuración automática de Spring Boot, consulte los siguientes recursos:

- [La función de configuración automática en Spring Boot](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-auto-configuration.html)

- [Deshabilitar la configuración automática en Spring Boot](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-auto-configuration.html# boot-features-auto -configuración-excluir)