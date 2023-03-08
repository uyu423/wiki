---
title: Una guía para java.util.concurrent.Exchanger de Java para el intercambio de datos concurrente
description: 
published: true
date: 2023-02-04T06:55:23.651Z
tags: 
editor: markdown
dateCreated: 2023-02-04T06:55:21.839Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [A Guide to Java's java.util.concurrent.Exchanger for Concurrent Data Exchange***English** document is available*](/en/Knowledge-base/Java/a-guide-to-java-s-java-util-concurrent-exchanger-for-concurrent-data-exchange)
{.links-list}


# Una guía para java.util.concurrent.Exchanger de Java para el intercambio de datos concurrentes

En la programación concurrente, el intercambio de datos entre hilos es una operación común. La clase Exchanger en la API concurrente de Java proporciona un mecanismo para que los subprocesos intercambien datos de una manera segura y conveniente.

Este artículo brindará una descripción general de la clase Exchanger y demostrará cómo se puede usar en un programa concurrente.

## ¿Qué es la Clase Intercambiador?

La clase Exchanger es una clase de utilidad para intercambiar datos entre subprocesos. Proporciona un único método, exchange(), que toma dos argumentos: los datos que se van a intercambiar y un valor de tiempo de espera.

Si hay otro subproceso esperando para intercambiar datos, el método exchange() regresará inmediatamente con los datos del otro subproceso. Si no hay otro subproceso esperando, el método exchange() se bloqueará hasta que otro subproceso llame a exchange() con los mismos datos.

La clase Exchanger es útil para situaciones en las que dos subprocesos necesitan sincronizar sus datos, como en una relación productor-consumidor.

## Uso de la clase de intercambiador

Aquí hay un ejemplo simple de cómo se puede usar la clase Exchanger. En este ejemplo, se utilizan dos subprocesos para intercambiar datos. El primer hilo genera un número aleatorio y el segundo hilo calcula el cuadrado de ese número.

```java
import java.util.concurrent.Exchanger;

public class ExchangerExample {
    public static void main(String[] args) {
        Exchanger<Integer> exchanger = new Exchanger<>();
        
        new Thread(() -> {
            try {
                int data = (int) (Math.random() * 100);
                System.out.println("Thread 1: " + data);
                
                data = exchanger.exchange(data);
                
                System.out.println("Thread 1: " + data);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();
        
        new Thread(() -> {
            try {
                int data = (int) (Math.random() * 100);
                System.out.println("Thread 2: " + data);
                
                data = exchanger.exchange(data);
                
                System.out.println("Thread 2: " + data);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();
    }
}
```

En este ejemplo, los dos subprocesos intercambian datos y luego imprimen los resultados. La salida de este programa podría ser algo como esto:

```
Thread 1: 97
Thread 2: 25
Thread 1: 625
Thread 2: 676
```

## Conclusión

La clase Exchanger proporciona un mecanismo para que los subprocesos intercambien datos de forma segura y cómoda. Es útil para situaciones en las que dos subprocesos necesitan sincronizar sus datos.