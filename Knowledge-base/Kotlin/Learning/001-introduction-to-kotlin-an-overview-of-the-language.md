---
title: 001: Kotlin 소개: 언어 개요
description: 
published: true
date: 2023-01-31T06:04:18.166Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:04:16.531Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [001: Introduction to Kotlin: An Overview of the Language***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/001-introduction-to-kotlin-an-overview-of-the-language)
{.links-list}



# 코틀린

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어이며 JavaScript 소스 코드로 컴파일할 수도 있습니다. Kotlin은 IntelliJ IDEA Java IDE를 만든 회사인 JetBrains에서 개발했습니다.

Kotlin은 유형 유추 기능이 있는 크로스 플랫폼, 정적 유형, 범용 프로그래밍 언어입니다. Kotlin은 Java와 완벽하게 상호 운용되도록 설계되었으며 표준 라이브러리의 JVM 버전은 Java 클래스 라이브러리에 의존하지만 유형 추론을 통해 구문이 더 간결해집니다.

## 특징

Kotlin에는 다음과 같은 기능이 있습니다.

- **Null 안전성**: Kotlin의 유형 시스템은 null 참조가 역참조되는 것을 방지합니다.

- **확장 기능**: Kotlin을 사용하면 클래스에서 상속하지 않고도 새로운 기능으로 클래스를 확장할 수 있습니다.

- **고차 함수 및 람다**: Kotlin은 고차 함수 및 람다를 지원합니다.

- **데이터 클래스**: Kotlin은 데이터만 포함하는 클래스를 만드는 간결한 방법을 제공합니다.

- **컴패니언 객체**: Kotlin을 사용하면 컴패니언 객체에서 클래스의 정적 멤버를 정의할 수 있습니다.

- **객체 지향**: Kotlin은 객체 지향이지만 함수형 프로그래밍도 지원합니다.

- **Kotlin 표준 라이브러리**: Kotlin은 풍부한 함수 및 유형 세트가 포함된 표준 라이브러리와 함께 제공됩니다.

## 구문

Kotlin은 배우기 쉬운 간결한 구문을 가지고 있습니다.

```kotlin
// Define a function that takes two Int arguments and returns an Int.
fun sum(a: Int, b: Int): Int {
   return a + b
}

// Define a data class.
data class User(val name: String, val age: Int)

// Define a companion object.
object MyClass {
   fun doSomething() { ... }
}

// Define a higher-order function.
fun MyClass.myFunction(a: Int, b: Int, f: (Int, Int) -> Int): Int {
   return f(a, b)
}

// Use a lambda expression.
val result = MyClass.myFunction(1, 2) { a, b -> a + b }

// Define an extension function.
fun String.toUpperCase(): String {
   return this.toUpperCase()
}
```

## 시작하기

Kotlin을 시작하려면 IntelliJ IDEA 또는 Eclipse용 Kotlin 플러그인을 다운로드할 수 있습니다.

Kotlin 명령줄 컴파일러를 사용하여 Kotlin 소스 코드를 JavaScript 또는 JVM 바이트코드로 컴파일할 수도 있습니다.

Kotlin에 대해 자세히 알아보려면 다음 리소스를 살펴보세요.

- 코틀린 웹사이트: https://kotlinlang.org

- Kotlin Koans: https://kotlinlang.org/docs/tutorials/koans.html

- Kotlin 표준 라이브러리 문서: https://kotlinlang.org/api/latest/jvm/stdlib/

- Kotlin 참조: https://kotlinlang.org/docs/reference/

## 결론

Kotlin은 JVM에서 실행되고 JavaScript로 컴파일될 수 있는 프로그래밍 언어를 사용하기에 간결하고 안전하며 재미있습니다.