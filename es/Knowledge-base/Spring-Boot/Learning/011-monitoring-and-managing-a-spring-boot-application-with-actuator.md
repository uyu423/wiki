---
title: 011: Supervisión y gestión de una aplicación Spring Boot con Actuator
description: 
published: true
date: 2023-02-03T09:04:41.913Z
tags: 
editor: markdown
dateCreated: 2023-02-03T09:04:36.918Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [011: Monitoring and managing a Spring Boot application with Actuator***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/011-monitoring-and-managing-a-spring-boot-application-with-actuator)
{.links-list}


# Supervisión y gestión de una aplicación Spring Boot con Actuator

Actuator es una herramienta que se puede usar para monitorear y administrar una aplicación Spring Boot. Proporciona una serie de características que se pueden usar para monitorear y administrar la aplicación, que incluyen:

- Chequeo de salud
- Métricas
- Inicio sesión
- Configuración
- Puntos finales

En esta publicación, nos enfocaremos en usar Actuator para monitorear y administrar una aplicación Spring Boot. Primero veremos cómo configurar Actuator en una aplicación Spring Boot. Luego veremos cómo usar la función de verificación de estado de Actuator para monitorear el estado de nuestra aplicación. Finalmente, veremos cómo usar la función de métricas de Actuator para monitorear el rendimiento de nuestra aplicación.

## Configuración de Actuator en una aplicación Spring Boot

El actuador no está habilitado de forma predeterminada en una aplicación Spring Boot. Para habilitar Actuator, debemos agregar la siguiente dependencia a nuestro proyecto:

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Una vez que hayamos agregado la dependencia, podemos habilitar Actuator agregando las siguientes propiedades a nuestro archivo application.properties:

```
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
```

La primera propiedad, management.endpoints.web.exposure.include, expone todos los puntos finales de Actuator. La segunda propiedad, management.endpoint.health.show-details, garantiza que el extremo de verificación de estado incluya información detallada sobre el estado de nuestra aplicación.

## Uso de la función de verificación de estado de Actuator

La función de verificación de estado de Actuator se puede usar para monitorear el estado de nuestra aplicación. De forma predeterminada, Actuator proporciona una serie de comprobaciones de estado integradas, incluidas comprobaciones de la base de datos, el espacio en disco y JMS.

Además de las comprobaciones de estado integradas, también podemos agregar nuestras propias comprobaciones de estado personalizadas. Para agregar una verificación de estado personalizada, debemos crear una clase que implemente la interfaz HealthIndicator. Por ejemplo, la siguiente clase implementa una verificación de estado para un servicio que hemos llamado MyService:

```java
public class MyServiceHealthIndicator implements HealthIndicator {

   @Override
   public Health health() {
      // check the health of our service
      // if the service is healthy, return a Health.Builder with a status of UP
      // if the service is not healthy, return a Health.Builder with a status of DOWN
   }
}
```

Una vez que hayamos creado nuestro control de salud personalizado, debemos registrarlo con Spring. Podemos hacer esto agregando la anotación @Component a nuestra clase. Por ejemplo:

```java
@Component
public class MyServiceHealthIndicator implements HealthIndicator {

   @Override
   public Health health() {
      // check the health of our service
      // if the service is healthy, return a Health.Builder with a status of UP
      // if the service is not healthy, return a Health.Builder with a status of DOWN
   }
}
```

## Uso de la función de métricas de Actuator

La función de métricas de Actuator se puede utilizar para monitorear el rendimiento de nuestra aplicación. De forma predeterminada, Actuator proporciona una serie de métricas integradas, incluidas métricas para la base de datos, JMS y solicitudes web.

Además de las métricas integradas, también podemos agregar nuestras propias métricas personalizadas. Para agregar una métrica personalizada, debemos crear una clase que implemente la interfaz MetricWriter. Por ejemplo, la siguiente clase implementa una métrica para un servicio que hemos llamado MyService:

```java
public class MyServiceMetricWriter implements MetricWriter {

   @Override
   public void write(Metric<?> metric) {
      // write the metric to our monitoring system
   }
}
```

Una vez que hayamos creado nuestra métrica personalizada, debemos registrarla con Spring. Podemos hacer esto agregando la anotación @Component a nuestra clase. Por ejemplo:

```java
@Component
public class MyServiceMetricWriter implements MetricWriter {

   @Override
   public void write(Metric<?> metric) {
      // write the metric to our monitoring system
   }
}
```

## Conclusión

En esta publicación, hemos visto cómo usar Actuator para monitorear y administrar una aplicación Spring Boot. Hemos visto cómo configurar Actuator en una aplicación Spring Boot y cómo usar las funciones de métricas y verificación de estado de Actuator para monitorear el estado y el rendimiento de nuestra aplicación.