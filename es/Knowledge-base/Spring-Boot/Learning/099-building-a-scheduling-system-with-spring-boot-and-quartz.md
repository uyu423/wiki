---
title: 099: Creación de un sistema de programación con Spring Boot y Quartz
description: 
published: true
date: 2023-02-06T03:32:28.850Z
tags: 
editor: markdown
dateCreated: 2023-02-06T03:32:27.110Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [099: Building a Scheduling System with Spring Boot and Quartz***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/099-building-a-scheduling-system-with-spring-boot-and-quartz)
{.links-list}


# 099: Construyendo un Sistema de Programación con Spring Boot y Quartz

Quartz es una biblioteca de programación potente y ampliamente utilizada que se puede integrar con Spring Boot para programar tareas en nuestras aplicaciones. En esta publicación, veremos cómo crear un sistema de programación con Spring Boot y Quartz.

## Requisitos previos

Antes de comenzar, deberá tener instalado lo siguiente en su máquina:

-Java8
- Experto 3.x

## Configuración del proyecto

Empecemos configurando nuestro proyecto. Usaremos Spring Boot para nuestro ejemplo, por lo que necesitaremos crear un nuevo proyecto Maven con las siguientes dependencias:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-quartz</artifactId>
    </dependency>
</dependencies>
```

## Configuración de cuarzo

A continuación, necesitamos configurar Quartz. Podemos hacer esto creando un nuevo archivo llamado `quartz.properties` en el directorio `src/main/resources` con los siguientes contenidos:

```properties
org.quartz.scheduler.instanceName=MyScheduler
org.quartz.scheduler.instanceId=AUTO

org.quartz.threadPool.threadCount=5

org.quartz.jobStore.class=org.quartz.simpl.RAMJobStore
```

Esto configurará Quartz con algunas configuraciones básicas. Para obtener más información sobre la configuración de Quartz, consulte la [documentación de Quartz] (http://www.quartz-scheduler.org/documentation/quartz-2.x/configuration/).

## Creando un trabajo

Ahora que tenemos configurado Quartz, vamos a crear un trabajo. Los trabajos en Quartz son clases simples de Java que implementan la interfaz `org.quartz.Job`. Para nuestro ejemplo, crearemos un trabajo que simplemente imprima un mensaje en la consola.

```java
public class MyJob implements Job {

    @Override
    public void execute(JobExecutionContext context) throws JobExecutionException {
        System.out.println("Hello, world!");
    }

}
```

## Programar un trabajo

Ahora que tenemos un trabajo, tenemos que programarlo. Hay dos formas de hacerlo: mediante código o mediante anotaciones.

### Programar un trabajo mediante código

Para programar un trabajo a través del código, debemos hacer lo siguiente:

1. Cree una instancia `org.quartz.Trigger` que defina cuándo debe ejecutarse el trabajo.
2. Registre el trabajo y dispare con el programador de Quartz.

He aquí un ejemplo de cómo hacer esto:

```java
@Component
public class MyJobScheduler {

    @Autowired
    private Scheduler scheduler;

    public void scheduleJob() throws SchedulerException {
        JobDetail job = JobBuilder.newJob(MyJob.class)
            .withIdentity("myJob", "group1")
            .build();

        Trigger trigger = TriggerBuilder.newTrigger()
            .withIdentity("myTrigger", "group1")
            .startNow()
            .withSchedule(SimpleScheduleBuilder.simpleSchedule()
                .withIntervalInSeconds(5)
                .repeatForever())
            .build();

        scheduler.scheduleJob(job, trigger);
    }
}
```

En el código anterior, hemos creado un componente `MyJobScheduler` que programa una instancia de `MyJob` para que se ejecute cada 5 segundos.

### Programar un trabajo a través de anotaciones

Alternativamente, podemos programar un trabajo a través de anotaciones. Para hacer esto, simplemente necesitamos anotar nuestra clase `MyJob` con `@DisallowConcurrentExecution` y `@Scheduled`.

```java
@DisallowConcurrentExecution
@Scheduled(cron = "0/5 * * * * ?")
public class MyJob implements Job {

    @Override
    public void execute(JobExecutionContext context) throws JobExecutionException {
        System.out.println("Hello, world!");
    }

}
```

En el código anterior, hemos anotado nuestra clase `MyJob` con `@DisallowConcurrentExecution` para garantizar que solo se ejecute una instancia del trabajo a la vez. También lo hemos anotado con `@Scheduled`, que toma una expresión cron que define cuándo debe ejecutarse el trabajo. En este caso, estamos ejecutando el trabajo cada 5 segundos.

## Ejecutando el ejemplo

Ahora que tenemos nuestro proyecto configurado, ¡vamos a ejecutarlo y ver nuestro trabajo en acción! Para hacer esto, simplemente ejecute el método `principal` en la clase `MyJobScheduler`. Debería ver el siguiente resultado:

```
Hello, world!
Hello, world!
Hello, world!
...
```

## Conclusión

En esta publicación, hemos repasado cómo crear un sistema de programación con Spring Boot y Quartz. Hemos visto cómo configurar Quartz y cómo programar trabajos mediante código o anotaciones.

Para obtener más información sobre Quartz, consulte la [documentación de Quartz] (http://www.quartz-scheduler.org/documentation/quartz-2.x/).