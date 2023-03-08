---
title: 051: Kotlin 표준 라이브러리: 내장 함수 및 클래스 활용
description: 
published: true
date: 2023-02-16T17:33:09.447Z
tags: 
editor: markdown
dateCreated: 2023-02-16T17:33:07.857Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [051: The Kotlin Standard Library: Utilizing the Built-in Functions and Classes***English** document is available*](/en/Knowledge-base/Kotlin/Learning/051-the-kotlin-standard-library-utilizing-the-built-in-functions-and-classes)
{.links-list}


# Kotlin 표준 라이브러리: 내장 함수 및 클래스 활용

Kotlin은 Java Virtual Machine에서 실행되는 강력한 프로그래밍 언어입니다. 객체 지향 및 기능적 프로그래밍 기능을 결합한 정적으로 유형이 지정된 언어입니다. Kotlin은 Java와의 상호 운용성으로 유명하므로 Android 애플리케이션 개발에 탁월한 선택입니다.

Kotlin의 가장 매력적인 기능 중 하나는 Kotlin 코드에서 사용할 수 있는 다양한 함수 및 클래스 집합이 포함된 표준 라이브러리입니다. 이 게시물에서는 Kotlin 표준 라이브러리에서 가장 유용한 함수와 클래스를 살펴보겠습니다.

## 코틀린 컬렉션

Kotlin 컬렉션은 기본적으로 변경할 수 없습니다. 즉, 일단 생성되면 수정할 수 없습니다. 이는 데이터 구조를 수정할 때 발생할 수 있는 버그를 방지하는 데 도움이 되기 때문에 훌륭한 기능입니다. Kotlin은 또한 `filter`, `map` 및 `reduce`와 같이 컬렉션 작업에 유용한 많은 기능을 제공합니다.

숫자 목록이 있고 짝수를 필터링하고 싶다고 가정해 보겠습니다. 우리는 `filter` 함수로 이것을 할 수 있습니다:

```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

val evenNumbers = numbers.filter { it % 2 == 0 }

println(evenNumbers) // prints [2, 4, 6, 8, 10]
```

컬렉션의 요소를 변환하기 위해 `map` 함수를 사용할 수도 있습니다. 예를 들어 문자열 목록이 있고 대문자로 변환하려는 경우 `map` 함수를 사용할 수 있습니다.

```kotlin
val strings = listOf("a", "b", "c", "d", "e")

val uppercaseStrings = strings.map { it.toUpperCase() }

println(uppercaseStrings) // prints [A, B, C, D, E]
```

마지막으로 `reduce` 함수를 사용하여 컬렉션의 요소를 단일 값으로 결합할 수 있습니다. 예를 들어 숫자 목록이 있고 모든 숫자의 합을 계산하려는 경우 `reduce` 함수를 사용할 수 있습니다.

```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

val sum = numbers.reduce { a, b -> a + b }

println(sum) // prints 55
```

다음은 Kotlin 컬렉션 작업에 사용할 수 있는 몇 가지 유용한 기능입니다. 전체 함수 목록은 [Kotlin 표준 라이브러리 문서](https://kotlinlang.org/api/latest/jvm/stdlib/index.html)를 참조하세요.

## 코틀린 문자열

Kotlin은 문자열 작업에 유용한 여러 함수를 제공합니다. 예를 들어 `trim` 함수는 문자열에서 선행 및 후행 공백을 제거하는 데 사용할 수 있습니다.

```kotlin
val s = "  hello world!  "

val trimmedString = s.trim()

println(trimmedString) // prints "hello world!"
```

`split` 함수는 지정된 구분 기호를 사용하여 문자열을 하위 문자열 목록으로 분할하는 데 사용할 수 있습니다.

```kotlin
val s = "a,b,c,d,e"

val substrings = s.split(",")

println(substrings) // prints ["a", "b", "c", "d", "e"]
```

`replace` 함수는 지정된 문자열의 모든 항목을 다른 문자열로 바꾸는 데 사용할 수 있습니다.

```kotlin
val s = "hello world"

val replacedString = s.replace("hello", "goodbye")

println(replacedString) // prints "goodbye world"
```

다음은 Kotlin 문자열 작업에 사용할 수 있는 몇 가지 유용한 함수입니다. 전체 함수 목록은 [Kotlin 표준 라이브러리 문서](https://kotlinlang.org/api/latest/jvm/stdlib/index.html)를 참조하세요.

## 코틀린 수학

Kotlin 표준 라이브러리는 몇 가지 기본 수학 함수도 제공합니다. 예를 들어 'abs' 함수는 숫자의 절대값을 계산하는 데 사용할 수 있습니다.

```kotlin
val x = -10

val absoluteValue = kotlin.math.abs(x)

println(absoluteValue) // prints 10
```

`max` 및 `min` 함수는 각각 두 숫자의 최대값과 최소값을 계산하는 데 사용할 수 있습니다.

```kotlin
val x = 10
val y = 20

val maximum = kotlin.math.max(x, y)
val minimum = kotlin.math.min(x, y)

println(maximum) // prints 20
println(minimum) // prints 10
```

마지막으로 `pow` 함수를 사용하여 지정된 거듭제곱으로 거듭제곱한 숫자를 계산할 수 있습니다.

```kotlin
val x = 2.0
val y = 10

val xToTheY = kotlin.math.pow(x, y)

println(xToTheY) // prints 1024.0
```

다음은 Kotlin 수학 작업에 사용할 수 있는 몇 가지 유용한 함수입니다. 전체 함수 목록은 [Kotlin 표준 라이브러리 문서](https://kotlinlang.org/api/latest/jvm/stdlib/index.html)를 참조하세요.

## Kotlin 날짜 및 시간

Kotlin은 날짜 및 시간 작업을 위한 포괄적인 함수 및 클래스 세트를 제공합니다. 예를 들어 `now` 함수를 사용하여 현재 날짜와 시간을 얻을 수 있습니다.

```kotlin
val now = LocalDateTime.now()

println(now) // prints 2020-03-27T12:34:56.789
```

`parse` 함수는 문자열을 `LocalDate` 개체로 구문 분석하는 데 사용할 수 있습니다.

```kotlin
val dateString = "2020-03-27"

val date = LocalDate.parse(dateString)

println(date) // prints 2020-03-27
```

`plusDays` 함수는 지정된 일수를 `LocalDate` 개체에 추가하는 데 사용할 수 있습니다.

```kotlin
val date = LocalDate.now()

val tomorrow = date.plusDays(1)

println(tomorrow) // prints 2020-03-28
```

다음은 Kotlin 날짜 및 시간 작업에 사용할 수 있는 몇 가지 유용한 함수입니다. 전체 함수 목록은 [Kotlin 표준 라이브러리 문서](https://kotlinlang.org/api/latest/jvm/stdlib/index.html)를 참조하세요.

## 결론

이 게시물에서는 Kotlin 표준 라이브러리에서 가장 유용한 함수와 클래스 중 일부를 살펴보았습니다. Kotlin 컬렉션을 필터링, 매핑 및 축소하는 방법을 살펴보았습니다. Kotlin 문자열을 트리밍, 분할 및 대체하는 방법 Kotlin 수학 함수를 사용하여 숫자의 절대값, 최대값, 최소값, 거듭제곱을 계산하는 방법을 알아보세요. 또한 Kotlin 날짜 및 시간을 구문 분석하고 형식을 지정하고 조작하는 방법도 살펴보았습니다.

Kotlin 표준 라이브러리에 대한 자세한 내용은 [Kotlin 표준 라이브러리 문서](https://kotlinlang.org/api/latest/jvm/stdlib/index.html)를 확인하세요.