---
title: 014: Kotlin의 확장 기능: 추가 기능으로 클래스 향상
description: 
published: true
date: 2023-01-31T16:57:24.979Z
tags: 
editor: markdown
dateCreated: 2023-01-31T16:57:23.408Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [014: Extensions Functions in Kotlin: Enhancing Classes with Additional Functions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/014-extensions-functions-in-kotlin-enhancing-classes-with-additional-functions)
{.links-list}



# 14: Kotlin의 확장 기능: 추가 기능으로 클래스 향상

Kotlin은 JVM, Android 및 브라우저용 정적 유형 프로그래밍 언어입니다. 상호 운용성, 안전성, 도구 지원 및 간결한 구문으로 유명합니다.

Kotlin의 가장 강력한 기능 중 하나는 확장 기능입니다. 확장 함수는 기존 클래스에서 상속받지 않고 추가되는 함수입니다. 즉, 클래스 자체를 수정하지 않고도 기존 클래스에 새 기능을 추가할 수 있습니다.

이 기사에서는 확장 기능을 만드는 방법과 기존 클래스를 향상시키는 데 사용할 수 있는 방법을 살펴보겠습니다.

## 확장 기능 만들기

확장 기능을 만드는 것은 간단합니다. 함수 이름 앞에 확장하려는 클래스 이름을 붙인 다음 마침표를 찍기만 하면 됩니다. 예를 들어 `string` 클래스에 `print()` 메서드를 추가하는 확장 함수를 만들려면 다음을 수행합니다.

```kotlin
fun String.print() {
    println(this)
}
```

이제 다음과 같이 모든 문자열에서 `print()` 메서드를 호출할 수 있습니다.

```kotlin
"Hello, world!".print() // prints "Hello, world!"
```

보시다시피 확장 함수는 기존 클래스에 새 기능을 추가하는 좋은 방법입니다.

## 확장 기능 사용

확장 함수는 제어할 수 없는 클래스에 새 메서드를 추가하려는 경우에 특히 유용합니다. 예를 들어 `User` 클래스가 있는 라이브러리를 사용하고 있지만 여기에 `getFullName()` 메서드를 추가하려고 한다고 가정해 보겠습니다. 확장 기능을 사용하면 `User` 클래스 자체를 수정하지 않고도 이 작업을 수행할 수 있습니다.

먼저 `User` 클래스를 정의해 보겠습니다.

```kotlin
class User(val firstName: String, val lastName: String)
```

이제 `User` 클래스에 `getFullName()` 메서드를 추가하는 확장 함수를 만들 수 있습니다.

```kotlin
fun User.getFullName(): String {
    return "$firstName $lastName"
}
```

이제 `User` 개체를 만들고 여기에 `getFullName()` 메서드를 호출할 수 있습니다.

```kotlin
val user = User("John", "Smith")
println(user.getFullName()) // prints "John Smith"
```

보시다시피 확장 함수는 클래스 자체를 수정하지 않고도 기존 클래스에 새 메서드를 추가할 수 있는 좋은 방법입니다.

## 결론

이 기사에서는 Kotlin의 확장 기능을 살펴보았습니다. 확장 함수를 만드는 방법과 확장 함수를 사용하여 기존 클래스에 새 메서드를 추가하는 방법을 살펴보았습니다.