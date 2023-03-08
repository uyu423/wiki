---
title: 053: Kotlin의 컬렉션 작업: 컬렉션 정렬, 필터링 및 변환
description: 
published: true
date: 2023-02-08T10:55:40.342Z
tags: 
editor: markdown
dateCreated: 2023-02-08T10:55:38.719Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [053: Collection Operations in Kotlin: Sorting, Filtering, and Transforming Collections***English** document is available*](/en/Knowledge-base/Kotlin/Learning/053-collection-operations-in-kotlin-sorting-filtering-and-transforming-collections)
{.links-list}


# Kotlin 수집 작업

Kotlin의 표준 라이브러리는 컬렉션 작업을 위한 다양한 기능을 제공합니다. 이 문서에서는 컬렉션 정렬, 필터링 및 변환과 같은 가장 일반적인 작업 중 일부를 살펴보겠습니다.

## 정렬

Kotlin의 표준 라이브러리는 컬렉션을 정렬하는 다양한 방법을 제공합니다. 컬렉션을 정렬하는 가장 일반적인 방법은 `sorted` 기능을 사용하는 것입니다. 이 함수는 'Comparator'를 인수로 사용하며 컬렉션의 요소 순서를 결정하는 데 사용됩니다.

예를 들어 `sorted` 함수를 사용하여 문자열 목록을 알파벳순으로 정렬할 수 있습니다.

```kotlin
val list = listOf("a", "b", "c")

val sortedList = list.sorted()

// sortedList is now equal to listOf("a", "b", "c")
```

또한 `sorted` 함수를 사용하여 숫자 목록을 오름차순 또는 내림차순으로 정렬할 수 있습니다.

```kotlin
val list = listOf(1, 2, 3)

val sortedList = list.sorted()

// sortedList is now equal to listOf(1, 2, 3)

val reversedList = list.sortedDescending()

// reversedList is now equal to listOf(3, 2, 1)
```

컬렉션을 맞춤 방식으로 정렬하려면 `sortBy` 기능을 사용할 수 있습니다. 이 함수는 컬렉션의 요소 순서를 결정하는 데 사용되는 `selector` 함수를 인수로 사용합니다.

예를 들어, `sortBy` 함수를 사용하여 문자열 목록을 길이별로 정렬할 수 있습니다.

```kotlin
val list = listOf("aa", "b", "ccc")

val sortedList = list.sortBy { it.length }

// sortedList is now equal to listOf("b", "aa", "ccc")
```

## 필터링

Kotlin의 표준 라이브러리는 컬렉션을 필터링하는 다양한 방법을 제공합니다. 컬렉션을 필터링하는 가장 일반적인 방법은 `filter` 기능을 사용하는 것입니다. 이 함수는 필터링된 컬렉션에 포함되어야 하는 요소를 결정하는 데 사용되는 'predicate' 함수를 인수로 사용합니다.

예를 들어 `filter` 함수를 사용하여 문자 "a"로 시작하는 문자열만 포함하도록 문자열 목록을 필터링할 수 있습니다.

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val filteredList = list.filter { it.startsWith("a") }

// filteredList is now equal to listOf("a", "ab", "ac")
```

또한 `filterNot` 함수를 사용하여 주어진 조건자와 일치하지 않는 요소만 포함하도록 컬렉션을 필터링할 수 있습니다. 예를 들어 'filterNot' 함수를 사용하여 문자 "a"로 시작하지 않는 문자열만 포함하도록 문자열 목록을 필터링할 수 있습니다.

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val filteredList = list.filterNot { it.startsWith("a") }

// filteredList is now equal to listOf("b", "c")
```

컬렉션을 필터링하면서 변환하려면 `map` 기능을 사용할 수 있습니다. 이 함수는 변환된 컬렉션에 포함되어야 하는 요소를 결정하는 데 사용되는 `transform` 함수를 인수로 사용합니다.

예를 들어 `map` 함수를 사용하여 문자열 목록을 길이 목록으로 변환할 수 있습니다.

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val mappedList = list.map { it.length }

// mappedList is now equal to listOf(1, 1, 1, 2, 2)
```

## 변신

Kotlin의 표준 라이브러리는 컬렉션을 변환하는 다양한 방법을 제공합니다. 컬렉션을 변환하는 가장 일반적인 방법은 `map` 함수를 사용하는 것입니다. 이 함수는 컬렉션의 요소를 변환하는 방법을 결정하는 데 사용되는 `transform` 함수를 인수로 사용합니다.

예를 들어 `map` 함수를 사용하여 문자열 목록을 길이 목록으로 변환할 수 있습니다.

```kotlin
val list = listOf("a", "b", "c", "ab", "ac")

val mappedList = list.map { it.length }

// mappedList is now equal to listOf(1, 1, 1, 2, 2)
```

`mapNotNull` 함수를 사용하여 컬렉션을 변환하는 동시에 `null` 값을 필터링할 수도 있습니다. 예를 들어 `mapNotNull` 함수를 사용하여 문자열 목록을 길이 목록으로 변환하는 동시에 `null` 값을 필터링할 수 있습니다.

```kotlin
val list = listOf("a", "b", null, "ab", "ac")

val mappedList = list.mapNotNull { it?.length }

// mappedList is now equal to listOf(1, 1, 2, 2)
```

컬렉션 모음을 평면화하려면 `flatten` 기능을 사용할 수 있습니다. 예를 들어 `flatten` 함수를 사용하여 문자열 목록을 평면화할 수 있습니다.

```kotlin
val list = listOf(listOf("a", "b"), listOf("c", "d"))

val flattenedList = list.flatten()

// flattenedList is now equal to listOf("a", "b", "c", "d")
```

또한 `flatMap` 함수를 사용하여 컬렉션을 평면화하고 동시에 변환할 수 있습니다. 예를 들어 `flatMap` 함수를 사용하여 문자열 목록을 평면화하고 길이 목록으로 변환할 수 있습니다.

```kotlin
val list = listOf(listOf("a", "b"), listOf("c", "d"))

val flattenedList = list.flatMap { it.map { it.length } }

// flattenedList is now equal to listOf(1, 1, 1, 1)
```

## 추가 정보

Kotlin의 표준 라이브러리는 컬렉션 작업을 위한 더 많은 기능을 제공합니다. 자세한 내용은 [Kotlin 설명서](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/)를 참조하세요.