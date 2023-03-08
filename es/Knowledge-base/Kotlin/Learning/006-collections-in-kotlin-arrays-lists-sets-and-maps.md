---
title: 006: Colecciones en Kotlin: arreglos, listas, conjuntos y mapas
description: 
published: true
date: 2023-02-16T03:32:49.414Z
tags: 
editor: markdown
dateCreated: 2023-02-16T03:32:47.614Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [006: Collections in Kotlin: Arrays, Lists, Sets, and Maps***English** document is available*](/en/Knowledge-base/Kotlin/Learning/006-collections-in-kotlin-arrays-lists-sets-and-maps)
{.links-list}


# Colecciones Kotlin

Kotlin proporciona diferentes tipos de colecciones para almacenar datos. Los principales tipos son:
* Matrices
* Listas
* Conjuntos
* Mapas

Echemos un vistazo a cada tipo con más detalle.

## matrices

Las matrices se utilizan para almacenar una colección secuencial de elementos de tamaño fijo. Puedes crear una matriz en Kotlin usando la función `arrayOf()`:

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
```

La función `arrayOf()` toma una cantidad variable de argumentos, por lo que también puede crear una matriz vacía usando:

```kotlin
val emptyArray = arrayOf<Any>() // creates an empty array of type Any
```

Si conoce el tamaño de la matriz que desea crear, puede usar la función `arrayOfNulls()`:

```kotlin
val nullArray = arrayOfNulls<String>(5) // creates an array of size 5 with null elements
```

Puede acceder a los elementos de una matriz utilizando su índice, que comienza en 0:

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
numbers[0] // returns 1
numbers[1] // returns 2
numbers[2] // returns 3
numbers[3] // returns 4
numbers[4] // returns 5
```

También puede usar el ciclo `for` para iterar sobre todos los elementos en una matriz:

```kotlin
for (number in numbers) {
    println(number)
}
```

## Listas

Las listas se utilizan para almacenar una colección secuencial de elementos de tamaño variable. Puedes crear una lista en Kotlin usando la función `listOf()`:

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
```

La función `listOf()` toma un número variable de argumentos, por lo que también puedes crear una lista vacía usando:

```kotlin
val emptyList = listOf<Any>() // creates an empty list of type Any
```

Puede acceder a los elementos de una lista utilizando su índice, que comienza en 0:

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
numbers[0] // returns 1
numbers[1] // returns 2
numbers[2] // returns 3
numbers[3] // returns 4
numbers[4] // returns 5
```

También puedes usar el bucle `for` para iterar sobre todos los elementos de una lista:

```kotlin
for (number in numbers) {
    println(number)
}
```

## Conjuntos

Los conjuntos se utilizan para almacenar una colección de tamaño variable de elementos únicos. Puedes crear un conjunto en Kotlin usando la función `setOf()`:

```kotlin
val numbers = setOf(1, 2, 3, 4, 5)
```

La función `setOf()` toma un número variable de argumentos, por lo que también puede crear un conjunto vacío usando:

```kotlin
val emptySet = setOf<Any>() // creates an empty set of type Any
```

Puede iterar sobre todos los elementos de un conjunto utilizando el bucle `for`:

```kotlin
for (number in numbers) {
    println(number)
}
```

## Mapas

Los mapas se utilizan para almacenar una colección de tamaño variable de pares clave-valor. Puedes crear un mapa en Kotlin usando la función `mapOf()`:

```kotlin
val numbers = mapOf("one" to 1, "two" to 2, "three" to 3)
```

La función `mapOf()` toma un número variable de argumentos, por lo que también puedes crear un mapa vacío usando:

```kotlin
val emptyMap = mapOf<Any, Any>() // creates an empty map of type Any to Any
```

Puede acceder al valor de un mapa usando la tecla:

```kotlin
numbers["one"] // returns 1
numbers["two"] // returns 2
numbers["three"] // returns 3
```

También puede iterar sobre todos los pares clave-valor en un mapa usando el ciclo `for`:

```kotlin
for ((key, value) in numbers) {
    println("$key -> $value")
}
```

## Conclusión

En esta publicación, analizamos los diferentes tipos de colecciones en Kotlin: arreglos, listas, conjuntos y mapas. Vimos cómo crear cada tipo de colección y cómo acceder e iterar sobre los elementos de cada colección.