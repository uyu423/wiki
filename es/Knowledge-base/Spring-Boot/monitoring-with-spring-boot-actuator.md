---
title: Supervisión con actuador Spring Boot
description: 
published: true
date: 2023-02-07T01:32:46.899Z
tags: 
editor: markdown
dateCreated: 2023-02-07T01:32:45.196Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Monitoring with Spring Boot Actuator***English** document is available*](/en/Knowledge-base/Spring-Boot/monitoring-with-spring-boot-actuator)
{.links-list}



# Monitoreo con actuador Spring Boot

Spring Boot Actuator es un subproyecto del marco Spring Boot que proporciona funciones listas para producción para ayudarlo a monitorear y administrar su aplicación. También le ayuda a la información auditada y de salud acerca de su aplicación. Spring Boot Actuator no está habilitado de forma predeterminada. Debe usar las anotaciones `@EnableAutoConfiguration` o `@SpringBootApplication` para habilitarlo.

## Habilitación del actuador Spring Boot

Para habilitar Spring Boot Actuator en su aplicación Spring Boot, debe agregar la dependencia `spring-boot-starter-actuator` a su archivo `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

También puede habilitar Spring Boot Actuator en su aplicación agregando las siguientes propiedades a su archivo `application.properties`:

```properties
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
```

## Supervisión con actuador Spring Boot

Spring Boot Actuator proporciona una serie de puntos finales listos para producción que puede usar para monitorear y administrar su aplicación. La siguiente tabla enumera los puntos finales más importantes:

| punto final | Descripción |
| --- | --- |
| `/salud` | Muestra información sobre el estado de la aplicación (predeterminado en "ARRIBA"). |
| `/información` | Muestra información de aplicación arbitraria. |
| `/métricas` | Muestra información de métricas de la aplicación. |
| `/rastreo` | Muestra información de seguimiento de la aplicación. |
| `/volcado` | Realiza un volcado de subprocesos. |
| `/joloquia` | Expone beans JMX sobre HTTP (requiere `jolokia-core`). |
| `/archivo de registro` | Devuelve el contenido del archivo de registro (si está configurado el registro). |
| `/actualizar` | Actualizar cachés de configuración y aplicaciones. |
| `/ruta de vuelo` | Muestra cualquier migración de base de datos de Flyway que se haya aplicado. |
| `/liquibase` | Muestra cualquier migración de base de datos de Liquibase que se haya aplicado. |

Los extremos `/health` e `/info` están protegidos de forma predeterminada. Para que sean de acceso público, debe agregar las siguientes propiedades a su archivo `application.properties`:

```properties
management.security.enabled=false
```

## Personalización del actuador Spring Boot

Spring Boot Actuator ofrece varias formas de personalizar su comportamiento.

### Cambio del puerto del servidor de administración

De manera predeterminada, Spring Boot Actuator usa el puerto `8080` para el servidor de administración. Puede cambiar esto agregando la siguiente propiedad a su archivo `application.properties`:

```properties
management.server.port=<port>
```

### Cambiar la ruta del servidor de administración

De manera predeterminada, Spring Boot Actuator usa la ruta `/actuator` para el servidor de administración. Puede cambiar esto agregando la siguiente propiedad a su archivo `application.properties`:

```properties
management.server.servlet.path=/<path>
```

### Cambio de ID de punto final

De forma predeterminada, Spring Boot Actuator usa los ID de punto final de la tabla anterior. Puede cambiarlos agregando la siguiente propiedad a su archivo `application.properties`:

```properties
management.endpoints.web.exposure.include=<endpoint1>,<endpoint2>,...
```

### Cambiar las rutas de puntos finales

De forma predeterminada, Spring Boot Actuator usa las rutas de puntos finales de la tabla anterior. Puede cambiarlos agregando la siguiente propiedad a su archivo `application.properties`:

```properties
management.endpoint.<endpoint>.path=/<path>
```

### Cambio de la información confidencial del endpoint

De forma predeterminada, Spring Boot Actuator expone información confidencial en los cuerpos de respuesta del punto final. Puede cambiar esto agregando la siguiente propiedad a su archivo `application.properties`:

```properties
management.endpoint.health.show-details=<value>
```

Donde `<valor>` puede ser uno de los siguientes:

| Valor | Descripción |
| --- | --- |
| `siempre` | Mostrar siempre los detalles. |
| `nunca` | Nunca muestres detalles. |
| `cuando_autorizado` | Mostrar detalles cuando el usuario está autorizado. |

### Cambio de la seguridad de punto final

De forma predeterminada, Spring Boot Actuator usa la autenticación básica HTTP para los puntos finales. Puede cambiar esto agregando la siguiente propiedad a su archivo `application.properties`:

```properties
management.security.enabled=false
```

### Cambiar el nombre de usuario y la contraseña del punto final

De forma predeterminada, Spring Boot Actuator usa el nombre de usuario `usuario` y la contraseña `contraseña` para los puntos finales. Puede cambiarlos agregando las siguientes propiedades a su archivo `application.properties`:

```properties
management.security.user.name=<username>
management.security.user.password=<password>
```

## Conclusión

En este artículo, analizamos cómo usar Spring Boot Actuator para monitorear y administrar su aplicación. También hemos visto cómo personalizar el comportamiento del actuador.