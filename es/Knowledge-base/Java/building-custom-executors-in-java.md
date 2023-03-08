---
title: Creación de ejecutores personalizados en Java
description: 
published: true
date: 2023-02-02T23:57:28.250Z
tags: 
editor: markdown
dateCreated: 2023-02-02T23:57:23.578Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building Custom Executors in Java***English** document is available*](/en/Knowledge-base/Java/building-custom-executors-in-java)
{.links-list}


# Creación de ejecutores personalizados en Java

Los desarrolladores a menudo necesitan crear ejecutores personalizados para ejecutar tareas en paralelo. En este artículo, exploraremos cómo hacer esto en Java.

## Creación de un grupo de subprocesos

El primer paso para crear un ejecutor personalizado es crear un grupo de subprocesos. Esto se puede hacer usando la clase ```Executors```:

```java
ExecutorService executor = Executors.newFixedThreadPool(10);
```

Esto creará un grupo de subprocesos con 10 subprocesos. También puedes usar la clase ```Executors``` para crear un ejecutor de un solo subproceso:

```java
ExecutorService executor = Executors.newSingleThreadExecutor();
```

## Ejecutando Tareas

Una vez que tenga un ejecutor, puede enviarle tareas para su ejecución. Por ejemplo, supongamos que tiene una tarea ```Runnable```:

```java
Runnable task = () -> {
    // task logic here
};
```

Puedes enviar esta tarea al ejecutor para que la ejecute usando el método ```submit()```:

```java
executor.submit(task);
```

Si tiene una tarea ```Callable```, también puede enviarla utilizando el método ```submit()```:

```java
Callable<T> task = () -> {
    // task logic here
    return result;
};
```

## Terminar un grupo de subprocesos

Una vez que haya terminado de ejecutar las tareas, deberá cerrar el grupo de subprocesos. Esto se puede hacer usando el método ```shutdown()```:

```java
executor.shutdown();
```

Si desea cerrar el grupo de subprocesos inmediatamente, puede usar el método ```shutdownNow()```:

```java
executor.shutdownNow();
```

## Recursos

- [Tutorial de ejecutores de Java y grupos de subprocesos] (https://www.baeldung.com/java-executors-and-thread-pools)
- [Grupo de subprocesos Java](https://www.geeksforgeeks.org/java-thread-pool/)
- [Tutorial de Java ExecutorService](https://www.journaldev.com/1069/java-executor-service-example-thread-pool-executor)