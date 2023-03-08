---
title: 078: El patrón de estrategia en Kotlin: algoritmos encapsulados como objetos
description: 
published: true
date: 2023-02-14T17:55:28.683Z
tags: 
editor: markdown
dateCreated: 2023-02-14T17:55:27.000Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [078: The Strategy Pattern in Kotlin: Encapsulating Algorithms as Objects***English** document is available*](/en/Knowledge-base/Kotlin/Learning/078-the-strategy-pattern-in-kotlin-encapsulating-algorithms-as-objects)
{.links-list}


# 078: El patrón de estrategia en Kotlin: encapsulando algoritmos como objetos

## Introducción

El patrón de estrategia es un patrón de diseño de software de comportamiento que permite seleccionar el comportamiento de un algoritmo en tiempo de ejecución. Esto es útil cuando una aplicación necesita usar diferentes algoritmos, y la elección del algoritmo se puede realizar en tiempo de ejecución de acuerdo con la entrada del usuario o el estado actual de la aplicación.

El patrón de estrategia también se conoce como patrón de política.

## El problema

Supongamos que tenemos una aplicación sencilla que ordena una lista de números enteros. Podríamos comenzar escribiendo una función simple de `clasificación` como esta:

```kotlin
fun sort(list: List<Int>): List<Int> {
    // implement sorting algorithm here
}
```

Esta función `ordenar` toma una lista de enteros como entrada y devuelve una nueva lista de enteros que se ordena en orden ascendente.

Ahora supongamos que queremos agregar otro algoritmo de clasificación a nuestra aplicación. Podríamos escribir otra función `ordenar`, pero entonces tendríamos dos funciones con el mismo nombre pero comportamientos diferentes. Esto sería confuso para los usuarios de nuestra aplicación.

En cambio, podemos usar el patrón de estrategia para encapsular cada algoritmo de clasificación en su propio objeto. Entonces podemos escribir una función `sort` que toma una lista de enteros y un objeto de estrategia como entrada, y usa el objeto de estrategia para ordenar la lista.

## La solución

Así es como podemos usar el patrón de estrategia para ordenar una lista de números enteros:

```kotlin
// define a sorting strategy interface
interface SortingStrategy {
    fun sort(list: List<Int>): List<Int>
}

// implement a sorting strategy for ascending order
class AscendingSortingStrategy : SortingStrategy {
    override fun sort(list: List<Int>): List<Int> {
        // implement sorting algorithm here
    }
}

// implement a sorting strategy for descending order
class DescendingSortingStrategy : SortingStrategy {
    override fun sort(list: List<Int>): List<Int> {
        // implement sorting algorithm here
    }
}

// use the strategy pattern to sort a list of integers
fun sort(list: List<Int>, strategy: SortingStrategy): List<Int> {
    return strategy.sort(list)
}
```

En el código anterior, hemos definido una interfaz `SortingStrategy` que representa una estrategia de clasificación. También hemos implementado dos estrategias de clasificación: `AscendingSortingStrategy` y `DescendingSortingStrategy`.

Finalmente, hemos escrito una función `ordenar` que toma una lista de enteros y una estrategia de clasificación como entrada, y usa la estrategia de clasificación para clasificar la lista.

Ahora podemos usar nuestra función `ordenar` de esta manera:

```kotlin
// sort a list of integers in ascending order
val ascendingList = sort(list, AscendingSortingStrategy())

// sort a list of integers in descending order
val descendingList = sort(list, DescendingSortingStrategy())
```

## Los beneficios

El patrón de estrategia tiene varios beneficios:

- Permite seleccionar el comportamiento de un algoritmo en tiempo de ejecución.

- Facilita agregar nuevos algoritmos a una aplicación.

- Facilita la prueba de algoritmos.

- Hace que el código sea más legible y mantenible.

## Las trampas

Hay algunos peligros potenciales al usar el patrón de estrategia:

- Puede hacer que el código sea más complejo.

- Puede hacer que el código sea más difícil de leer y comprender.

- Puede hacer que sea más difícil cambiar o agregar nuevos algoritmos.