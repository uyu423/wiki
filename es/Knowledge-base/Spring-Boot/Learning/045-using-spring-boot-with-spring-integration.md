---
title: 045: Uso de Spring Boot con Spring Integration
description: 
published: true
date: 2023-02-04T11:32:17.052Z
tags: 
editor: markdown
dateCreated: 2023-02-04T11:32:15.442Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [045: Using Spring Boot with Spring Integration***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/045-using-spring-boot-with-spring-integration)
{.links-list}


# Usar Spring Boot con Spring Integration

En esta publicación, veremos cómo usar Spring Boot con Spring Integration. Repasaremos los conceptos básicos de Spring Integration y mostraremos cómo usarlo con Spring Boot.

## ¿Qué es la integración de primavera?

Spring Integration es un marco que amplía Spring Framework para proporcionar soporte para patrones de integración empresarial. Estos patrones se utilizan para facilitar la comunicación entre diferentes aplicaciones y sistemas.

Spring Integration proporciona adaptadores para una variedad de tecnologías diferentes, como JMS, HTTP y FTP. También proporciona soporte para canales de mensajes, enrutadores de mensajes y transformadores de mensajes.

## ¿Por qué usar Spring Integration?

Spring Integration le permite crear aplicaciones a escala empresarial que son resistentes y escalables. Le ayuda a evitar el bloqueo de proveedores al proporcionar un modelo de programación coherente en diferentes tecnologías.

## Empezando

En esta sección, le mostraremos cómo comenzar con Spring Integration. Repasaremos las diferentes dependencias que necesitará y le mostraremos cómo configurar Spring Integration.

### Dependencias

Primero, deberá agregar las siguientes dependencias a su proyecto:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-integration</artifactId>
    </dependency>
</dependencies>
```

Estas dependencias obtendrán los archivos jar necesarios para Spring Integration.

### Configuración

A continuación, deberá configurar Spring Integration. Puede hacer esto agregando lo siguiente a su archivo `application.properties`:

```properties
spring.integration.dsl.enabled=true
```

Esto habilitará Spring Integration Java DSL.

## Conclusión

En esta publicación, echamos un vistazo a cómo usar Spring Boot con Spring Integration. Hemos repasado los conceptos básicos de Spring Integration y mostramos cómo comenzar con él.