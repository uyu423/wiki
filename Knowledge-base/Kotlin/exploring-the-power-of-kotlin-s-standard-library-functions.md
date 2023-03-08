---
title: Kotlin의 표준 라이브러리 함수의 성능 살펴보기
description: 
published: true
date: 2023-02-18T00:06:25.352Z
tags: 
editor: markdown
dateCreated: 2023-02-18T00:06:23.964Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Exploring the Power of Kotlin's Standard Library Functions***English** document is available*](/en/Knowledge-base/Kotlin/exploring-the-power-of-kotlin-s-standard-library-functions)
{.links-list}


# Kotlin의 표준 라이브러리 함수의 성능 살펴보기

Kotlin은 다양한 애플리케이션에 사용할 수 있는 다목적 언어입니다. 인기의 이유 중 하나는 표준 라이브러리에서 사용할 수 있는 기능이 풍부하기 때문입니다. 이 기사에서는 Kotlin의 표준 라이브러리에서 가장 유용한 몇 가지 기능과 이를 사용하여 코드를 간소화하는 방법을 살펴보겠습니다.

## 필터

'filter' 함수는 Kotlin에서 가장 일반적으로 사용되는 함수 중 하나입니다. 특정 기준과 일치하지 않는 목록에서 요소를 제거할 수 있습니다. 예를 들어 숫자 목록이 있고 모든 짝수를 제거하려고 한다고 가정해 보겠습니다. '필터' 기능을 사용하여 이 작업을 수행할 수 있습니다.

```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

val evenNumbers = numbers.filter { it % 2 == 0 }

println(evenNumbers) // prints [2, 4, 6, 8, 10]
```

보시다시피 `filter` 함수는 람다를 인수로 받습니다. 이 람다는 목록에 유지해야 하는 요소를 결정하는 데 사용됩니다. 위의 예에서는 2로 균등하게 나누어지는 모든 요소를 유지합니다.

## 지도

`map` 함수는 Kotlin에서 매우 유용한 또 다른 함수입니다. 목록의 요소를 새 값으로 변환할 수 있습니다. 예를 들어 문자열 목록이 있고 이를 정수 목록으로 변환하려고 한다고 가정해 보겠습니다. 여기서 각 정수는 해당 문자열의 길이입니다. `map` 기능을 사용하여 이 작업을 수행할 수 있습니다.

```kotlin
val strings = listOf("a", "ab", "abc", "abcd", "abcde")

val lengths = strings.map { it.length }

println(lengths) // prints [1, 2, 3, 4, 5]
```

`filter` 함수와 마찬가지로 `map` 함수는 람다를 인수로 사용합니다. 이 람다는 각 요소를 변환하는 방법을 결정하는 데 사용됩니다. 위의 예에서 각 문자열을 길이로 변환합니다.

## 플랫맵

`flatMap` 기능은 `map` 기능과 유사하지만 목록 목록을 단일 목록으로 변환하는 데 사용할 수 있습니다. 예를 들어 문자열 목록이 있고 이를 단일 문자열 목록으로 변환하려고 한다고 가정해 보겠습니다. `flatMap` 함수를 사용하여 이 작업을 수행할 수 있습니다.

```kotlin
val listOfStrings = listOf(listOf("a", "b", "c"), listOf("d", "e", "f"))

val flattened = listOfStrings.flatMap { it }

println(flattened) // prints [a, b, c, d, e, f]
```

보시다시피 `flatMap` 함수는 람다를 인수로 사용합니다. 이 람다는 각 요소를 변환하는 방법을 결정하는 데 사용됩니다. 위의 예에서 각 문자열 목록을 단일 문자열 목록으로 변환합니다.

## 정렬됨

'sorted' 함수는 목록을 정렬하는 데 사용됩니다. 예를 들어 문자열 목록이 있고 알파벳순으로 정렬하려고 한다고 가정해 보겠습니다. `sorted` 함수를 사용하여 이 작업을 수행할 수 있습니다.

```kotlin
val strings = listOf("c", "b", "a")

val sorted = strings.sorted()

println(sorted) // prints [a, b, c]
```

'sorted' 함수는 요소를 정렬해야 하는 순서를 정의하는 람다와 목록을 오름차순 또는 내림차순으로 정렬할지 여부를 결정하는 부울의 두 가지 인수를 사용합니다. 위의 예에서는 문자열을 알파벳순으로 오름차순으로 정렬합니다.

## 줄이다

'reduce' 함수는 목록을 단일 값으로 줄이는 데 사용됩니다. 예를 들어 정수 목록이 있고 그 합계를 계산하려고 한다고 가정해 보겠습니다. `reduce` 함수를 사용하여 이 작업을 수행할 수 있습니다.

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)

val sum = numbers.reduce { a, b -> a + b }

println(sum) // prints 15
```

`reduce` 함수는 요소를 결합하는 방법을 정의하는 람다와 초기 값의 두 가지 인수를 사용합니다. 위의 예에서는 요소를 함께 추가하여 결합합니다.

## 결론

이는 Kotlin의 표준 라이브러리에서 사용할 수 있는 많은 유용한 기능 중 일부에 불과합니다. 이러한 기능을 사용하여 코드를 간소화하고 더 간결하게 만들 수 있습니다.