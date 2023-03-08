---
title: 060: Trabajar con el actuador Spring Boot para monitoreo
description: 
published: true
date: 2023-02-04T23:32:25.110Z
tags: 
editor: markdown
dateCreated: 2023-02-04T23:32:23.531Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [060: Working with Spring Boot's Actuator for Monitoring***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/060-working-with-spring-boot-s-actuator-for-monitoring)
{.links-list}


# Actuador de Spring Boot para monitoreo

Spring Boot's Actuator es una excelente herramienta para monitorear y administrar su aplicación Spring Boot. En esta publicación, veremos cómo usar Actuator para monitorear el estado y el rendimiento de su aplicación.

## ¿Qué es el actuador?

Actuator es un módulo Spring Boot que proporciona funciones listas para producción para ayudarlo a monitorear y administrar su aplicación. Con Actuator, puede monitorear la salud y el rendimiento de su aplicación e incluso crear un punto final personalizado para obtener información sobre el estado de su aplicación.

## ¿Cómo usar el actuador?

Para usar Actuator en su aplicación Spring Boot, debe agregar la siguiente dependencia a su `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Una vez que haya agregado la dependencia, puede comenzar a usar las funciones de Actuator.

## Monitoreo de la salud de su aplicación

Una de las características más importantes de Actuator es su capacidad para monitorear el estado de su aplicación. De forma predeterminada, Actuator expone un punto final `/health` que puede usar para verificar el estado de su aplicación.

El extremo `/health` devuelve una propiedad `status` que puede tener uno de los siguientes valores:

- `UP`: La aplicación está funcionando.
- `DOWN`: La aplicación está caída.
- `OUT_OF_SERVICE`: La aplicación está fuera de servicio.

El extremo `/salud` también devuelve una propiedad `detalles` que contiene más información sobre la salud de la aplicación. Por ejemplo, la propiedad `detalles` podría contener información sobre la conexión de la base de datos de la aplicación o la cantidad de subprocesos que se están ejecutando actualmente.

Además del punto final `/health`, Actuator también expone un punto final `/info` que puede usar para obtener información sobre su aplicación. El extremo `/info` devuelve una propiedad `build` que contiene información sobre la compilación de la aplicación, como el número de versión y la marca de tiempo de la compilación.

## Supervisión del rendimiento de su aplicación

Además de monitorear el estado de su aplicación, Actuator también puede ayudarlo a monitorear el rendimiento de su aplicación. Actuator expone una serie de puntos finales relacionados con el rendimiento, como `/metrics`, `/dump` y `/trace`.

El extremo `/metrics` devuelve una serie de métricas relacionadas con el rendimiento, como la cantidad de solicitudes que se han procesado, el tiempo de respuesta promedio y la cantidad de errores que se han producido.

El extremo `/dump` devuelve un volcado de subprocesos de la aplicación, que puede ser útil para fines de depuración.

El extremo `/trace` devuelve un seguimiento de la aplicación, que puede ser útil para comprender el flujo de la aplicación.

## Creando un punto final personalizado

Además del punto final integrado, Actuator también le permite crear un punto final personalizado. Para crear un punto final personalizado, debe crear una clase que implemente la interfaz "Punto final".

Por ejemplo, la siguiente clase crea un extremo `/myendpoint` personalizado que devuelve una propiedad `message`:

```java
@Component
public class MyEndpoint implements Endpoint<Map<String, String>> {

    @Override
    public String getId() {
        return "/myendpoint";
    }

    @Override
    public Map<String, String> invoke() {
        Map<String, String> result = new HashMap<>();
        result.put("message", "Hello, world!");
        return result;
    }

    @Override
    public boolean isSensitive() {
        return false;
    }

}
```

## Conclusión

En esta publicación, hemos visto cómo usar el Actuador de Spring Boot para monitorear su aplicación. Actuator es una excelente herramienta para monitorear el estado y el rendimiento de su aplicación. Además, Actuator le permite crear puntos finales personalizados para obtener información sobre su aplicación.