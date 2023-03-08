---
title: 043: Implementando una tarea programada en una aplicación Spring Boot
description: 
published: true
date: 2023-02-04T09:32:17.557Z
tags: 
editor: markdown
dateCreated: 2023-02-04T09:32:12.341Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [043: Implementing a scheduled task in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/043-implementing-a-scheduled-task-in-a-spring-boot-application)
{.links-list}


# Implementando una tarea programada en una aplicación Spring Boot

En esta publicación, veremos cómo implementar una tarea programada en una aplicación Spring Boot. Spring Boot proporciona una manera simple y conveniente de ejecutar tareas programadas.

## Programación de tareas

Spring Boot proporciona una anotación @Scheduled que se puede usar en métodos para marcarlos como tareas que deben ejecutarse periódicamente. Por ejemplo, podemos usar la anotación @Scheduled para ejecutar una tarea cada minuto:

```java
@Scheduled(cron = "0 * * * * ?")
public void runEveryMinute() {
    // do something
}
```

En el ejemplo anterior, estamos usando una expresión cron para programar la tarea. Las expresiones cron son una forma conveniente de especificar cuándo se debe ejecutar una tarea. Para obtener más información sobre las expresiones cron, consulte los documentos java [CronTrigger](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/scheduling/support/CronTrigger.html).

## Ejecutar tareas en una aplicación Spring Boot

Para ejecutar la tarea en nuestra aplicación Spring Boot, solo necesitamos anotar nuestra clase principal con la anotación @EnableScheduling:

```java
@SpringBootApplication
@EnableScheduling
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## Información adicional

- Para obtener más información sobre la programación de tareas en Spring Boot, consulte la [documentación de Spring Boot] (https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-scheduling.html).
- Para obtener más información sobre el uso de la anotación @Scheduled, consulte la [documentación de Spring](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/scheduling/annotation/Scheduled.html) .