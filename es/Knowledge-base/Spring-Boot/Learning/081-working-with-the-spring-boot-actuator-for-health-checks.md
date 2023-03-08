---
title: 081: Trabajo con el actuador Spring Boot para controles de estado
description: 
published: true
date: 2023-02-05T12:32:18.494Z
tags: 
editor: markdown
dateCreated: 2023-02-05T12:32:16.947Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [081: Working with the Spring Boot Actuator for Health Checks***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/081-working-with-the-spring-boot-actuator-for-health-checks)
{.links-list}


# ¿Qué es el actuador Spring Boot para controles de estado?

Spring Boot Actuator for Health Checks es una herramienta que permite a los desarrolladores comprobar fácilmente el estado de sus aplicaciones. Se puede utilizar para supervisar el rendimiento de la aplicación, identificar posibles problemas y proporcionar información sobre el estado general de la aplicación.

Spring Boot Actuator for Health Checks es una herramienta integrada que se incluye con el marco Spring Boot. Es fácil de usar y proporciona una gran cantidad de información sobre el estado de una aplicación.

# ¿Por qué usar el actuador Spring Boot para las comprobaciones de estado?

Spring Boot Actuator for Health Checks es una herramienta valiosa para los desarrolladores. Puede ayudar a identificar posibles problemas con una aplicación y proporcionar información sobre el estado general de la aplicación.

Spring Boot Actuator for Health Checks es fácil de usar y proporciona una gran cantidad de información. Es una herramienta valiosa para los desarrolladores que desean monitorear la salud de sus aplicaciones.

# Cómo usar el actuador Spring Boot para controles de salud

Usar Spring Boot Actuator para Health Checks es fácil. Simplemente agregue la siguiente dependencia a su proyecto:

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Una vez que haya agregado la dependencia, puede acceder al extremo del actuador agregando lo siguiente a su archivo application.properties:

```properties
management.endpoints.web.exposure.include=health
```

A continuación, puede acceder al extremo de estado en http://localhost:8080/actuator/health.

# Conclusión

Spring Boot Actuator for Health Checks es una herramienta valiosa para los desarrolladores. Es fácil de usar y proporciona una gran cantidad de información sobre el estado de una aplicación. Es una herramienta valiosa para los desarrolladores que desean monitorear la salud de sus aplicaciones.