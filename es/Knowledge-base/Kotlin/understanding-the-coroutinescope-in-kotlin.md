---
title: Entendiendo CoroutineScope en Kotlin
description: 
published: true
date: 2023-02-14T07:55:19.709Z
tags: 
editor: markdown
dateCreated: 2023-02-14T07:55:17.878Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Understanding the CoroutineScope in Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/understanding-the-coroutinescope-in-kotlin)
{.links-list}


# Entendiendo el CoroutineScope en Kotlin

Las rutinas son una herramienta poderosa para la programación concurrente en Kotlin. Son subprocesos livianos que se pueden usar para mejorar el rendimiento de su aplicación Kotlin.

En este artículo, echaremos un vistazo a CoroutineScope y cómo se puede usar para administrar corrutinas en su aplicación.

## ¿Qué es CoroutineScope?

CoroutineScope es una clase en la biblioteca de corrutinas de Kotlin que se usa para administrar el ciclo de vida de las corrutinas. Proporciona una forma de cancelar todas las corrutinas iniciadas en su alcance cuando se cancela el alcance.

Los ámbitos se pueden crear mediante la función del constructor coroutineScope. Esta función de creación crea un nuevo ámbito y lo agrega al ámbito actual.

Veamos un ejemplo sencillo:

```kotlin
fun main() {
    // create a new scope
    val scope = coroutineScope {
        // launch a coroutine in the scope
        launch {
            delay(1000L)
            println("World!")
        }
        println("Hello")
    }
}
```

En el ejemplo anterior, usamos la función del constructor coroutineScope para crear un nuevo alcance. Luego lanzamos una corrutina en el osciloscopio. La rutina se retrasará un segundo y luego imprimirá "¡Mundo!".

Observe que la corrutina se inicia en el alcance. Esto significa que la rutina se cancelará cuando se cancele el alcance.

## Cancelando CoroutineScope

 CoroutineScope se puede cancelar mediante el método de cancelación. Este método cancelará todas las rutinas iniciadas en el alcance. Veamos un ejemplo sencillo:

```kotlin
fun main() {
    // create a new scope
    val scope = coroutineScope {
        // launch a coroutine in the scope
        launch {
            delay(1000L)
            println("World!")
        }
        println("Hello")
    }
    // cancel the scope
    scope.cancel()
}
```

En el ejemplo anterior, creamos un nuevo alcance y lanzamos una rutina en el alcance. La rutina se retrasará un segundo y luego imprimirá "¡Mundo!".

Luego llamamos al método de cancelación en el alcance. Esto cancelará todas las corrutinas iniciadas en el alcance. En este caso, la rutina no imprimirá "¡Mundo!" porque fue cancelado antes de que tuviera la oportunidad de ejecutarse.

## Conclusión

En este artículo, analizamos CoroutineScope y cómo se puede usar para administrar corrutinas en su aplicación. También hemos visto cómo cancelar un alcance y cómo esto cancelará todas las corrutinas iniciadas en el alcance.