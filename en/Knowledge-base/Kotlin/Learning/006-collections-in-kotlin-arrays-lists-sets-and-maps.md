---
title: 006: Collections in Kotlin: Arrays, Lists, Sets, and Maps
description: 
published: true
date: 2023-02-16T03:32:55.571Z
tags: 
editor: markdown
dateCreated: 2023-02-16T03:32:47.615Z
---

- [006: Colecciones en Kotlin: arreglos, listas, conjuntos y mapas***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/006-collections-in-kotlin-arrays-lists-sets-and-maps)
{.links-list}
- [006：Kotlin 中的集合：数组、列表、集合和映射***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/006-collections-in-kotlin-arrays-lists-sets-and-maps)
{.links-list}
- [006: Kotlin의 컬렉션: 배열, 목록, 세트 및 맵***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/006-collections-in-kotlin-arrays-lists-sets-and-maps)
{.links-list}


# Kotlin Collections 

Kotlin provides different types of collections to store data. The main types are: 
* Arrays 
* Lists 
* Sets 
* Maps 

Let's take a look at each type in more detail. 

## Arrays 

Arrays are used to store a fixed-size sequential collection of elements. You can create an array in Kotlin using the `arrayOf()` function: 

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
```

The `arrayOf()` function takes a variable number of arguments, so you can also create an empty array using: 

```kotlin
val emptyArray = arrayOf<Any>() // creates an empty array of type Any
```

If you know the size of the array you want to create, you can use the `arrayOfNulls()` function: 

```kotlin
val nullArray = arrayOfNulls<String>(5) // creates an array of size 5 with null elements
```

You can access elements in an array using their index, which starts at 0: 

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
numbers[0] // returns 1
numbers[1] // returns 2
numbers[2] // returns 3
numbers[3] // returns 4
numbers[4] // returns 5
```

You can also use the `for` loop to iterate over all the elements in an array: 

```kotlin
for (number in numbers) {
    println(number)
}
```

## Lists 

Lists are used to store a variable-size sequential collection of elements. You can create a list in Kotlin using the `listOf()` function: 

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
```

The `listOf()` function takes a variable number of arguments, so you can also create an empty list using: 

```kotlin
val emptyList = listOf<Any>() // creates an empty list of type Any
```

You can access elements in a list using their index, which starts at 0: 

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
numbers[0] // returns 1
numbers[1] // returns 2
numbers[2] // returns 3
numbers[3] // returns 4
numbers[4] // returns 5
```

You can also use the `for` loop to iterate over all the elements in a list: 

```kotlin
for (number in numbers) {
    println(number)
}
```

## Sets 

Sets are used to store a variable-size collection of unique elements. You can create a set in Kotlin using the `setOf()` function: 

```kotlin
val numbers = setOf(1, 2, 3, 4, 5)
```

The `setOf()` function takes a variable number of arguments, so you can also create an empty set using: 

```kotlin
val emptySet = setOf<Any>() // creates an empty set of type Any
```

You can iterate over all the elements in a set using the `for` loop: 

```kotlin
for (number in numbers) {
    println(number)
}
```

## Maps 

Maps are used to store a variable-size collection of key-value pairs. You can create a map in Kotlin using the `mapOf()` function: 

```kotlin
val numbers = mapOf("one" to 1, "two" to 2, "three" to 3)
```

The `mapOf()` function takes a variable number of arguments, so you can also create an empty map using: 

```kotlin
val emptyMap = mapOf<Any, Any>() // creates an empty map of type Any to Any
```

You can access the value of a map using the key: 

```kotlin
numbers["one"] // returns 1
numbers["two"] // returns 2
numbers["three"] // returns 3
```

You can also iterate over all the key-value pairs in a map using the `for` loop: 

```kotlin
for ((key, value) in numbers) {
    println("$key -> $value")
}
```

## Conclusion 

In this post, we looked at the different types of collections in Kotlin: arrays, lists, sets, and maps. We saw how to create each type of collection and how to access and iterate over the elements in each collection.