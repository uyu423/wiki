---
title: Kotlin의 고차 함수 활용
description: 
published: true
date: 2023-01-31T04:36:24.277Z
tags: 
editor: markdown
dateCreated: 2023-01-31T04:36:20.907Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Utilizing Kotlin's Higher-Order Functions***English** version of this document is available*](/en/Knowledge-base/Kotlin/utilizing-kotlin-s-higher-order-functions)
{.links-list}


# Kotlin의 고차 함수 활용

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어이며 JavaScript 소스 코드로 컴파일할 수도 있습니다. Kotlin은 JetBrains에서 개발했습니다.

다른 언어에 비해 Kotlin의 주요 이점 중 하나는 고차 함수를 사용한다는 것입니다. Kotlin에서 고차 함수는 다른 함수를 인수로 받거나 함수를 결과로 반환하는 함수입니다.

고차 함수는 다음과 같은 많은 이점을 제공합니다.

- 코드의 가독성과 유지보수성 향상
- 상용구 코드 감소
- 더 간결한 코드

이 기사에서는 Kotlin에서 고차 함수를 사용할 수 있는 몇 가지 방법을 살펴보겠습니다.

## 함수를 인수로 전달

고차 함수의 가장 일반적인 사용 사례 중 하나는 함수를 다른 함수에 인수로 전달하는 것입니다.

다음 코드 스니펫을 고려하십시오.

```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

    numbers.forEach {
        println(it)
    }
}
```

이 코드에는 `forEach` 고차 함수를 사용하여 반복하는 숫자 목록이 있습니다. `forEach` 함수는 함수를 인수로 사용합니다. 이 경우 목록의 각 요소를 인쇄하는 익명 함수입니다.

함수를 별도로 정의하고 `forEach`에 전달할 수도 있습니다.

```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

    val printFunction = { element: Int ->
        println(element)
    }

    numbers.forEach(printFunction)
}
```

여기서는 `printFunction`을 별도로 정의하여 `forEach`에 전달했습니다.

## 다른 함수에서 함수 반환

고차 함수의 또 다른 일반적인 사용 사례는 다른 함수에서 함수를 반환하는 것입니다.

다음 코드 스니펫을 고려하십시오.

```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

    val printFunction = printer()

    numbers.forEach(printFunction)
}

fun printer(): (Int) -> Unit {
    return { println(it) }
}
```

이 코드에서는 `Int`를 받아서 인쇄하는 함수를 반환하는 `printer` 함수를 정의했습니다. 그런 다음 이 함수를 `forEach`에 전달하여 목록의 각 요소를 출력했습니다.

## 결론

이 기사에서는 Kotlin에서 고차 함수를 사용할 수 있는 몇 가지 방법을 살펴보았습니다. 고차 함수는 코드의 가독성 및 유지 관리 용이성 증가, 상용구 코드 감소, 더 간결한 코드 등 여러 가지 이점을 제공합니다.