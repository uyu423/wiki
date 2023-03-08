---
title: 093: comprensión y configuración del sistema de seguimiento Spring Boot
description: 
published: true
date: 2023-02-04T20:55:17.510Z
tags: 
editor: markdown
dateCreated: 2023-02-04T20:55:15.924Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [093: Understanding and Configuring the Spring Boot Tracing System***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/093-understanding-and-configuring-the-spring-boot-tracing-system)
{.links-list}


# 093: Comprender y configurar el sistema de seguimiento Spring Boot

Spring Boot proporciona un sistema de seguimiento que se puede usar para recopilar y ver información sobre las solicitudes que fluyen a través de un sistema. Esto puede ser útil para fines de depuración o para monitorear el rendimiento de un sistema.

En esta publicación, veremos cómo configurar el sistema de seguimiento Spring Boot y cómo usarlo para recopilar información sobre el procesamiento de solicitudes.

## Configuración del sistema de seguimiento Spring Boot

El sistema de rastreo Spring Boot se configura usando la propiedad `spring.sleuth` en el archivo `application.properties`. Las siguientes propiedades se pueden utilizar para configurar el sistema de seguimiento:

- `spring.sleuth.sampler.probability`: La probabilidad de que una solicitud sea muestreada. El valor predeterminado es 1.0, lo que significa que se muestrearán todas las solicitudes.

- `spring.sleuth.sampler.spans`: el número máximo de intervalos que se pueden crear para una sola solicitud. El valor predeterminado es 100.

- `spring.sleuth.trace-id128`: si se establece en verdadero, se generarán ID de seguimiento de 128 bits. El valor predeterminado es falso.

- `spring.sleuth.web.skip-pattern`: una expresión regular que se utiliza para determinar qué solicitudes no deben rastrearse. El valor predeterminado es `/salud`

Puede encontrar más información sobre estas propiedades en la [documentación de Spring Boot] (https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-tracing.html# boot-features- rastreo-primavera-detective).

## Recopilación de información de rastreo

El sistema de seguimiento Spring Boot se puede utilizar para recopilar información sobre el procesamiento de solicitudes. Esta información se puede recopilar de dos formas:

- Registrando la información en un archivo
- Enviando la información a un servidor [Zipkin](https://zipkin.io/)

### Registro de información de seguimiento en un archivo

El sistema de seguimiento Spring Boot se puede configurar para registrar información de seguimiento en un archivo. Esto se puede hacer configurando la propiedad `spring.sleuth.log.file` en el archivo `application.properties`. El siguiente es un ejemplo de cómo configurar el sistema de seguimiento para registrar información en un archivo:

```
spring.sleuth.log.file=traces.log
```

### Envío de información de seguimiento a un servidor Zipkin

El sistema de seguimiento Spring Boot se puede configurar para enviar información de seguimiento a un servidor Zipkin. Esto se puede hacer configurando la propiedad `spring.sleuth.zipkin.baseUrl` en el archivo `application.properties`. El siguiente es un ejemplo de cómo configurar el sistema de seguimiento para enviar información a un servidor Zipkin:

```
spring.sleuth.zipkin.baseUrl=http://localhost:9411
```

## Ver información de rastreo

### Registro de información de seguimiento en un archivo

Si el sistema de rastreo está configurado para registrar información en un archivo, la información se puede ver abriendo el archivo en un editor de texto. La información se registrará en formato [JSON](https://www.json.org/).

### Envío de información de seguimiento a un servidor Zipkin

Si el sistema de rastreo está configurado para enviar información a un servidor Zipkin, la información se puede ver abriendo el servidor Zipkin en un navegador web. El servidor Zipkin proporcionará una interfaz gráfica para ver la información de seguimiento.

## Conclusión

En esta publicación, analizamos cómo configurar el sistema de seguimiento Spring Boot y cómo usarlo para recopilar información sobre el procesamiento de solicitudes. También hemos visto cómo ver la información de seguimiento que recopila el sistema.