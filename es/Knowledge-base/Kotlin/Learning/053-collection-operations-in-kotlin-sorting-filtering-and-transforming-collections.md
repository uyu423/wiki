---
title: 053: Operaciones de colección en Kotlin: ordenar, filtrar y transformar colecciones
description: 
published: true
date: 2023-02-08T10:55:40.371Z
tags: 
editor: markdown
dateCreated: 2023-02-08T10:55:38.727Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [053: Collection Operations in Kotlin: Sorting, Filtering, and Transforming Collections***English** document is available*](/en/Knowledge-base/Kotlin/Learning/053-collection-operations-in-kotlin-sorting-filtering-and-transforming-collections)
{.links-list}


# Operaciones de colección de Kotlin

La biblioteca estándar de Kotlin proporciona una gran cantidad de funciones para trabajar con colecciones. En este artículo, veremos algunas de las operaciones más comunes: ordenar, filtrar y transformar colecciones.

## Clasificación

La biblioteca estándar de Kotlin proporciona varias formas de ordenar las colecciones. La forma más común de ordenar una colección es usar la función `ordenada`. Esta función toma un 'Comparador' como argumento, que se usa para determinar el orden de los elementos en la colección.

Por ejemplo, podemos usar la función `sorted` para ordenar alfabéticamente una lista de cadenas:

```kotlin
val list = listOf("a", "b", "c")

val sortedList = list.sorted()

// sortedList is now equal to listOf("a", "b", "c")
```

También podemos usar la función `sorted` para ordenar una lista de números en orden ascendente o descendente:

```kotlin
val list = listOf(1, 2, 3)

val sortedList = list.sorted()

// sortedList is now equal to listOf(1, 2, 3)

val reversedList = list.sortedDescending()

// reversedList is now equal to listOf(3, 2, 1)
```

Si queremos ordenar una colección de forma personalizada, podemos usar la función `sortBy`. Esta función toma una función `selector` como argumento, que se usa para determinar el orden de los elementos en la colección.

Por ejemplo, podemos usar la función `sortBy` para ordenar una lista de cadenas por su longitud:

```kotlin
val list = listOf("aa", "b", "ccc")

val sortedList = list.sortBy { it.length }

// sortedList is now equal to listOf("b", "aa", "ccc")
```

## Filtrado

La biblioteca estándar de Kotlin proporciona varias formas de filtrar colecciones. La forma más común de filtrar una colección es usar la función `filter`. Esta función toma una función `predicado` como argumento, que se utiliza para determinar qué elementos deben incluirse en la colección filtrada.

Por ejemplo, podemos usar la función `filter` para filtrar una lista de cadenas para incluir solo cadenas que comiencen con la letra "a":

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val filteredList = list.filter { it.startsWith("a") }

// filteredList is now equal to listOf("a", "ab", "ac")
```

También podemos usar la función `filterNot` para filtrar una colección para incluir solo elementos que no coincidan con un predicado dado. Por ejemplo, podemos usar la función `filterNot` para filtrar una lista de cadenas para incluir solo cadenas que no comienzan con la letra "a":

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val filteredList = list.filterNot { it.startsWith("a") }

// filteredList is now equal to listOf("b", "c")
```

Si queremos transformar una colección mientras la filtramos, podemos usar la función `map`. Esta función toma una función `transform` como argumento, que se utiliza para determinar qué elementos deben incluirse en la colección transformada.

Por ejemplo, podemos usar la función `map` para transformar una lista de cadenas en una lista de sus longitudes:

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val mappedList = list.map { it.length }

// mappedList is now equal to listOf(1, 1, 1, 2, 2)
```

## Transformando

La biblioteca estándar de Kotlin proporciona varias formas de transformar colecciones. La forma más común de transformar una colección es usar la función `mapa`. Esta función toma una función `transform` como argumento, que se utiliza para determinar cómo se deben transformar los elementos de la colección.

Por ejemplo, podemos usar la función `map` para transformar una lista de cadenas en una lista de sus longitudes:

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val mappedList = list.map { it.length }

// mappedList is now equal to listOf(1, 1, 1, 2, 2)
```

También podemos usar la función `mapNotNull` para transformar una colección, al mismo tiempo que filtramos los valores `null`. Por ejemplo, podemos usar la función `mapNotNull` para transformar una lista de cadenas en una lista de sus longitudes, al mismo tiempo que filtramos los valores `null`:

```kotlin
val list = listOf("a", "b", null, "ab", "ac")

val mappedList = list.mapNotNull { it?.length }

// mappedList is now equal to listOf(1, 1, 2, 2)
```

Si queremos aplanar una colección de colecciones, podemos usar la función `aplanar`. Por ejemplo, podemos usar la función `flatten` para aplanar una lista de listas de cadenas:

```kotlin
val list = listOf(listOf("a", "b"), listOf("c", "d"))

val flattenedList = list.flatten()

// flattenedList is now equal to listOf("a", "b", "c", "d")
```

También podemos usar la función `flatMap` para aplanar una colección y transformarla al mismo tiempo. Por ejemplo, podemos usar la función `flatMap` para aplanar una lista de cadenas y transformarla en una lista de sus longitudes:

```kotlin
val list = listOf(listOf("a", "b"), listOf("c", "d"))

val flattenedList = list.flatMap { it.map { it.length } }

// flattenedList is now equal to listOf(1, 1, 1, 1)
```

## Información adicional

La biblioteca estándar de Kotlin proporciona muchas más funciones para trabajar con colecciones. Para obtener más información, consulte la [documentación de Kotlin] (https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/).