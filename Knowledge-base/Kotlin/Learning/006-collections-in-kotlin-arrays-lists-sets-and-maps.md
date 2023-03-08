---
title: 006: Kotlin의 컬렉션: 배열, 목록, 세트 및 맵
description: 
published: true
date: 2023-02-16T03:32:50.102Z
tags: 
editor: markdown
dateCreated: 2023-02-16T03:32:47.610Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [006: Collections in Kotlin: Arrays, Lists, Sets, and Maps***English** document is available*](/en/Knowledge-base/Kotlin/Learning/006-collections-in-kotlin-arrays-lists-sets-and-maps)
{.links-list}


# 코틀린 컬렉션

Kotlin은 데이터를 저장하기 위한 다양한 유형의 컬렉션을 제공합니다. 주요 유형은 다음과 같습니다.
* 배열
* 목록
* 세트
* 지도

각 유형에 대해 자세히 살펴보겠습니다.

## 배열

배열은 요소의 고정 크기 순차 컬렉션을 저장하는 데 사용됩니다. `arrayOf()` 함수를 사용하여 Kotlin에서 배열을 만들 수 있습니다.

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
```

`arrayOf()` 함수는 가변 개수의 인수를 사용하므로 다음을 사용하여 빈 배열을 만들 수도 있습니다.

```kotlin
val emptyArray = arrayOf<Any>() // creates an empty array of type Any
```

만들려는 배열의 크기를 알고 있는 경우 `arrayOfNulls()` 함수를 사용할 수 있습니다.

```kotlin
val nullArray = arrayOfNulls<String>(5) // creates an array of size 5 with null elements
```

0부터 시작하는 인덱스를 사용하여 배열의 요소에 액세스할 수 있습니다.

```kotlin
val numbers = arrayOf(1, 2, 3, 4, 5)
numbers[0] // returns 1
numbers[1] // returns 2
numbers[2] // returns 3
numbers[3] // returns 4
numbers[4] // returns 5
```

또한 `for` 루프를 사용하여 배열의 모든 요소를 반복할 수 있습니다.

```kotlin
for (number in numbers) {
    println(number)
}
```

## 목록

목록은 요소의 가변 크기 순차 컬렉션을 저장하는 데 사용됩니다. `listOf()` 함수를 사용하여 Kotlin에서 목록을 만들 수 있습니다.

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
```

`listOf()` 함수는 가변 개수의 인수를 사용하므로 다음을 사용하여 빈 목록을 만들 수도 있습니다.

```kotlin
val emptyList = listOf<Any>() // creates an empty list of type Any
```

0부터 시작하는 인덱스를 사용하여 목록의 요소에 액세스할 수 있습니다.

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
numbers[0] // returns 1
numbers[1] // returns 2
numbers[2] // returns 3
numbers[3] // returns 4
numbers[4] // returns 5
```

또한 `for` 루프를 사용하여 목록의 모든 요소를 반복할 수 있습니다.

```kotlin
for (number in numbers) {
    println(number)
}
```

## 세트

세트는 고유 요소의 가변 크기 컬렉션을 저장하는 데 사용됩니다. `setOf()` 함수를 사용하여 Kotlin에서 집합을 만들 수 있습니다.

```kotlin
val numbers = setOf(1, 2, 3, 4, 5)
```

`setOf()` 함수는 가변 개수의 인수를 사용하므로 다음을 사용하여 빈 집합을 만들 수도 있습니다.

```kotlin
val emptySet = setOf<Any>() // creates an empty set of type Any
```

`for` 루프를 사용하여 집합의 모든 요소를 반복할 수 있습니다.

```kotlin
for (number in numbers) {
    println(number)
}
```

## 지도

맵은 키-값 쌍의 가변 크기 컬렉션을 저장하는 데 사용됩니다. `mapOf()` 함수를 사용하여 Kotlin에서 지도를 만들 수 있습니다.

```kotlin
val numbers = mapOf("one" to 1, "two" to 2, "three" to 3)
```

`mapOf()` 함수는 가변 개수의 인수를 사용하므로 다음을 사용하여 빈 지도를 만들 수도 있습니다.

```kotlin
val emptyMap = mapOf<Any, Any>() // creates an empty map of type Any to Any
```

다음 키를 사용하여 맵 값에 액세스할 수 있습니다.

```kotlin
numbers["one"] // returns 1
numbers["two"] // returns 2
numbers["three"] // returns 3
```

`for` 루프를 사용하여 맵의 모든 키-값 쌍을 반복할 수도 있습니다.

```kotlin
for ((key, value) in numbers) {
    println("$key -> $value")
}
```

## 결론

이 게시물에서는 배열, 목록, 세트 및 맵과 같은 Kotlin의 다양한 유형의 컬렉션을 살펴보았습니다. 각 유형의 컬렉션을 만드는 방법과 각 컬렉션의 요소에 액세스하고 반복하는 방법을 살펴보았습니다.