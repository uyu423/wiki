---
title: Kotlin y la arquitectura basada en eventos: creación de sistemas receptivos y reactivos
description: 
published: true
date: 2023-02-05T03:55:37.134Z
tags: 
editor: markdown
dateCreated: 2023-02-05T03:55:31.754Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin and Event-driven Architecture: Building Responsive and Reactive Systems***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-event-driven-architecture-building-responsive-and-reactive-systems)
{.links-list}



# Kotlin y la arquitectura basada en eventos: creación de sistemas receptivos y reactivos

En los últimos años, ha habido un cambio en la forma en que construimos sistemas de software. La arquitectura basada en eventos (EDA) es un estilo de arquitectura de software que se está volviendo más popular debido a sus muchos beneficios. Kotlin es un gran lenguaje para construir sistemas EDA, debido a sus características que permiten la concurrencia y su fuerte soporte para la programación funcional. En este artículo, exploraremos cómo se puede usar Kotlin para crear sistemas receptivos y reactivos.

## ¿Qué es la arquitectura basada en eventos?

La arquitectura dirigida por eventos es un estilo de arquitectura de software que se basa en la comunicación de eventos. En un sistema EDA, hay tres tipos de componentes:

- Productores de eventos: Estos componentes generan eventos.
- Consumidores de eventos: estos componentes reciben eventos y realizan alguna acción en respuesta.
- Canales de eventos: estos componentes transportan eventos desde los productores hasta los consumidores.

![Arquitectura basada en eventos](https://kotlinlang.org/docs/reference/coroutines-overview.html# event-driven-architecture)

EDA tiene muchos beneficios sobre otras arquitecturas, como ser más escalable, más resistente y más receptivo. En un sistema EDA, cada componente es independiente y se puede agregar, quitar o modificar sin afectar a los demás componentes. Esto hace que el sistema sea más escalable, ya que se pueden agregar nuevos componentes según sea necesario.

Los sistemas EDA también son más resistentes, ya que cada componente puede fallar sin afectar a los demás componentes. Esto se debe a que cada componente es independiente y no existen dependencias entre los componentes.

Finalmente, los sistemas EDA son más receptivos, ya que cada componente puede reaccionar a los eventos a medida que ocurren. Esto se debe al hecho de que cada componente es asíncrono y puede manejar eventos en paralelo.

## Kotlin y la arquitectura basada en eventos

Kotlin es un gran lenguaje para construir sistemas EDA, debido a sus características que permiten la concurrencia y su fuerte soporte para la programación funcional.

Kotlin tiene un gran soporte para la concurrencia, con funciones como rutinas y canales. Las corrutinas son subprocesos ligeros que se pueden usar para ejecutar código en paralelo. Los canales son construcciones de comunicación que se pueden usar para enviar y recibir datos entre rutinas.

Kotlin también tiene un fuerte soporte para la programación funcional, con funciones como lambdas y funciones de orden superior. Estas características facilitan la escritura de código declarativo y conciso.

## Construyendo un sistema receptivo

En esta sección, construiremos un sistema simple que responda a los eventos. Comenzaremos definiendo una clase de evento.


```kotlin
class Event(val data: String)
```

A continuación, definiremos un productor que genera eventos.


```kotlin
class Producer {
    suspend fun produce(): Event {
        // ...
    }
}
```

Luego, definiremos un consumidor que recibe eventos y los imprime en la consola.


```kotlin
class Consumer {
    suspend fun consume(event: Event) {
        // ...
    }
}
```

Finalmente, definiremos un canal que transporte eventos desde el productor hasta el consumidor.


```kotlin
class Channel {
    suspend fun send(event: Event) {
        // ...
    }

    suspend fun receive(): Event {
        // ...
    }
}
```

Ahora que tenemos nuestros componentes definidos, podemos escribir el código para unirlos. Primero, crearemos un productor y un consumidor.


```kotlin
val producer = Producer()
val consumer = Consumer()
```

A continuación, crearemos un canal.


```kotlin
val channel = Channel()
```

Luego, lanzaremos una rutina que produce eventos y los envía al canal.


```kotlin
GlobalScope.launch {
    while (true) {
        val event = producer.produce()
        channel.send(event)
    }
}
```

Finalmente, lanzaremos una rutina que recibe eventos del canal y los consume.


```kotlin
GlobalScope.launch {
    while (true) {
        val event = channel.receive()
        consumer.consume(event)
    }
}
```

## Construyendo un sistema reactivo

En esta sección, construiremos un sistema simple que sea reactivo a los eventos. Comenzaremos definiendo una clase de evento.


```kotlin
class Event(val data: String)
```

A continuación, definiremos un productor que genera eventos.


```kotlin
class Producer {
    suspend fun produce(): Event {
        // ...
    }
}
```

Luego, definiremos un consumidor que recibe eventos y los imprime en la consola.


```kotlin
class Consumer {
    suspend fun consume(event: Event) {
        // ...
    }
}
```

Finalmente, definiremos un canal que transporte eventos desde el productor hasta el consumidor.


```kotlin
class Channel {
    suspend fun send(event: Event) {
        // ...
    }

    suspend fun receive(): Event {
        // ...
    }
}
```

Ahora que tenemos nuestros componentes definidos, podemos escribir el código para unirlos. Primero, crearemos un productor y un consumidor.


```kotlin
val producer = Producer()
val consumer = Consumer()
```

A continuación, crearemos un canal.


```kotlin
val channel = Channel()
```

Luego, lanzaremos una rutina que produce eventos y los envía al canal.


```kotlin
GlobalScope.launch {
    while (true) {
        val event = producer.produce()
        channel.send(event)
    }
}
```

Finalmente, lanzaremos una rutina que recibe eventos del canal y los consume.


```kotlin
GlobalScope.launch {
    while (true) {
        val event = channel.receive()
        consumer.consume(event)
    }
}
```

## Conclusión

En este artículo, exploramos cómo se puede usar Kotlin para crear sistemas receptivos y reactivos. Hemos visto cómo las características de Kotlin permiten la concurrencia y su sólido soporte para la programación funcional lo convierte en una excelente opción para crear sistemas EDA.