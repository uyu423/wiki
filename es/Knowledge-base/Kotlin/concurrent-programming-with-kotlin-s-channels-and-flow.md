---
title: Programación simultánea con canales y flujo de Kotlin
description: 
published: true
date: 2023-02-08T19:55:19.833Z
tags: 
editor: markdown
dateCreated: 2023-02-08T19:55:18.278Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Concurrent Programming with Kotlin's Channels and Flow***English** document is available*](/en/Knowledge-base/Kotlin/concurrent-programming-with-kotlin-s-channels-and-flow)
{.links-list}


# Programación simultánea con canales y flujo de Kotlin

En la programación concurrente, diferentes partes de un programa pueden ejecutarse independientemente unas de otras para hacer un mejor uso de los recursos como el tiempo de CPU y la memoria. Un desafío común con la programación simultánea es coordinar las diferentes partes del programa para evitar conflictos.

Los canales y el flujo de Kotlin brindan una forma útil de administrar la programación simultánea al permitir que diferentes partes del programa se comuniquen entre sí. Los canales son como conductos que pueden transportar datos de una parte del programa a otra, y el flujo es una forma de administrar el flujo de datos a través de esos canales.

Aquí hay un ejemplo simple de cómo se pueden usar los canales y el flujo para coordinar diferentes partes de un programa. Tenemos un programa que necesita imprimir una lista de números, pero queremos hacerlo en dos partes separadas: una parte para imprimir los números mismos y otra parte para imprimir un mensaje después de que se hayan impreso los números.

Podemos usar un canal para enviar los números de la primera parte del programa a la segunda parte, y usar el flujo para asegurarnos de que el mensaje solo se imprima después de que se hayan enviado todos los números.


```kotlin
import kotlinx.coroutines.*
import kotlinx.coroutines.flow.*

fun main() {
    val numbers = (1..5).asFlow() // 1
    val printMessage = numbers.onEach { println(it) } // 2
        .collect { println("Done printing numbers") } // 3
    runBlocking {
        launch { printMessage.collect() } // 4
    }
}
```

1. Creamos un flujo de números usando la función de extensión `asFlow`.
2. Usamos la transformación `onEach` para imprimir cada número a medida que fluye a través del canal.
3. Usamos la transformación `collect` para esperar hasta que se hayan impreso todos los números, luego imprimimos un mensaje.
4. Lanzamos una rutina para ejecutar el flujo.

Este ejemplo muestra cómo se pueden usar los canales y el flujo para coordinar diferentes partes de un programa. Los canales permiten que diferentes partes del programa se comuniquen entre sí, y el flujo proporciona una forma de administrar el flujo de datos a través de esos canales.