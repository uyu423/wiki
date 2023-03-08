---
title: 048: Kotlin의 Elvis 연산자: 간결한 방식으로 Null 값 처리
description: 
published: true
date: 2023-02-02T09:57:28.064Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:57:26.488Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [048: The Elvis Operator in Kotlin: Dealing with Null Values in a Compact Way***English** document is available*](/en/Knowledge-base/Kotlin/Learning/048-the-elvis-operator-in-kotlin-dealing-with-null-values-in-a-compact-way)
{.links-list}


# Kotlin의 Elvis 연산자: 간결한 방식으로 Null 값 처리

Null 값은 모든 프로그래밍 언어에서 처리하기 어려울 수 있습니다. Kotlin에서 Elvis 연산자는 null 값을 처리하는 간결하고 안전한 방법을 제공합니다.

## 엘비스 오퍼레이터란?

Elvis 연산자는 피연산자의 null이 아닌 값 또는 피연산자가 null인 경우 기본값을 반환하는 null-safe 연산자입니다. Elvis 연산자는 다음과 같이 작성됩니다.

```kotlin
val result = operand ?: defaultValue
```

피연산자가 null이 아닌 경우 Elvis 연산자는 피연산자를 반환합니다. 피연산자가 null이면 Elvis 연산자는 기본값을 반환합니다.

## 엘비스 오퍼레이터는 어떻게 작동하나요?

Elvis 연산자는 null-safe 연산자(`?.`)와 Elvis 연산자(`?:`)의 두 부분으로 구성됩니다.

null-safe 연산자(`?.`)는 nullable 개체의 멤버에 안전하게 액세스하는 데 사용됩니다. 개체가 null이면 null-safe 연산자는 NullPointerException을 throw하는 대신 null을 반환합니다.

Elvis 연산자(`?:`)는 피연산자가 null인 경우 기본값을 제공하는 데 사용됩니다.

## 엘비스 연산자를 사용하는 경우

Elvis 연산자는 간결하고 안전한 방식으로 null 값을 처리하는 데 가장 일반적으로 사용됩니다.

예를 들어 다음 코드를 고려하십시오.

```kotlin
val list: List<String>? = null

val firstItem = list?.get(0) ?: "Default Value"
```

이 코드에서 `list` 변수는 null을 허용합니다. `list`가 null이면 `firstItem` 변수가 기본값("기본값")으로 설정됩니다. `list`가 null이 아닌 경우 `firstItem` 변수는 목록의 첫 번째 항목으로 설정됩니다.

## 추가 정보

다음은 Elvis 연산자에 대해 자세히 알아볼 수 있는 추가 리소스입니다.

- [Kotlin 문서 - Elvis 연산자](https://kotlinlang.org/docs/reference/null-safety.html# the-elvis-operator)
- [Kotlin 아카데미 - Null 안전 및 Elvis 연산자](https://kotlinacademy.com/kotlin-null-safety-elvis-operator/)
- [Android 개발자 - Kotlin에서 null 처리](https://developer.android.com/kotlin/null-safety)