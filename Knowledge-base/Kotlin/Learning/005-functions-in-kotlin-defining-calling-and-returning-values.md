---
title: 005: Kotlin의 함수: 값 정의, 호출 및 반환
description: 
published: true
date: 2023-02-16T02:32:23.662Z
tags: 
editor: markdown
dateCreated: 2023-02-16T02:32:22.067Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [005: Functions in Kotlin: Defining, Calling, and Returning Values***English** document is available*](/en/Knowledge-base/Kotlin/Learning/005-functions-in-kotlin-defining-calling-and-returning-values)
{.links-list}


# Kotlin의 함수: 값 정의, 호출 및 반환

기능은 특정 작업을 수행하는 코드 집합입니다. Kotlin에서는 나중에 해당 작업을 수행해야 할 때마다 호출할 자체 함수를 정의할 수 있습니다. 이 게시물에서는 함수를 정의하고 호출하고 값을 반환하는 방법을 배웁니다.

## 함수 정의

Kotlin에서는 ```fun``` 키워드를 사용하여 함수를 정의합니다. 예를 들어 인사말을 출력하는 함수를 정의하고 싶다고 합시다. 다음과 같이 할 수 있습니다.

```kotlin
fun printGreeting() {
    println("Hello, world!")
}
```

인수를 받는 함수를 정의할 수도 있습니다. 예를 들어 이름이 있는 인사말 메시지를 인쇄하는 함수를 정의하고 싶다고 가정해 보겠습니다. 다음과 같이 할 수 있습니다.

```kotlin
fun printGreeting(name: String) {
    println("Hello, $name!")
}
```

값을 반환하는 함수를 정의할 수도 있습니다. 예를 들어 두 숫자의 합을 계산하는 함수를 정의하고 싶다고 가정해 보겠습니다. 다음과 같이 할 수 있습니다.

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

## 함수 호출

함수 이름 뒤에 괄호 ```()```를 사용하여 함수를 호출합니다. 예를 들어 앞에서 정의한 ```printGreeting()``` 함수를 다음과 같이 호출할 수 있습니다.

```kotlin
printGreeting() // prints "Hello, world!"
```

인수를 받는 함수를 정의한 경우 괄호 ```()``` 안에 인수를 전달해야 합니다. 예를 들어 앞에서 정의한 ```printGreeting(name: String)``` 함수를 다음과 같이 호출할 수 있습니다.

```kotlin
printGreeting("John") // prints "Hello, John!"
```

값을 반환하는 함수를 정의한 경우 반환 값을 변수에 저장해야 합니다. 예를 들어 앞에서 정의한 ```sum(a: Int, b: Int): Int``` 함수를 다음과 같이 호출할 수 있습니다.

```kotlin
val result = sum(1, 2) // result is 3
```

## 반환 값

이전 섹션에서 본 것처럼 값을 반환하는 함수를 정의할 수 있습니다. Kotlin에서는 ```return``` 키워드를 사용하여 함수에서 값을 반환합니다. 예를 들어 두 숫자의 합을 계산하고 결과를 반환하는 함수를 정의하고 싶다고 가정해 보겠습니다. 다음과 같이 할 수 있습니다.

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

```kotlin
fun sum(a: Int, b: Int): Int = a + b
```코틀린
재미있는 합(a: Int, b: Int): Int = a + b
```

후자의 예에서는 간단히 함수 이름 ```sum```에 할당하여 ```a + b``` 값을 반환합니다.

이번 포스팅은 여기까지! 요약하면 함수를 정의하고 호출하고 값을 반환하는 방법을 배웠습니다.