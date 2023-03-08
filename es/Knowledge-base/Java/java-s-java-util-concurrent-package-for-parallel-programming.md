---
title: Paquete java.util.concurrent de Java para programación paralela
description: 
published: true
date: 2023-02-01T21:57:42.366Z
tags: 
editor: markdown
dateCreated: 2023-02-01T21:57:40.658Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Java's java.util.concurrent Package for Parallel Programming***English** document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-package-for-parallel-programming)
{.links-list}


# Paquete java.util.concurrent de Java para programación paralela

El paquete `java.util.concurrent` proporciona un conjunto de clases e interfaces que admiten la programación multiproceso. Este paquete permite a los desarrolladores escribir fácilmente programas que aprovechan múltiples procesadores.

El paquete `java.util.concurrent` contiene los siguientes elementos:

* Ejecutores
* Futuros
* Grupos de subprocesos
* Cerraduras
* Variables Atómicas
* Colecciones concurrentes
* Sincronizadores

En este artículo, nos centraremos en cómo usar el paquete `java.util.concurrent` para escribir programas paralelos.

## Ejecutores

Un 'Ejecutor' es un objeto que ejecuta tareas 'Ejecutables' enviadas. La interfaz `Executor` proporciona una forma de desvincular el envío de tareas de la mecánica de cómo se ejecutará cada tarea, incluidas las colas, la programación y la ejecución.

Hay una serie de implementaciones integradas de `Executor` en el paquete `java.util.concurrent`, como `ThreadPoolExecutor` y `ScheduledThreadPoolExecutor`. También podemos crear nuestra propia implementación `Executor`.

En el siguiente ejemplo, creamos una tarea 'Ejecutable' y la enviamos a un 'Ejecutor' para su ejecución:

```java
Runnable task = () -> {
    // Do something
};

Executor executor = Executors.newSingleThreadExecutor();
executor.execute(task);
```

## Futuros

Un 'Futuro' representa el resultado de un cálculo asíncrono. Podemos usar un `Futuro` para verificar si el cálculo está completo y para recuperar el resultado del cálculo.

En el siguiente ejemplo, usamos un `Futuro` para comprobar si una tarea ha finalizado y recuperar el resultado:

```java
Future<Integer> future = executor.submit(task);

if (future.isDone()) {
    int result = future.get();
}
```

## Grupos de subprocesos

Un `ThreadPool` es una colección de `Threads` que se pueden usar para ejecutar tareas. Un `ThreadPool` administra los `Subprocesos` en el grupo y proporciona mecanismos para reutilizar `Subprocesos` cuando están disponibles.

En el siguiente ejemplo, creamos un `ThreadPool` con cuatro `Threads`:

```java
ExecutorService threadPool = Executors.newFixedThreadPool(4);
```

Podemos enviar tareas `Runnable` al `ThreadPool` para su ejecución:

```java
threadPool.submit(task);
```

Cuando hayamos terminado con `ThreadPool`, podemos apagarlo:

```java
threadPool.shutdown();
```

## Cerraduras

Un 'Bloqueo' es un mecanismo para controlar el acceso a un recurso compartido. Los bloqueos se pueden usar para implementar secciones críticas, que son secciones de código que deben ejecutarse de forma atómica.

En el siguiente ejemplo, usamos un `Bloqueo` para controlar el acceso a un recurso compartido:

```java
Lock lock = new ReentrantLock();

lock.lock();
try {
    // Access the shared resource
} finally {
    lock.unlock();
}
```

## Variables atómicas

Una `AtomicVariable` es una variable que se puede actualizar atómicamente. `AtomicVariable`s se utilizan para implementar secciones críticas.

En el siguiente ejemplo, usamos una `AtomicVariable` para controlar el acceso a un recurso compartido:

```java
AtomicInteger counter = new AtomicInteger();

int value = counter.incrementAndGet();
```

## Colecciones concurrentes

El paquete `java.util.concurrent` contiene una serie de colecciones simultáneas, que son colecciones que varios subprocesos pueden utilizar de forma segura.

En el siguiente ejemplo, usamos un `ConcurrentHashMap` para almacenar datos de forma segura para subprocesos:

```java
ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();

map.put("foo", 42);
map.get("foo");
```

## Sincronizadores

Un `Synchronizer` es un objeto que coordina las acciones de múltiples hilos. El paquete `java.util.concurrent` contiene varios sincronizadores, como `Semaphore` y `CountDownLatch`.

En el siguiente ejemplo, usamos `CountDownLatch` para esperar a que finalice una tarea:

```java
CountDownLatch latch = new CountDownLatch(1);

executor.submit(() -> {
    try {
        // Do something
        latch.countDown();
    } catch (InterruptedException e) {
        // Handle the exception
    }
});

latch.await();
```

## Conclusión

En este artículo, hemos visto cómo usar el paquete `java.util.concurrent` para escribir programas paralelos. Hemos visto cómo usar `Executors`, `Futures`, `ThreadPools`, `Locks`, `AtomicVariables`, `ConcurrentCollections` y `Synchronizers`.