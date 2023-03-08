---
title: 090: Implementación de un sistema de registro personalizado en Spring Boot
description: 
published: true
date: 2023-02-05T20:32:24.890Z
tags: 
editor: markdown
dateCreated: 2023-02-05T20:32:19.515Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [090: Implementing a Custom Logging System in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/090-implementing-a-custom-logging-system-in-spring-boot)
{.links-list}


# Implementación de un sistema de registro personalizado en Spring Boot

El registro es una parte crítica de cualquier aplicación. Puede ayudarnos a depurar problemas, rastrear eventos y monitorear el rendimiento. El sistema de registro predeterminado en Spring Boot es Logback, pero también podemos usar nuestro propio sistema de registro personalizado. En esta publicación, veremos cómo implementar un sistema de registro personalizado en Spring Boot.

## Iniciar sesión en Spring Boot

Antes de sumergirnos en cómo implementar un sistema de registro personalizado, demos un paso atrás y entendamos cómo funciona el registro en Spring Boot. Spring Boot usa Logback de forma predeterminada para iniciar sesión. Logback es un excelente marco de registro que tiene muchas características, como:

- Soporte para múltiples niveles de registro (por ejemplo, DEPURACIÓN, INFORMACIÓN, ADVERTENCIA, ERROR)
- La capacidad de iniciar sesión en múltiples destinos (por ejemplo, consola, archivos, base de datos)
- Recarga automática de archivos de configuración

Logback se configura usando un archivo llamado `logback.xml`. Este archivo normalmente se encuentra en el directorio `src/main/resources`. El contenido del archivo `logback.xml` se puede personalizar para cambiar el comportamiento de registro de nuestra aplicación. Por ejemplo, podemos cambiar el nivel de registro, agregar anexadores o cambiar el formato del registro.

## Implementación de un sistema de registro personalizado

Ahora que hemos cubierto los conceptos básicos del inicio de sesión en Spring Boot, echemos un vistazo a cómo implementar un sistema de registro personalizado. Lo primero que debemos hacer es crear un archivo llamado `log4j2.xml` en el directorio `src/main/resources`. El contenido de este archivo será similar al archivo `logback.xml`, pero usaremos Log4j2 en lugar de Logback.

A continuación, debemos agregar la siguiente dependencia a nuestro archivo `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.logging.log4j</groupId>
    <artifactId>log4j-api</artifactId>
    <version>2.11.1</version>
</dependency>
```

Finalmente, necesitamos agregar la siguiente propiedad a nuestro archivo `application.properties`:

```
logging.config=classpath:log4j2.xml
```

Esto le indicará a Spring Boot que use nuestro archivo `log4j2.xml` para la configuración de registro.

## Conclusión

En esta publicación, hemos visto cómo implementar un sistema de registro personalizado en Spring Boot. También hemos visto cómo configurar Log4j2 y cómo cambiar el nivel de registro.