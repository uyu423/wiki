---
title: Una guía para java.util.concurrent.locks.Condition de Java para la señalización de subprocesos
description: 
published: true
date: 2023-02-04T02:55:25.532Z
tags: 
editor: markdown
dateCreated: 2023-02-04T02:55:20.088Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [A Guide to Java's java.util.concurrent.locks.Condition for Thread Signaling***English** document is available*](/en/Knowledge-base/Java/a-guide-to-java-s-java-util-concurrent-locks-condition-for-thread-signaling)
{.links-list}



# Una guía para java.util.concurrent.locks.Condition de Java para la señalización de subprocesos

Los subprocesos a menudo necesitan comunicarse entre sí. Por ejemplo, un subproceso puede necesitar decirles a otros subprocesos que se realizó una tarea o que un recurso compartido está disponible.

Java tiene un mecanismo incorporado para la comunicación de subprocesos, llamado clase `java.util.concurrent.locks.Condition`. En este artículo, veremos cómo usar `Condición` para comunicarse entre hilos.

## ¿Qué es la condición?

La condición es una clase de Java que permite que los subprocesos esperen o señalen otros subprocesos. Es parte del paquete `java.util.concurrent.locks`, que también contiene la clase `Lock`.

Condition funciona con Lock para proporcionar una forma más flexible de controlar cuándo se pueden ejecutar los subprocesos. Con Lock, un subproceso solo puede ejecutarse cuando mantiene el bloqueo. Con Condición, un subproceso puede ejecutarse solo cuando otro subproceso lo ha señalado.

## Condición de uso

Condition funciona con Lock para proporcionar una forma más flexible de controlar cuándo se pueden ejecutar los subprocesos. Con Lock, un subproceso solo puede ejecutarse cuando mantiene el bloqueo. Con Condición, un subproceso puede ejecutarse solo cuando otro subproceso lo ha señalado.

Aquí hay un ejemplo simple de cómo se puede usar Condition. Supongamos que tenemos un recurso compartido que puede estar en uno de dos estados: vacío o lleno. Tenemos dos hilos: uno que produce el recurso y otro que lo consume.

Queremos asegurarnos de que el subproceso del consumidor solo intente consumir el recurso cuando esté en el estado "lleno", y que el subproceso del productor solo intente producir el recurso cuando esté en el estado "vacío". Para hacer esto, podemos usar un Bloqueo y una Condición:


```java
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class Resource {
    private final Lock lock = new ReentrantLock();
    private final Condition isEmpty = lock.newCondition();
    private final Condition isFull = lock.newCondition();

    private boolean empty = true;

    public void produce() throws InterruptedException {
        lock.lock();
        try {
            while (!empty) {
                isEmpty.await();
            }
            // produce resource
            empty = false;
            isFull.signalAll();
        } finally {
            lock.unlock();
        }
    }

    public void consume() throws InterruptedException {
        lock.lock();
        try {
            while (empty) {
                isFull.await();
            }
            // consume resource
            empty = true;
            isEmpty.signalAll();
        } finally {
            lock.unlock();
        }
    }
}
```

En este ejemplo, el método `produce()` primero verifica si el recurso está vacío. Si no es así, espera hasta que esté vacío (llamando a `isEmpty.await()`). Una vez que el recurso está vacío, produce el recurso y señala cualquier subproceso en espera (llamando a `isFull.signalAll()`).

De manera similar, el método `consume()` primero verifica si el recurso está lleno. Si no es así, espera hasta que esté lleno (llamando a `isFull.await()`). Una vez que el recurso está lleno, consume el recurso y señala cualquier subproceso en espera (llamando a `isEmpty.signalAll()`).

## Otros metodos

Condition también proporciona un método `signal()`, que activa un solo hilo que está esperando la condición. Si hay varios subprocesos esperando, uno de ellos se elegirá al azar para despertar.

También hay un método `awaitUninterruptably()`, que es similar a `await()` excepto que no lanza una InterruptedException si el hilo se interrumpe.

## Consejos para usar la condición

Aquí hay algunos consejos para usar Condition:

- Llama siempre a `await()` o `signal()` dentro de un bucle. Esto se debe a que `await()` puede interrumpirse (mediante una llamada a `interrupt()`), y `signal()` puede perderse (si hay varios subprocesos esperando, solo uno de ellos se activará).

- Tenga cuidado de no llamar a `await()` o `signal()` fuera de un candado. Si lo hace, otro hilo podría adquirir el bloqueo entre el momento en que comprueba la condición y el momento en que llama a `await()` o `signal()`. Esto podría causar que su programa se congele.

- Cuando utilice varias condiciones, tenga cuidado de no utilizar el mismo bloqueo para todas ellas. Esto podría causar un interbloqueo.

## Conclusión

En este artículo, hemos visto cómo usar la clase `java.util.concurrent.locks.Condition` de Java para la comunicación de subprocesos. También hemos visto algunos consejos para usar Condición.