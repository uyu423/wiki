---
title: 080: Comprensión y uso de las métricas de Spring Boot para el monitoreo
description: 
published: true
date: 2023-02-05T11:32:25.195Z
tags: 
editor: markdown
dateCreated: 2023-02-05T11:32:19.686Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [080: Understanding and Using the Spring Boot Metrics for Monitoring***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/080-understanding-and-using-the-spring-boot-metrics-for-monitoring)
{.links-list}


# Introducción

El monitoreo es una parte crítica de cualquier proceso de desarrollo de software. Permite a los desarrolladores identificar y diagnosticar problemas con sus aplicaciones en producción.

Spring Boot proporciona una serie de métricas integradas para monitorear aplicaciones. En esta publicación, veremos qué son las métricas de Spring Boot y cómo usarlas para monitorear sus aplicaciones.

# ¿Qué son las métricas de Spring Boot?

Las métricas de Spring Boot son un conjunto de herramientas para monitorear aplicaciones basadas en Spring. Proporcionan información sobre el comportamiento en tiempo de ejecución de las aplicaciones y se pueden utilizar para identificar cuellos de botella en el rendimiento.

Las métricas de Spring Boot están diseñadas para usarse con una variedad de herramientas de monitoreo, como Prometheus, Graphite y StatsD.

# Cómo usar las métricas de Spring Boot

Spring Boot proporciona varias formas de configurar y usar métricas. En esta sección, veremos algunas de las opciones de configuración más importantes.

## Habilitación de métricas

Las métricas están deshabilitadas de forma predeterminada en Spring Boot. Para habilitar las métricas, debe agregar la siguiente propiedad al archivo `application.properties` de su aplicación:

```
spring.metrics.enable=true
```

## Configuración de métricas

Spring Boot le permite configurar una serie de aspectos del sistema de métricas. Por ejemplo, puede configurar el registro predeterminado, el prefijo del nombre de la métrica y el formato de exportación.

La siguiente propiedad se puede utilizar para configurar el registro predeterminado:

```
spring.metrics.default-registry=my-registry
```

La siguiente propiedad se puede utilizar para configurar el prefijo del nombre de la métrica:

```
spring.metrics.prefix=my-prefix
```

La siguiente propiedad se puede utilizar para configurar el formato de exportación:

```
spring.metrics.export.format=json
```

## Exportación de métricas

Spring Boot admite varias formas de exportar métricas. La forma más común es usar el punto final `/metrics`. Este punto final expone las métricas en el formato Prometheus de forma predeterminada.

También puede usar el extremo `/metrics/{name}` para exportar una sola métrica. Por ejemplo, el siguiente punto final exportaría la métrica `jvm.memory.used`:

```
/metrics/jvm.memory.used
```

# Conclusión

En esta publicación, analizamos las métricas de Spring Boot y cómo usarlas para monitorear sus aplicaciones. También hemos visto cómo habilitar y configurar métricas, y cómo exportar métricas para usarlas con herramientas de monitoreo.