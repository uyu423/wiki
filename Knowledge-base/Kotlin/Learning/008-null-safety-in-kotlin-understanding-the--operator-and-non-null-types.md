---
title: 008: Kotlin의 Null 안전: ? 연산자 및 Null이 아닌 유형
description: 
published: true
date: 2023-01-31T05:24:38.820Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:24:37.172Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [008: Null Safety in Kotlin: Understanding the ? Operator and Non-Null Types***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/008-null-safety-in-kotlin-understanding-the--operator-and-non-null-types)
{.links-list}




# Kotlin의 Null 안전: ? 이해하기 연산자 및 Null이 아닌 유형

Kotlin은 JVM에서 실행되는 정적 유형 프로그래밍 언어입니다. Java와 완벽하게 상호 운용 가능하며 종종 Android 개발을 위한 Java의 대안으로 사용됩니다. Null 안전은 Kotlin의 주요 기능 중 하나입니다. Java 프로그램에서 오류의 주요 원인이 될 수 있는 널 포인터 예외의 위험을 제거합니다.

Kotlin에서 모든 변수는 null을 허용하거나 null이 아닌 것으로 선언해야 합니다. 널 입력 가능 변수는 널 값을 보유할 수 있지만 널이 아닌 변수는 보유할 수 없습니다. 이는 컴파일 타임에 적용되므로 null이 아닌 변수에 null 값을 할당할 수 없습니다.

Kotlin의 null 안전성을 이해하는 핵심은 ? 운영자. 이 연산자는 변수를 nullable로 표시하는 데 사용됩니다. 예를 들어 다음 변수는 null 또는 null이 아닌 값을 보유할 수 있습니다.

```kotlin
var str: String? = "Hello, world!"
```

nullable 변수의 유형은 ?를 추가하여 표시됩니다. 유형 이름 뒤에. 위의 예에서 변수의 유형은 String?입니다.

먼저 null인지 확인하지 않고 nullable 변수에 액세스하려고 하면 컴파일 시간 오류가 발생합니다. 예를 들어 다음 코드는 컴파일되지 않습니다.

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str.length)
}
```

컴파일러는 str이 null일 수 있다는 것을 알고 있으므로 그것에 대해 length 속성을 호출하는 것을 허용하지 않습니다. 이 문제를 해결하려면 액세스하기 전에 str이 null인지 확인해야 합니다.

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    if (str != null) {
        println(str.length)
    }
}
```

또는 ? nullable 변수에 안전하게 액세스하는 연산자입니다. 변수에 액세스하기 전에 변수가 null인지 확인합니다. null이면 전체 표현식이 null로 평가됩니다. 예를 들어:

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str?.length)
}
```

위의 코드에서 str?.length 표현식은 str이 null인 경우 null로 평가됩니다. 그렇지 않으면 문자열의 길이로 평가됩니다.

?를 사용하는 것도 가능합니다. 변수가 null인 경우 사용할 기본값을 지정하는 연산자입니다. 예를 들어:

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str?.length ?: 0)
}
```

위의 코드에서 str이 null이면 표현식은 0으로 평가됩니다. 그렇지 않으면 문자열의 길이로 평가됩니다.

nullable 형식에서 null이 아닌 형식을 만드는 것이 유용한 경우가 많습니다. 이것은 !!를 사용하여 수행할 수 있습니다. 운영자. 이 연산자는 nullable 형식을 null이 아닌 형식으로 변환합니다. 그러나 nullable 유형이 실제로 null이면 예외가 발생합니다. 예를 들어:

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str!!.length)
}
```

위의 코드에서 str이 null이면 예외가 발생합니다. 그렇지 않으면 문자열의 길이가 인쇄됩니다.

?를 사용하는 것도 가능합니다. 연산자 !! 운영자. 먼저 nullable 변수가 null인지 확인합니다. null이면 null을 반환합니다. 그렇지 않으면 nullable 변수를 null이 아닌 유형으로 변환하고 반환합니다. 예를 들어:

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str?.length ?: 0)
}
```

위의 코드에서 str이 null이면 표현식은 null로 평가됩니다. 그렇지 않으면 문자열의 길이로 평가됩니다.

Null 안전은 null 포인터 예외를 방지하는 데 도움이 되는 Kotlin의 중요한 기능입니다. ?를 조심스럽게 사용함으로써 연산자를 사용하면 코드를 보다 강력하게 만들고 이러한 유형의 오류를 피할 수 있습니다.