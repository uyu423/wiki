---
title: 079: Implementación del procesamiento asíncrono en una aplicación Spring Boot
description: 
published: true
date: 2023-02-05T10:32:15.825Z
tags: 
editor: markdown
dateCreated: 2023-02-05T10:32:14.253Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [079: Implementing Asynchronous Processing in a Spring Boot Application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/079-implementing-asynchronous-processing-in-a-spring-boot-application)
{.links-list}


# 079: Implementando Procesamiento Asíncrono en una Aplicación Spring Boot

El procesamiento asincrónico es una forma de procesar tareas de forma paralela o sin bloqueo. En una aplicación Spring Boot, el procesamiento asincrónico se puede usar para mejorar el rendimiento de las tareas de ejecución prolongada descargándolas en un subproceso separado.

En esta publicación, veremos cómo implementar el procesamiento asíncrono en una aplicación Spring Boot. Comenzaremos analizando los diferentes tipos de procesamiento asíncrono que se pueden usar en Spring Boot. Luego veremos cómo configurar Spring Boot para usar el procesamiento asíncrono. Finalmente, veremos algunos consejos para usar el procesamiento asíncrono en una aplicación Spring Boot.

## Tipos de procesamiento asíncrono

Hay dos tipos de procesamiento asíncrono que se pueden usar en Spring Boot:

* Procesamiento paralelo: Este es un tipo de procesamiento asíncrono donde las tareas se ejecutan en paralelo. El procesamiento en paralelo se puede utilizar para mejorar el rendimiento de las tareas de ejecución prolongada mediante la distribución del trabajo entre varios subprocesos.

* Procesamiento sin bloqueo: este es un tipo de procesamiento asíncrono en el que las tareas se ejecutan sin bloqueo. El procesamiento sin bloqueo se puede utilizar para mejorar la capacidad de respuesta de una aplicación al evitar la necesidad de esperar a que se completen las tareas de ejecución prolongada.

## Configuración del procesamiento asíncrono

Para usar el procesamiento asíncrono en una aplicación Spring Boot, debe configurar la aplicación para usar un ejecutor de tareas. Un ejecutor de tareas es un componente que se encarga de ejecutar tareas de forma paralela o sin bloqueo.

Spring Boot proporciona varios ejecutores de tareas diferentes que se pueden usar para diferentes tipos de procesamiento asíncrono. Por ejemplo, SimpleAsyncTaskExecutor se puede usar para el procesamiento en paralelo y CallableProcessingInterceptor se puede usar para el procesamiento sin bloqueo.

Para configurar la aplicación para usar un ejecutor de tareas, debe agregar la siguiente propiedad al archivo application.properties:

primavera.tarea.ejecutor.grupo.tamaño=10

Esta propiedad configura el tamaño del grupo de ejecutores de tareas. El grupo de ejecutores de tareas se utiliza para ejecutar tareas de forma paralela o sin bloqueo.

## Sugerencias para usar el procesamiento asíncrono

Cuando se utiliza el procesamiento asíncrono en una aplicación Spring Boot, hay algunas cosas que se deben tener en cuenta:

* Evite el uso de métodos sincrónicos: cuando use procesamiento asincrónico, evite usar métodos sincrónicos. Los métodos sincrónicos pueden bloquear el subproceso que ejecuta la tarea, lo que puede hacer que la tarea tarde más en completarse.

* Use un ejecutor de tareas: cuando use procesamiento asíncrono, asegúrese de usar un ejecutor de tareas. Un ejecutor de tareas puede ayudar a mejorar el rendimiento de las tareas de ejecución prolongada al distribuir el trabajo entre varios subprocesos.

* Use una devolución de llamada: cuando use procesamiento asíncrono, asegúrese de usar una devolución de llamada. Una devolución de llamada puede ayudar a mejorar la capacidad de respuesta de una aplicación al evitar la necesidad de esperar a que se completen las tareas de ejecución prolongada.