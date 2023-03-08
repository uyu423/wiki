---
title: 015: Kotlin의 Null 허용 유형 및 Null 안전성: Null 값 처리
description: 
published: true
date: 2023-02-16T04:32:56.520Z
tags: 
editor: markdown
dateCreated: 2023-02-16T04:32:54.821Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [015: Nullable Types and Null Safety in Kotlin: Dealing with Null Values***English** document is available*](/en/Knowledge-base/Kotlin/Learning/015-nullable-types-and-null-safety-in-kotlin-dealing-with-null-values)
{.links-list}


## 소개

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어입니다. 간결하고 안전하며 상호 운용이 가능하도록 설계된 범용 언어입니다.

Kotlin의 주요 기능 중 하나는 null 안전입니다. Null 안전은 null 포인터 예외를 방지하기 위한 메커니즘입니다. Kotlin의 유형 시스템은 코드에서 null 참조 가능성을 제거하도록 설계되었습니다.

Nullable 형식은 null일 수 있는 형식을 나타내는 방법입니다. Kotlin에서 모든 유형은 기본적으로 null을 허용하지 않습니다. 즉, null이 아닌 유형의 변수는 null 값을 보유할 수 없습니다.

nullable 형식을 만들려면 형식 이름 뒤에 물음표(?)를 사용합니다. 예를 들어 다음 코드는 null 허용 문자열 변수를 정의합니다.

```kotlin
var str: String? = "Hello"
```

이제 str 변수는 문자열 값이나 null을 보유할 수 있습니다.

null이 아닌 유형의 변수에 null 값을 할당하려고 하면 컴파일 오류가 발생합니다.

```kotlin
var str: String = "Hello"
str = null // error: null can not be a value of a non-null type String
```

이 문제를 해결하기 위해 str 변수의 유형을 nullable 유형으로 변경하거나 null이 아닌 어설션을 사용할 수 있습니다. null이 아닌 어설션은 변수가 null이 아님을 컴파일러에 알리는 연산자입니다. 다음과 같이 사용합니다.

```kotlin
var str: String = "Hello"
str = null // error: null can not be a value of a non-null type String

str!!.length // non-null assertion
```

null이 아닌 어설션 연산자는 이중 느낌표(!!)입니다. 변수가 null이 아니라고 확신하는 경우에만 사용해야 합니다. 그렇지 않으면 런타임 예외가 발생합니다.

## Null 확인

Kotlin에서는 `isNullOrEmpty()` 함수를 사용하여 변수가 null인지 확인할 수 있습니다.

```kotlin
fun main() {
    var str: String? = "Hello"
    if (str.isNullOrEmpty()) {
        println("str is null or empty")
    } else {
        println(str.length)
    }
}
```

`isNullOrEmpty()` 함수는 문자열이 null이거나 비어 있으면 true를 반환합니다. 그렇지 않으면 false를 반환합니다.

`?` 연산자를 사용하여 변수가 null인지 확인할 수도 있습니다.

```kotlin
fun main() {
    var str: String? = "Hello"
    val length = str?.length // str is not null, so length is not null
    println(length)
}
```

`?` 연산자를 안전한 호출 연산자라고 합니다. 길이 속성을 호출하기 전에 변수가 null인지 확인합니다. 변수가 null이면 null을 반환합니다. 그렇지 않으면 문자열의 길이를 반환합니다.

`?` 연산자를 사용하여 nullable 변수에 대한 함수를 호출할 수 있습니다.

```kotlin
fun main() {
    var str: String? = "Hello"
    str?.let {
        println(it.length) // it is not null, so we can call the length property
    }
}
```

`let` 함수는 람다를 인수로 취하는 고차 함수입니다. 람다는 변수가 null이 아닌 경우에만 실행됩니다.

변수가 null이 아닌 경우 `?` 연산자를 사용하여 코드 블록을 실행할 수도 있습니다.

```kotlin
fun main() {
    var str: String? = "Hello"
    str?.let {
        println(it.length) // it is not null, so we can call the length property
    }
}
```

`?` 연산자를 안전한 호출 연산자라고 합니다. 람다를 실행하기 전에 변수가 null인지 확인합니다. 변수가 null이면 아무 작업도 수행하지 않습니다. 그렇지 않으면 람다를 실행합니다.

## 엘비스 오퍼레이터

Elvis 연산자는 nullable 변수에 기본값을 할당하는 방법입니다. 다음과 같이 사용합니다.

```kotlin
fun main() {
    var str: String? = "Hello"
    val length = str?.length ?: 0 // if str is null, length is 0
    println(length)
}
```

`str` 변수가 null이면 `length` 변수에 값 0이 지정됩니다. 그렇지 않으면 `str.length` 값이 지정됩니다.

Elvis 연산자는 종종 `let` 함수와 함께 사용됩니다.

```kotlin
fun main() {
    var str: String? = "Hello"
    str?.let {
        println(it.length) // it is not null, so we can call the length property
    } ?: println("str is null") // if str is null, print "str is null"
}
```

`str` 변수가 null이면 `println("str is null")` 문이 실행됩니다. 그렇지 않으면 `println(it.length)` 문이 실행됩니다.

## Null이 아닌 어설션 연산자

null이 아닌 어설션 연산자는 변수가 null이 아님을 컴파일러에 알리는 방법입니다. 다음과 같이 사용합니다.

```kotlin
fun main() {
    var str: String? = "Hello"
    str!!.length // str is not null, so we can call the length property
}
```

null이 아닌 어설션 연산자는 이중 느낌표(!!)입니다. 변수가 null이 아니라고 확신하는 경우에만 사용해야 합니다. 그렇지 않으면 런타임 예외가 발생합니다.

## !! 운영자

!! 연산자는 변수가 null이 아님을 컴파일러에 알리는 방법입니다. 다음과 같이 사용합니다.

```kotlin
fun main() {
    var str: String? = "Hello"
    str!!.length // str is not null, so we can call the length property
}
```

!! 연산자는 이중 느낌표(!!)입니다. 변수가 null이 아니라고 확신하는 경우에만 사용해야 합니다. 그렇지 않으면 런타임 예외가 발생합니다.

## 결론

이 기사에서는 Kotlin의 null 안전에 대해 배웠습니다. nullable 유형을 사용하는 방법과 null 값을 확인하는 다양한 방법을 살펴보았습니다. 또한 Elvis 연산자와 null이 아닌 어설션 연산자를 사용하는 방법도 살펴보았습니다.