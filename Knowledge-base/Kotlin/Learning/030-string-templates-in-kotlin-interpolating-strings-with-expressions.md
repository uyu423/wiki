---
title: 030: Kotlin의 문자열 템플릿: 표현식으로 문자열 보간
description: 
published: true
date: 2023-02-01T05:04:48.115Z
tags: 
editor: markdown
dateCreated: 2023-02-01T05:04:46.508Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [030: String Templates in Kotlin: Interpolating Strings with Expressions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/030-string-templates-in-kotlin-interpolating-strings-with-expressions)
{.links-list}




# Kotlin의 문자열 템플릿: 표현식으로 문자열 보간

Kotlin의 문자열 템플릿은 문자열 내에서 식을 보간하는 간단하고 편리한 방법을 제공합니다. 이는 사용자 이름이나 현재 날짜와 같은 문자열에 동적 콘텐츠를 삽입해야 할 때 유용할 수 있습니다.

문자열 템플릿은 달러 기호 `$`로 시작하고 그 뒤에 중괄호 `{}`로 묶인 표현식이 옵니다. 표현식은 유효한 Kotlin 코드가 될 수 있으며 평가되고 그 결과가 문자열에 삽입됩니다.

예를 들어 다음 문자열 템플릿은 다음과 같습니다.

```kotlin
val name = "John"
println("Hello, $name!")
```

'Hello, John!'을 출력합니다.

문자열 템플릿을 사용하여 함수 호출 결과를 삽입할 수도 있습니다.

```kotlin
fun getCurrentDate(): String {
    // ...
}

println("Today is $getCurrentDate().")
```

표현식이 복잡한 표현식인 경우 `$` 문자를 사용하여 멤버에 액세스할 수 있습니다.

```kotlin
data class User(val name: String, val age: Int)

val user = User("John", 30)
println("User $user.name is $user.age years old.")
```

그러면 '사용자 John은 30세입니다.'가 인쇄됩니다.

문자열 템플릿을 사용하여 함수 호출 결과를 삽입할 수도 있습니다.

```kotlin
fun getCurrentDate(): String {
    // ...
}

println("Today is $getCurrentDate().")
```

표현식이 복잡한 표현식인 경우 `$` 문자를 사용하여 멤버에 액세스할 수 있습니다.

```kotlin
data class User(val name: String, val age: Int)

val user = User("John", 30)
println("User $user.name is $user.age years old.")
```

그러면 '사용자 John은 30세입니다.'가 인쇄됩니다.

`${}` 구문을 사용하여 복잡한 표현식을 보간할 수도 있습니다.

```kotlin
data class User(val name: String, val age: Int)

val user = User("John", 30)
println("User ${user.name} is ${user.age} years old.")
```

이는 이전 예제와 동일합니다.

## 중괄호 이스케이프

문자열 템플릿에 리터럴 `$` 또는 `{` 문자를 삽입해야 하는 경우 백슬래시 `\`로 이스케이프할 수 있습니다.

```kotlin
println("\${5 + 5}") // prints ${5 + 5}
println("\$5 + 5") // prints $5 + 5
```

백슬래시 문자를 삽입해야 하는 경우 다른 백슬래시로 이스케이프할 수 있습니다.

```kotlin
println("\\") // prints \
```

## 공백 자르기

기본적으로 문자열 템플릿은 보간된 식에서 선행 또는 후행 공백을 유지합니다. 이 공백을 제거하려면 `trimIndent()` 또는 `trimMargin()` 메서드를 사용할 수 있습니다.

```kotlin
val text = """
    |Lorem ipsum dolor sit amet,
    |consectetur adipiscing elit.
    |""".trimMargin()

println(text) // prints Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

`trimIndent()` 메서드는 모든 선행 공백을 제거하는 반면 `trimMargin()` 메서드는 각 줄의 첫 번째 비공백 문자까지 모든 선행 공백을 제거합니다. 위의 예에서 이 문자는 `|`입니다.

## 안전한 통화

문자열 템플릿에서 nullable 표현식을 보간하면 Kotlin은 자동으로 안전한 호출 `?.`을 삽입하여 NullPointerException을 방지합니다.

```kotlin
fun getUserName(): String? {
    // ...
}

println("User name is ${getUserName()}.")
```

`getUserName()` 함수가 `null`을 반환하면 `User name is null.`이 인쇄됩니다.

## Null이 아닌 어설션

식이 `null`이 아니라고 확신하는 경우 null이 아닌 어설션 연산자 `!!`를 사용하여 안전한 호출을 비활성화할 수 있습니다.

```kotlin
fun getUserName(): String? {
    // ...
}

println("User name is ${getUserName()!!}.")
```

`getUserName()` 함수가 `null`을 반환하면 `User name is null.`이 인쇄됩니다.

## 결론

Kotlin의 문자열 템플릿은 문자열 내에서 식을 보간하는 간단하고 편리한 방법을 제공합니다. 이는 사용자 이름이나 현재 날짜와 같은 문자열에 동적 콘텐츠를 삽입해야 할 때 유용할 수 있습니다.