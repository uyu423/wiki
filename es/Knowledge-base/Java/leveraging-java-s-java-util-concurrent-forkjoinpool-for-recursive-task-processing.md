---
title: Aprovechamiento de java.util.concurrent.ForkJoinPool de Java para el procesamiento recursivo de tareas
description: 
published: true
date: 2023-02-04T21:17:23.914Z
tags: 
editor: markdown
dateCreated: 2023-02-04T21:17:22.310Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Leveraging Java's java.util.concurrent.ForkJoinPool for Recursive Task Processing***English** document is available*](/en/Knowledge-base/Java/leveraging-java-s-java-util-concurrent-forkjoinpool-for-recursive-task-processing)
{.links-list}


# Aprovechar java.util.concurrent.ForkJoinPool de Java para el procesamiento recursivo de tareas

ForkJoinPool de Java es una poderosa herramienta para el procesamiento de tareas recursivas, lo que permite una ejecución de tareas mucho más eficiente de lo que es posible con un solo hilo. En este artículo, veremos cómo usar ForkJoinPool para procesar tareas de forma recursiva, con un enfoque en cómo administrar adecuadamente la seguridad de subprocesos.

## ¿Qué es ForkJoinPool?

ForkJoinPool es un Java ExecutorService que se especializa en ejecutar ForkJoinTasks. Una ForkJoinTask es una tarea que se puede dividir en subtareas más pequeñas, que se pueden ejecutar simultáneamente. ForkJoinPool distribuirá automáticamente las tareas entre los subprocesos disponibles y también reutilizará automáticamente los subprocesos que ya se han utilizado para otras tareas.

## ¿Por qué usar ForkJoinPool?

ForkJoinPool tiene una serie de ventajas sobre un ExecutorService tradicional. Primero, está diseñado para aprovechar múltiples procesadores, si están disponibles. En segundo lugar, utiliza el robo de trabajo para distribuir tareas entre subprocesos. Esto significa que si un subproceso está inactivo, puede robar trabajo de otro subproceso que está ocupado. Esto puede conducir a un uso mucho más eficiente de los subprocesos y, a menudo, puede conducir a tiempos de ejecución generales más cortos.

## Cómo usar ForkJoinPool

Usar ForkJoinPool es relativamente simple. Primero, crea un ForkJoinPool:

```java
ForkJoinPool pool = new ForkJoinPool();
```

A continuación, cree una ForkJoinTask. Hay dos tipos de ForkJoinTasks: RecursiveAction y RecursiveTask. RecursiveAction se usa para tareas que no devuelven un resultado, mientras que RecursiveTask se usa para tareas que devuelven un resultado. En este ejemplo, usaremos una RecursiveTask:

```java
RecursiveTask<Integer> task = new RecursiveTask<Integer>() {
    protected Integer compute() {
        // TODO: compute something
    }
};
```

Tenga en cuenta que el método compute() es donde se realizará el trabajo de la tarea. Aquí es donde colocaría el código que divide la tarea en subtareas más pequeñas y luego ejecuta esas subtareas.

Una vez que se crea la tarea, se puede enviar a ForkJoinPool para su ejecución:

```java
pool.submit(task);
```

El método submit() devolverá un objeto Future, que se puede usar para verificar el estado de la tarea o para obtener el resultado de la tarea (si es una RecursiveTask).

## Seguridad de subprocesos

Al usar ForkJoinPool, es importante tener en cuenta el potencial de problemas de seguridad de subprocesos. Esto se debe a que varios subprocesos pueden ejecutar una ForkJoinTask al mismo tiempo. Como resultado, cualquier código ejecutado por una ForkJoinTask debe sincronizarse correctamente.

Hay algunas formas de lograr una sincronización adecuada. La forma más sencilla es utilizar la palabra clave sincronizada de Java. Por ejemplo, si tiene una estructura de datos compartida a la que accede ForkJoinTask, puede usar la palabra clave sincronizada para asegurarse de que solo un subproceso pueda acceder a la estructura de datos a la vez:

```java
synchronized(data) {
    // TODO: access data
}
```

Otra forma de lograr una sincronización adecuada es usar las clases Atomic de Java. Estas clases proporcionan una serie de operaciones atómicas que se pueden utilizar para acceder de forma segura a los datos compartidos. Por ejemplo, la clase AtomicInteger proporciona una operación de incremento atómico:

```java
AtomicInteger i = new AtomicInteger();
// TODO: increment i
i.incrementAndGet();
```

Las clases atómicas se pueden usar para mucho más que simplemente incrementar un valor. También se pueden usar para operaciones como agregar dos valores o comparar e intercambiar. Consulte la documentación de Java para obtener más información sobre las clases Atomic.

## Conclusión

ForkJoinPool es una herramienta poderosa para el procesamiento de tareas recursivas y puede conducir a una ejecución de tareas mucho más eficiente de lo que es posible con un solo hilo. Al usar ForkJoinPool, es importante tener en cuenta el potencial de problemas de seguridad de subprocesos y tomar medidas para garantizar que su código esté correctamente sincronizado.