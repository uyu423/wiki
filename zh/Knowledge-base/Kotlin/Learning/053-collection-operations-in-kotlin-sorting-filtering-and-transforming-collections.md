---
title: 053：Kotlin 中的集合操作：排序、过滤和转换集合
description: 
published: true
date: 2023-02-08T10:55:40.355Z
tags: 
editor: markdown
dateCreated: 2023-02-08T10:55:38.719Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [053: Collection Operations in Kotlin: Sorting, Filtering, and Transforming Collections***English** document is available*](/en/Knowledge-base/Kotlin/Learning/053-collection-operations-in-kotlin-sorting-filtering-and-transforming-collections)
{.links-list}


# Kotlin 集合操作

Kotlin 的标准库提供了丰富的函数来处理集合。在本文中，我们将了解一些最常见的操作：排序、过滤和转换集合。

## 排序

Kotlin 的标准库提供了多种对集合进行排序的方法。对集合进行排序的最常见方法是使用 `sorted` 函数。该函数以一个“Comparator”作为参数，用于确定集合中元素的顺序。

例如，我们可以使用 sorted 函数按字母顺序对字符串列表进行排序：

```kotlin
val list = listOf("a", "b", "c")

val sortedList = list.sorted()

// sortedList is now equal to listOf("a", "b", "c")
```

我们还可以使用 `sorted` 函数按升序或降序对数字列表进行排序：

```kotlin
val list = listOf(1, 2, 3)

val sortedList = list.sorted()

// sortedList is now equal to listOf(1, 2, 3)

val reversedList = list.sortedDescending()

// reversedList is now equal to listOf(3, 2, 1)
```

如果我们想以自定义方式对集合进行排序，我们可以使用 sortBy 函数。该函数以一个“选择器”函数作为参数，用于确定集合中元素的顺序。

例如，我们可以使用 sortBy 函数按长度对字符串列表进行排序：

```kotlin
val list = listOf("aa", "b", "ccc")

val sortedList = list.sortBy { it.length }

// sortedList is now equal to listOf("b", "aa", "ccc")
```

## 过滤

Kotlin 的标准库提供了多种过滤集合的方法。过滤集合的最常见方法是使用“filter”函数。此函数以一个“谓词”函数作为参数，用于确定哪些元素应包含在过滤后的集合中。

例如，我们可以使用 `filter` 函数过滤一个字符串列表，只包含以字母“a”开头的字符串：

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val filteredList = list.filter { it.startsWith("a") }

// filteredList is now equal to listOf("a", "ab", "ac")
```

我们还可以使用 `filterNot` 函数来过滤集合以仅包含与给定谓词不匹配的元素。例如，我们可以使用 `filterNot` 函数过滤字符串列表，只包含不以字母“a”开头的字符串：

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val filteredList = list.filterNot { it.startsWith("a") }

// filteredList is now equal to listOf("b", "c")
```

如果我们想在转换集合的同时过滤它，我们可以使用 `map` 函数。此函数将“转换”函数作为参数，用于确定哪些元素应包含在转换后的集合中。

例如，我们可以使用 `map` 函数将字符串列表转换为它们的长度列表：

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val mappedList = list.map { it.length }

// mappedList is now equal to listOf(1, 1, 1, 2, 2)
```

## 转型

Kotlin 的标准库提供了多种转换集合的方法。转换集合的最常见方法是使用 `map` 函数。此函数将“转换”函数作为参数，用于确定应如何转换集合中的元素。

例如，我们可以使用 `map` 函数将字符串列表转换为它们的长度列表：

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val mappedList = list.map { it.length }

// mappedList is now equal to listOf(1, 1, 1, 2, 2)
```

我们还可以使用 `mapNotNull` 函数来转换集合，同时也过滤掉 `null` 值。例如，我们可以使用 `mapNotNull` 函数将字符串列表转换为它们的长度列表，同时也过滤掉 `null` 值：

```kotlin
val list = listOf("a", "b", null, "ab", "ac")

val mappedList = list.mapNotNull { it?.length }

// mappedList is now equal to listOf(1, 1, 2, 2)
```

如果我们想展平一个集合的集合，我们可以使用 `flatten` 函数。例如，我们可以使用 `flatten` 函数来展平字符串列表的列表：

```kotlin
val list = listOf(listOf("a", "b"), listOf("c", "d"))

val flattenedList = list.flatten()

// flattenedList is now equal to listOf("a", "b", "c", "d")
```

我们还可以使用 `flatMap` 函数来展平一个集合并同时对其进行转换。例如，我们可以使用 flatMap 函数来展平字符串列表并将其转换为长度列表：

```kotlin
val list = listOf(listOf("a", "b"), listOf("c", "d"))

val flattenedList = list.flatMap { it.map { it.length } }

// flattenedList is now equal to listOf(1, 1, 1, 1)
```

## 附加信息

Kotlin 的标准库提供了更多处理集合的函数。有关详细信息，请参阅 [Kotlin 文档](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/)。