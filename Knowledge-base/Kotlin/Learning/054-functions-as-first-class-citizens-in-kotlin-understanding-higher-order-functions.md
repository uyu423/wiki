---
title: 054: Kotlin의 일급 시민으로서의 기능: 고차 함수 이해
description: 
published: true
date: 2023-02-16T18:33:04.065Z
tags: 
editor: markdown
dateCreated: 2023-02-16T18:32:55.838Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [054: Functions as First-Class Citizens in Kotlin: Understanding Higher-Order Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/054-functions-as-first-class-citizens-in-kotlin-understanding-higher-order-functions)
{.links-list}


## 소개

Kotlin은 Java Virtual Machine에서 실행되는 최신 프로그래밍 언어입니다. 객체 지향 및 함수형 프로그래밍의 최고의 기능을 결합한 정적으로 유형이 지정된 언어입니다.

Kotlin은 JVM의 일급 시민입니다. 즉, 간단한 명령줄 프로그램에서 복잡한 웹 애플리케이션에 이르기까지 모든 종류의 Java 애플리케이션을 개발하는 데 사용할 수 있습니다.

Kotlin의 가장 중요한 기능 중 하나는 고차 함수를 지원한다는 것입니다. 이번 글에서는 고차 함수가 무엇인지, 코틀린에서 어떻게 사용하는지 알아보겠습니다.

## 고차 함수란?

고차 함수는 하나 이상의 함수를 인수로 취하고 함수를 결과로 반환하는 함수입니다.

Kotlin에서 고차 함수는 ```Function<T, R>``` 유형으로 표현됩니다. 이 유형에는 두 가지 유형 매개변수가 있습니다.

- ```T```는 함수에 대한 인수의 유형입니다.
- ```R```은 함수 결과의 유형입니다.

```kotlin
val list = listOf("a", "b", "c")

val upperCaseList = list.map { it.toUpperCase() }

// upperCaseList is now a list of strings: ["A", "B", "C"]
```map``` 함수

```kotlin
val list = listOf(1, 2, 3)

val doubleList = list.map { it * 2 }

// doubleList is now a list of integers: [2, 4, 6]
```map``` 기능을 사용하여 이 작업을 수행할 수 있습니다.

```kotlin
val list = listOf("a", "ab", "abc", "abcd")

val filteredList = list.filter { it.length <= 3 }

// filteredList is now a list of strings: ["a", "ab", "abc"]
```

위의 예에서 문자열 목록이 있고 ```map``` 함수를 사용하여 ```toUpperCase()``` 함수를 목록의 각 요소에 적용합니다.

```kotlin
val list = listOf(1, 2, 3, 4, 5)

val filteredList = list.filter { it % 2 == 0 }

// filteredList is now a list of integers: [2, 4]
```코틀린
값 목록 = listOf(1, 2, 3)

val doubleList = list.map { it * 2 }

// doubleList는 이제 정수 목록입니다: [2, 4, 6]
```kotlin
val list = listOf(1, 2, 3, 4, 5)

val sum = list.reduce { a, b -> a + b }

// sum is now 15
```필터``` 기능

```kotlin
val list = listOf("a", "b", "c")

val concatenatedString = list.reduce { a, b -> a + b }

// concatenatedString is now "abc"
```filter``` 함수는 함수가 ```true```를 반환하는 요소만 포함하는 새 목록을 반환합니다.

예를 들어 문자열 목록이 있고 3자보다 긴 모든 문자열을 필터링하려고 한다고 가정합니다. ```filter``` 기능을 사용하여 이를 수행할 수 있습니다:

```코틀린
값 목록 = listOf("a", "ab", "abc", "abcd")

val FilteredList = list.filter { it.length <= 3 }

// 이제 FilteredList는 문자열 목록입니다: ["a", "ab", "abc"]
```

위의 예에서 문자열 목록이 있고 ```filter``` 기능을 사용하여 3자보다 긴 모든 문자열을 제거합니다.

```filter``` 함수는 문자열 목록뿐만 아니라 모든 유형의 목록과 함께 사용할 수 있습니다. 예를 들어 정수 목록과 함께 ```filter```를 사용할 수 있습니다.

```코틀린
값 목록 = listOf(1, 2, 3, 4, 5)

val FilteredList = list.filter { 그것 % 2 == 0 }

// 이제 FilteredList는 정수 목록입니다: [2, 4]
```

위의 예에서 정수 목록이 있고 ```filter``` 함수를 사용하여 모든 홀수를 제거합니다.

### ```reduce``` 기능

```reduce``` 함수는 함수를 인수로 받아 목록의 각 요소에 적용하는 고차 함수입니다. 함수는 두 개의 인수를 사용하고 단일 값을 반환해야 합니다.

```reduce``` 함수는 목록의 각 요소에 함수를 적용한 결과인 단일 값을 반환합니다.

예를 들어 정수 목록이 있고 목록에 있는 모든 요소의 합을 찾고 싶다고 가정합니다. ```reduce``` 기능을 사용하여 이를 수행할 수 있습니다:

```코틀린
값 목록 = listOf(1, 2, 3, 4, 5)

합계 = list.reduce { a, b -> a + b }

// 합계는 이제 15입니다.
```

위의 예에서 정수 목록이 있고 ```reduce``` 함수를 사용하여 목록에 있는 모든 요소의 합계를 찾습니다.

```reduce``` 함수는 정수 목록뿐만 아니라 모든 유형의 목록과 함께 사용할 수 있습니다. 예를 들어 문자열 목록과 함께 ```reduce```를 사용할 수 있습니다.

```코틀린
값 목록 = listOf("a", "b", "c")

val concatenatedString = list.reduce { a, b -> a + b }

// concatenatedString은 이제 "abc"입니다.
```

위의 예에서는 문자열 목록이 있고 ```reduce``` 함수를 사용하여 모든 문자열을 단일 문자열로 연결합니다.

## 결론

이 기사에서는 고차 함수가 무엇이며 Kotlin에서 어떻게 사용하는지 알아보았습니다. ```map```, ```filter``` 및 ```reduce``` 기능을 사용하여 목록을 변환하고 조작하는 방법을 살펴보았습니다.

고차 함수는 간결하고 읽기 쉬운 코드를 작성하는 데 사용할 수 있는 강력한 도구입니다. Kotlin을 처음 사용하는 경우 고차 함수를 실험하고 무엇을 생각해낼 수 있는지 확인하는 것이 좋습니다.