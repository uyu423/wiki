---
title: 006：Kotlin 中的集合：数组、列表、集合和映射
description: 
published: true
date: 2023-02-16T03:32:49.322Z
tags: 
editor: markdown
dateCreated: 2023-02-16T03:32:47.606Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [006: Collections in Kotlin: Arrays, Lists, Sets, and Maps***English** document is available*](/en/Knowledge-base/Kotlin/Learning/006-collections-in-kotlin-arrays-lists-sets-and-maps)
{.links-list}


# 科特林集合

Kotlin 提供了不同类型的集合来存储数据。主要类型有：
* 数组
* 列表
* 套
*地图

让我们更详细地了解每种类型。

## 数组

数组用于存储固定大小的顺序元素集合。您可以使用 `arrayOf()` 函数在 Kotlin 中创建一个数组：

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
```

`arrayOf()` 函数接受可变数量的参数，因此您还可以使用以下方法创建一个空数组：

```kotlin
val emptyArray = arrayOf<Any>() // creates an empty array of type Any
```

如果您知道要创建的数组的大小，则可以使用 arrayOfNulls() 函数：

```kotlin
val nullArray = arrayOfNulls<String>(5) // creates an array of size 5 with null elements
```

您可以使用从 0 开始的索引访问数组中的元素：

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
numbers[0] // returns 1
numbers[1] // returns 2
numbers[2] // returns 3
numbers[3] // returns 4
numbers[4] // returns 5
```

您还可以使用 `for` 循环遍历数组中的所有元素：

```kotlin
for (number in numbers) {
    println(number)
}
```

## 列表

列表用于存储可变大小的顺序元素集合。您可以使用 `listOf()` 函数在 Kotlin 中创建一个列表：

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
```

`listOf()` 函数接受可变数量的参数，因此您还可以使用以下方法创建一个空列表：

```kotlin
val emptyList = listOf<Any>() // creates an empty list of type Any
```

您可以使用从 0 开始的索引访问列表中的元素：

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
numbers[0] // returns 1
numbers[1] // returns 2
numbers[2] // returns 3
numbers[3] // returns 4
numbers[4] // returns 5
```

您还可以使用 `for` 循环遍历列表中的所有元素：

```kotlin
for (number in numbers) {
    println(number)
}
```

## 套

集合用于存储可变大小的唯一元素集合。您可以使用 `setOf()` 函数在 Kotlin 中创建一个集合：

```kotlin
val numbers = setOf(1, 2, 3, 4, 5)
```

`setOf()` 函数接受可变数量的参数，因此您还可以使用以下方法创建一个空集：

```kotlin
val emptySet = setOf<Any>() // creates an empty set of type Any
```

您可以使用“for”循环遍历集合中的所有元素：

```kotlin
for (number in numbers) {
    println(number)
}
```

## 地图

映射用于存储可变大小的键值对集合。您可以使用 `mapOf()` 函数在 Kotlin 中创建地图：

```kotlin
val numbers = mapOf("one" to 1, "two" to 2, "three" to 3)
```

`mapOf()` 函数接受可变数量的参数，因此您还可以使用以下方法创建一个空地图：

```kotlin
val emptyMap = mapOf<Any, Any>() // creates an empty map of type Any to Any
```

您可以使用键访问地图的值：

```kotlin
numbers["one"] // returns 1
numbers["two"] // returns 2
numbers["three"] // returns 3
```

您还可以使用“for”循环遍历映射中的所有键值对：

```kotlin
for ((key, value) in numbers) {
    println("$key -> $value")
}
```

## 结论

在本文中，我们了解了 Kotlin 中不同类型的集合：数组、列表、集合和映射。我们了解了如何创建每种类型的集合以及如何访问和迭代每个集合中的元素。