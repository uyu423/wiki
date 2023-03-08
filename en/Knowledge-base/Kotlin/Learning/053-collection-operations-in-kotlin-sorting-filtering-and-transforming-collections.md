---
title: 053: Collection Operations in Kotlin: Sorting, Filtering, and Transforming Collections
description: 
published: true
date: 2023-02-08T10:55:44.559Z
tags: 
editor: markdown
dateCreated: 2023-02-08T10:55:38.728Z
---

- [053: Operaciones de colección en Kotlin: ordenar, filtrar y transformar colecciones***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/053-collection-operations-in-kotlin-sorting-filtering-and-transforming-collections)
{.links-list}
- [053：Kotlin 中的集合操作：排序、过滤和转换集合***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/053-collection-operations-in-kotlin-sorting-filtering-and-transforming-collections)
{.links-list}
- [053: Kotlin의 컬렉션 작업: 컬렉션 정렬, 필터링 및 변환***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/053-collection-operations-in-kotlin-sorting-filtering-and-transforming-collections)
{.links-list}


# Kotlin Collection Operations

Kotlin's standard library provides a wealth of functions for working with collections. In this article, we'll take a look at some of the most common operations: sorting, filtering, and transforming collections.

## Sorting

Kotlin's standard library provides a number of ways to sort collections. The most common way to sort a collection is to use the `sorted` function. This function takes a `Comparator` as an argument, which is used to determine the order of the elements in the collection.

For example, we can use the `sorted` function to sort a list of strings alphabetically:

```kotlin
val list = listOf("a", "b", "c")

val sortedList = list.sorted()

// sortedList is now equal to listOf("a", "b", "c")
```

We can also use the `sorted` function to sort a list of numbers in ascending or descending order:

```kotlin
val list = listOf(1, 2, 3)

val sortedList = list.sorted()

// sortedList is now equal to listOf(1, 2, 3)

val reversedList = list.sortedDescending()

// reversedList is now equal to listOf(3, 2, 1)
```

If we want to sort a collection in a custom way, we can use the `sortBy` function. This function takes a `selector` function as an argument, which is used to determine the order of the elements in the collection.

For example, we can use the `sortBy` function to sort a list of strings by their length:

```kotlin
val list = listOf("aa", "b", "ccc")

val sortedList = list.sortBy { it.length }

// sortedList is now equal to listOf("b", "aa", "ccc")
```

## Filtering

Kotlin's standard library provides a number of ways to filter collections. The most common way to filter a collection is to use the `filter` function. This function takes a `predicate` function as an argument, which is used to determine which elements should be included in the filtered collection.

For example, we can use the `filter` function to filter a list of strings to only include strings that start with the letter "a":

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val filteredList = list.filter { it.startsWith("a") }

// filteredList is now equal to listOf("a", "ab", "ac")
```

We can also use the `filterNot` function to filter a collection to only include elements that do not match a given predicate. For example, we can use the `filterNot` function to filter a list of strings to only include strings that do not start with the letter "a":

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val filteredList = list.filterNot { it.startsWith("a") }

// filteredList is now equal to listOf("b", "c")
```

If we want to transform a collection while also filtering it, we can use the `map` function. This function takes a `transform` function as an argument, which is used to determine which elements should be included in the transformed collection.

For example, we can use the `map` function to transform a list of strings to a list of their lengths:

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val mappedList = list.map { it.length }

// mappedList is now equal to listOf(1, 1, 1, 2, 2)
```

## Transforming

Kotlin's standard library provides a number of ways to transform collections. The most common way to transform a collection is to use the `map` function. This function takes a `transform` function as an argument, which is used to determine how the elements in the collection should be transformed.

For example, we can use the `map` function to transform a list of strings to a list of their lengths:

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val mappedList = list.map { it.length }

// mappedList is now equal to listOf(1, 1, 1, 2, 2)
```

We can also use the `mapNotNull` function to transform a collection, while also filtering out `null` values. For example, we can use the `mapNotNull` function to transform a list of strings to a list of their lengths, while also filtering out `null` values:

```kotlin
val list = listOf("a", "b", null, "ab", "ac")

val mappedList = list.mapNotNull { it?.length }

// mappedList is now equal to listOf(1, 1, 2, 2)
```

If we want to flatten a collection of collections, we can use the `flatten` function. For example, we can use the `flatten` function to flatten a list of lists of strings:

```kotlin
val list = listOf(listOf("a", "b"), listOf("c", "d"))

val flattenedList = list.flatten()

// flattenedList is now equal to listOf("a", "b", "c", "d")
```

We can also use the `flatMap` function to flatten a collection and transform it at the same time. For example, we can use the `flatMap` function to flatten a list of lists of strings and transform it to a list of their lengths:

```kotlin
val list = listOf(listOf("a", "b"), listOf("c", "d"))

val flattenedList = list.flatMap { it.map { it.length } }

// flattenedList is now equal to listOf(1, 1, 1, 1)
```

## Additional Information

Kotlin's standard library provides many more functions for working with collections. For more information, please see the [Kotlin documentation](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/).