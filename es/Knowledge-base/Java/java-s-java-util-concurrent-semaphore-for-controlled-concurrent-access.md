---
title: java.util.concurrent.Semaphore de Java para acceso concurrente controlado
description: 
published: true
date: 2023-02-02T01:23:26.368Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:23:24.777Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Java's java.util.concurrent.Semaphore for Controlled Concurrent Access***English** document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-semaphore-for-controlled-concurrent-access)
{.links-list}


# java.util.concurrent.Semaphore de Java para acceso concurrente controlado

En la programación de subprocesos múltiples, a menudo es necesario limitar la cantidad de subprocesos que pueden acceder a un recurso o bloque de código en un momento dado. Esto se conoce como control de concurrencia.

Una forma de lograr el control de concurrencia en Java es usar la clase `java.util.concurrent.Semaphore`.

Un semáforo es un token que permite que un subproceso ingrese a una sección crítica, que es un bloque de código que solo puede ser ejecutado por un subproceso a la vez. Cuando el subproceso sale de la sección crítica, devuelve el semáforo al grupo.

Se puede usar un semáforo para controlar el acceso a cualquier recurso, no solo al código. Por ejemplo, se puede usar un semáforo para controlar el acceso a una impresora o base de datos.

## Crear un semáforo

Se crea un semáforo especificando el número de permisos. Este es el número de subprocesos que pueden acceder a la sección crítica al mismo tiempo. Por ejemplo, para crear un semáforo con 10 permisos:

```java
Semaphore semaphore = new Semaphore(10);
```

## Solicitud de un permiso

Un hilo solicita un permiso llamando al método `acquire()`. Este método bloquea el subproceso hasta que haya un permiso disponible. Por ejemplo:

```java
semaphore.acquire();
```

## Liberación de un permiso

Cuando un hilo sale de la sección crítica, llama al método `release()` para devolver el permiso al semáforo. Por ejemplo:

```java
semaphore.release();
```

## Ejemplo

El siguiente ejemplo muestra cómo usar un semáforo para controlar el acceso a una impresora.

```java
import java.util.concurrent.Semaphore;

public class Printer {
    private Semaphore semaphore;

    public Printer(int numPermits) {
        semaphore = new Semaphore(numPermits);
    }

    public void print(String document) {
        try {
            semaphore.acquire();
            // print the document
        } catch (InterruptedException e) {
            // handle error
        } finally {
            semaphore.release();
        }
    }
}
```

En este ejemplo, el método `print()` adquiere un permiso antes de imprimir el documento. Si no hay permisos disponibles, el método `acquire()` bloquea el hilo hasta que haya uno disponible. Después de imprimir el documento, el método `release()` devuelve el permiso al semáforo.

## Diferencias entre semáforos y candados

Los semáforos y los candados son ambos mecanismos para el control de concurrencia. Sin embargo, hay algunas diferencias clave entre ellos.

- Un semáforo puede tener múltiples permisos, mientras que una cerradura solo puede tener uno.
- Un semáforo puede ser liberado por un hilo que no lo adquirió, mientras que un bloqueo solo puede ser liberado por el hilo que lo adquirió.
- Un semáforo no tiene concepto de propiedad, mientras que un candado sí.

## Conclusión

La clase `java.util.concurrent.Semaphore` de Java proporciona un mecanismo para el control de concurrencia. Los semáforos se pueden usar para controlar el acceso a cualquier recurso, no solo al código. Al usar semáforos, es importante recordar las diferencias entre semáforos y candados.