---
title: 049: Kotlin의 고차 함수 및 람다: 클로저 및 함수 유형 이해
description: 
published: true
date: 2023-02-16T15:32:43.297Z
tags: 
editor: markdown
dateCreated: 2023-02-16T15:32:41.058Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [049: Higher-Order Functions and Lambdas in Kotlin: Understanding Closures and Function Types***English** document is available*](/en/Knowledge-base/Kotlin/Learning/049-higher-order-functions-and-lambdas-in-kotlin-understanding-closures-and-function-types)
{.links-list}


# 049: Kotlin의 고차 함수 및 람다: 클로저 및 함수 유형 이해

이 게시물에서는 Kotlin의 고차 함수와 람다를 살펴보겠습니다. 우리는 그것들이 무엇인지, 어떻게 사용하는지 배우고 클로저 및 함수 유형과 같은 몇 가지 개념을 이해할 것입니다.

## 고차 함수와 람다는 무엇인가요?

Kotlin에서 고차 함수는 하나 이상의 함수를 인수로 받거나 함수를 결과로 반환하는 함수입니다. 람다는 이름이 없는 익명 함수의 한 유형입니다.

람다를 인수로 취하는 고차 함수의 간단한 예를 살펴보겠습니다. 이 함수는 Int를 사용하여 부울을 반환하는 람다를 사용하고 람다에 전달될 때 true를 반환하는 모든 Int의 목록을 반환합니다.

```kotlin
fun filter(predicate: (Int) -> Boolean): List<Int> {
    val list = mutableListOf<Int>()
    for (i in 1..10) {
        if (predicate(i)) {
            list.add(i)
        }
    }
    return list
}
```

이 함수를 다음과 같이 호출할 수 있습니다.

```kotlin
val evenNumbers = filter { it % 2 == 0 }
```

람다의 it 키워드는 람다에 전달되는 인수의 자리 표시자입니다. 이 경우 필터 함수에 전달되는 Int를 나타냅니다.

## 클로저란 무엇인가요?

클로저는 주변 환경의 상태를 캡처하는 기능입니다. 즉, 정의된 범위에서 변수에 액세스할 수 있습니다.

다음은 Kotlin 클로저의 간단한 예입니다. 카운터라는 변수와 카운터를 증가시키고 새 값을 반환하는 함수가 있습니다. 이 함수는 카운터 변수의 상태를 캡처하기 때문에 클로저입니다.

```kotlin
var counter = 0
fun incrementCounter(): Int {
    return ++counter
}
```

incrementCounter 함수를 여러 번 호출하면 카운터 변수의 현재 값을 추적하고 매번 새 값을 반환합니다.

```kotlin
incrementCounter() // returns 1
incrementCounter() // returns 2
incrementCounter() // returns 3
```

## 함수 유형이 무엇인가요?

Kotlin에서는 모든 함수에 유형이 있습니다. 함수의 유형은 함수가 취하는 인수의 유형과 함수가 반환하는 값의 유형으로 구성됩니다.

예를 들어, 이전 섹션의 incrementCounter 함수의 유형은 (() -> Int)입니다. 이것은 "인수를 받지 않고 Int를 반환하는 함수"로 읽을 수 있습니다.

첫 번째 섹션의 필터 함수 유형은 ((Int) -> Boolean) -> List<Int>입니다. 이것은 "Int를 취하고 Boolean을 반환하고 Int 목록을 반환하는 함수를 취하는 함수"로 읽을 수 있습니다.

함수 유형은 작업하려는 함수 유형을 지정할 수 있기 때문에 Kotlin에서 중요합니다. 예를 들어, (Int) -> Boolean 유형의 함수를 사용하고 함수에 전달될 때 true를 반환하는 모든 Int의 목록을 반환하는 고차 함수를 작성할 수 있습니다.

```kotlin
fun filter(predicate: (Int) -> Boolean): List<Int> {
    val list = mutableListOf<Int>()
    for (i in 1..10) {
        if (predicate(i)) {
            list.add(i)
        }
    }
    return list
}
```

이 함수를 다음과 같이 호출할 수 있습니다.

```kotlin
val evenNumbers = filter { it % 2 == 0 }
```

람다의 it 키워드는 람다에 전달되는 인수의 자리 표시자입니다. 이 경우 필터 함수에 전달되는 Int를 나타냅니다.

## 결론

이번 포스트에서는 Kotlin의 고차함수와 람다에 대해 알아보았습니다. 우리는 그것들을 사용하는 방법을 보았고 클로저 및 함수 유형과 같은 그 배후에 있는 몇 가지 개념에 대해서도 배웠습니다.