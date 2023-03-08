---
title: Kotlin의 Null 안전 탐색
description: 
published: true
date: 2023-02-17T23:06:42.307Z
tags: 
editor: markdown
dateCreated: 2023-02-17T23:06:40.936Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Exploring Null Safety in Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/exploring-null-safety-in-kotlin)
{.links-list}


# Kotlin에서 Null 안전성 살펴보기

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어이며 JavaScript 소스 코드로 컴파일할 수도 있습니다. Apache 2.0 라이센스에 따른 오픈 소스 프로젝트입니다. Kotlin은 Java에서 크게 영감을 받았으며 Java에 대한 보다 간결하고 안전하며 표현력이 풍부한 대안이 되도록 고안되었습니다.

Kotlin의 가장 주목할만한 기능 중 하나는 NullPointerException 오류(종종 "십억 달러의 실수"라고 함)의 위험을 제거하도록 설계된 null 안전성입니다. Kotlin에서 모든 유형은 기본적으로 null을 허용하지 않습니다. 즉, String 유형의 변수는 null을 보유할 수 없습니다. 그러나 nullable 형식은 다음과 같이 형식에 물음표를 추가하여 선언할 수 있습니다.

```kotlin
var s: String? = null
```

이제 변수 s는 문자열 또는 null을 보유할 수 있습니다. 변수가 null을 보유할 수 있으면 nullable이라고 합니다.

먼저 null인지 확인하지 않고 nullable 변수에 액세스하려고 하면 컴파일러 오류가 발생합니다. 예를 들어 다음 코드는 컴파일되지 않습니다.

```kotlin
var s: String? = null
println(s.length) // error: variable s can be null
```

nullable 변수에 액세스하려면 먼저 null인지 확인해야 합니다. ?를 사용하여 이 작업을 수행할 수 있습니다. 연산자는 다음과 같습니다.

```kotlin
var s: String? = null
println(s?.length) // prints null if s is null, otherwise prints s.length
```

이제 코드가 컴파일되지만 변수 s가 null이면 null을 인쇄합니다. 변수가 null인 경우 다른 작업을 수행하려면 ?:로 작성되는 elvis 연산자를 사용할 수 있습니다. 예를 들어 다음과 같이 변수가 null인 경우 기본 길이를 인쇄할 수 있습니다.

```kotlin
var s: String? = null
println(s?.length ?: 0) // prints 0 if s is null, otherwise prints s.length
```

먼저 null인지 확인하지 않고 nullable 변수에 액세스하려면 !! 변수가 null인 경우 예외를 throw하는 연산자입니다. 예를 들어 다음 코드는 변수 s가 null인 경우 예외를 발생시킵니다.

```kotlin
var s: String? = null
println(s!!.length) // throws an exception if s is null
```

## 널 입력 가능 유형

이전에 본 것처럼 nullable 형식은 형식에 물음표를 추가하여 선언합니다. 예를 들어 다음 변수는 문자열 또는 null을 보유할 수 있습니다.

```kotlin
var s: String? = null
```

또한 숫자, 부울 등과 같은 다른 유형에 대해 nullable 유형을 가질 수 있습니다. 예를 들어 다음 변수는 숫자 또는 null을 보유할 수 있습니다.

```kotlin
var n: Int? = null
```

Nullable 형식은 값이 없음을 나타내려는 경우에 유용합니다. 예를 들어 문자열을 숫자로 변환하는 함수를 생각해 보십시오. 문자열을 숫자로 변환할 수 없는 경우 null을 반환할 수 있습니다.

```kotlin
fun parseInt(s: String): Int? {
    // ...
}
```

이 함수를 다음과 같이 호출할 수 있습니다.

```kotlin
val n = parseInt("42")
```

이제 변수 n은 문자열을 구문 분석할 수 있으면 숫자 42를 보유하고 그렇지 않으면 null을 보유합니다.

컬렉션에 대해 nullable 형식을 가질 수도 있습니다. 예를 들어 다음 변수는 문자열 목록 또는 null을 보유할 수 있습니다.

```kotlin
var list: List<String>? = null
```

Nullable 형식은 값이 없음을 나타내려는 경우에 유용하지만 위험할 수도 있습니다. 예를 들어 다음 코드를 고려하십시오.

```kotlin
fun printLength(s: String?) {
    println(s?.length ?: 0)
}

printLength(null) // prints 0
printLength("abc") // prints 3
```

이 코드는 문제 없이 컴파일되고 실행되지만 null을 전달하면 잘못된 결과가 인쇄됩니다. 0을 인쇄하는 대신 null을 인쇄합니다. elvis 연산자는 왼쪽이 null이고 elvis 연산자의 오른쪽이 0인 경우 오른쪽을 반환하기 때문입니다.

이 문제를 해결하기 위해 변수가 null이 아닌 경우에만 함수 내부의 코드를 실행하는 let 함수를 사용할 수 있습니다.

```kotlin
fun printLength(s: String?) {
    s?.let {
        println(it.length)
    }
}

printLength(null) // prints nothing
printLength("abc") // prints 3
```

이제 코드는 문자열이 null이 아닌 경우에만 문자열의 길이를 인쇄합니다.

## Null을 허용하지 않는 유형

이전에 본 것처럼 모든 유형은 Kotlin에서 기본적으로 null을 허용하지 않습니다. 이것은 String 유형의 변수가 null을 가질 수 없음을 의미합니다. 그러나 다음과 같이 형식에 물음표를 추가하여 null 허용 형식을 계속 가질 수 있습니다.

```kotlin
var s: String? = null
```

이제 변수 s는 문자열 또는 null을 보유할 수 있습니다.

Null을 허용하지 않는 유형은 값의 존재를 나타내려는 경우에 유용합니다. 예를 들어 문자열을 숫자로 변환하는 함수를 생각해 보십시오. 문자열을 숫자로 변환할 수 없는 경우 -1을 반환할 수 있습니다.

```kotlin
fun parseInt(s: String): Int {
    // ...
}
```

이 함수를 다음과 같이 호출할 수 있습니다.

```kotlin
val n = parseInt("42")
```

이제 변수 n은 문자열을 구문 분석할 수 있으면 숫자 42를 유지하고 그렇지 않으면 -1을 유지합니다.

컬렉션에 대해 null을 허용하지 않는 유형을 가질 수도 있습니다. 예를 들어 다음 변수는 문자열 목록 또는 빈 목록을 보유할 수 있습니다.

```kotlin
var list: List<String> = emptyList()
```

Null을 허용하지 않는 유형은 값의 존재를 나타내려는 경우에 유용하지만 위험할 수도 있습니다. 예를 들어 다음 코드를 고려하십시오.

```kotlin
fun printLength(s: String) {
    println(s.length)
}

printLength(null) // error: variable s cannot be null
printLength("abc") // prints 3
```

변수 s가 null을 허용하지 않는 형식으로 선언되었기 때문에 이 코드는 컴파일되지 않습니다. 이 문제를 해결하기 위해 변수가 null이 아닌 경우에만 함수 내부의 코드를 실행하는 let 함수를 사용할 수 있습니다.

```kotlin
fun printLength(s: String) {
    s.let {
        println(it.length)
    }
}

printLength(null) // error: variable s cannot be null
printLength("abc") // prints 3
```

이제 코드는 문자열이 null이 아닌 경우에만 문자열의 길이를 인쇄합니다.

## 결론

Null 안전성은 NullPointerException 오류를 방지하는 데 도움이 되는 Kotlin의 중요한 기능입니다. nullable 형식은 값이 없음을 나타낼 때 유용하고 nullable이 아닌 형식은 값이 있음을 나타낼 때 유용합니다. 그러나 nullable 형식과 nullable이 아닌 형식은 모두 주의하지 않으면 위험할 수 있습니다.