---
title: Kotlin의 확장 기능 및 속성 이해
description: 
published: true
date: 2023-02-02T03:36:28.567Z
tags: 
editor: markdown
dateCreated: 2023-02-02T03:36:26.950Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Understanding Kotlin's Extension Functions and Properties***English** document is available*](/en/Knowledge-base/Kotlin/understanding-kotlin-s-extension-functions-and-properties)
{.links-list}


# Kotlin의 확장 기능 및 속성 이해

Kotlin은 더 빠르고 쉽게 개발할 수 있도록 많은 기능을 제공하는 강력한 프로그래밍 언어입니다. 이러한 기능 중 하나는 확장 기능 및 속성입니다.

확장 함수 및 속성을 사용하면 클래스에서 상속하지 않고도 클래스의 기능을 확장할 수 있습니다. 이는 해당 라이브러리에 의존하지 않고 라이브러리의 기능을 사용하려는 경우에 특히 유용합니다.

이 기사에서는 Kotlin의 확장 기능과 속성을 자세히 살펴보겠습니다. 우리는 그것들을 정의하는 방법과 우리 자신의 코드에서 그것들을 사용하는 방법을 배울 것입니다.

## 확장 기능 및 속성 정의

확장 기능과 속성은 각각 `fun` 및 `val` 키워드를 사용하여 정의됩니다. 확장하려는 클래스의 이름 뒤에 점 `.`이 붙습니다.

```kotlin
// Extension function
fun String.repeat(times: Int): String {
    return this.repeat(times)
}

// Extension property
val String.length: Int
    get() = this.length
```

위의 예에서 주어진 횟수만큼 문자열을 반복할 수 있는 확장 함수 `repeat`를 정의했습니다. 또한 문자열의 길이를 얻을 수 있는 확장 속성 `length`를 정의했습니다.

확장 기능과 속성은 확장 중인 클래스에서 실제로 정의되지 않습니다. 이들은 정의된 클래스에서 정적 메서드 및 속성으로 컴파일됩니다. 즉, 클래스 외부에서도 어디에서나 호출할 수 있습니다.

## 확장 기능 및 속성 사용

확장 기능과 속성은 다른 기능이나 속성처럼 사용할 수 있습니다. 아래 예에서는 `repeat` 함수를 사용하여 문자열을 10번 반복합니다.

```kotlin
fun main() {
    val s = "Hello, world!".repeat(10)
    println(s)
}
```

문자열의 길이를 얻기 위해 `length` 속성을 사용할 수도 있습니다:

```kotlin
fun main() {
    val s = "Hello, world!"
    println(s.length)
}
```

## 확장 기능 및 속성 재정의

확장 기능 및 속성을 재정의할 수도 있습니다. 이는 특정 컨텍스트에서 함수 또는 속성의 동작을 변경하려는 경우에 유용할 수 있습니다.

확장 함수 또는 속성을 재정의하려면 다른 함수 또는 속성과 동일한 방식으로 정의하기만 하면 됩니다. 아래 예에서는 주어진 수의 느낌표가 있는 문자열을 반환하도록 `repeat` 함수를 재정의합니다.

```kotlin
fun main() {
    fun String.repeat(times: Int): String {
        return this + "!".repeat(times)
    }

    val s = "Hello, world!".repeat(10)
    println(s)
}
```

## 결론

확장 함수 및 속성은 클래스에서 상속하지 않고도 클래스의 기능을 확장하는 데 사용할 수 있는 Kotlin의 강력한 기능입니다. 각각 `fun` 및 `val` 키워드를 사용하여 정의되며 확장하는 클래스 이름 뒤에 점 `.`이 붙습니다.

확장 기능과 속성은 다른 기능이나 속성처럼 사용할 수 있습니다. 정적 메서드 및 속성으로 컴파일되므로 클래스 외부에서도 어디에서나 호출할 수 있습니다.

확장 기능 및 속성을 재정의할 수도 있습니다. 이는 특정 컨텍스트에서 함수 또는 속성의 동작을 변경하려는 경우에 유용할 수 있습니다.