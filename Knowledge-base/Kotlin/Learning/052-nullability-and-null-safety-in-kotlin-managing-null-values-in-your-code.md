---
title: 052: Kotlin의 Null 허용 및 Null 안전성: 코드에서 Null 값 관리
description: 
published: true
date: 2023-02-14T03:17:31.322Z
tags: 
editor: markdown
dateCreated: 2023-02-14T03:17:29.679Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [052: Nullability and Null Safety in Kotlin: Managing Null Values in Your Code***English** document is available*](/en/Knowledge-base/Kotlin/Learning/052-nullability-and-null-safety-in-kotlin-managing-null-values-in-your-code)
{.links-list}


## 소개

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어입니다. Java와 상호 운용이 가능하고 Android 앱을 개발하는 데 사용할 수 있는 JVM 언어입니다.

Kotlin의 주요 기능 중 하나는 null 안전입니다. Null 안전은 NullPointerException을 피하는 기능입니다. Kotlin은 null 허용 및 null이 아닌 유형을 사용하여 null 안전성을 달성합니다.

Nullable 유형은 null 값을 보유할 수 있지만 null이 아닌 유형은 보유할 수 없습니다. 즉, null이 아닌 유형에 null 값을 할당하려고 하면 컴파일 타임 오류가 발생합니다.

## Null 허용 및 Null이 아닌 유형

Kotlin에는 두 가지 유형의 nullable 및 null이 아닌 유형이 있습니다.

* **Nullable 유형**: Null 값을 보유할 수 있는 유형입니다. 코틀린은 ? (물음표)는 nullable 형식을 나타냅니다.

* **널이 아닌 유형**: 널 값을 보유할 수 없는 유형. 코틀린은 !! (이중 느낌표)는 null이 아닌 유형을 나타냅니다.

다음은 nullable 형식과 null이 아닌 형식을 선언하는 방법의 예입니다.

```kotlin
// Nullable type
var name: String? = "John"

// Non-null type
var age: Int = 20
```

보시다시피 nullable 형식은 ? null이 아닌 형식은 ? 없이 선언됩니다.

## Null 값 할당

nullable 형식에 null 값을 할당할 수 있지만 null이 아닌 형식에는 null 값을 할당할 수 없습니다.

null이 아닌 유형에 null 값을 할당하려고 하면 컴파일 타임 오류가 발생합니다.

다음은 null 허용 형식에 null 값을 할당하는 방법의 예입니다.

```kotlin
var name: String? = "John"

name = null
```

보시다시피 nullable 유형을 선언하고 null 값을 할당했습니다. 형식이 null을 허용하기 때문에 허용됩니다.

그러나 null이 아닌 유형으로 동일한 작업을 수행하려고 하면 컴파일 타임 오류가 발생합니다.

```kotlin
var age: Int = 20

age = null // This will give a compile-time error
```

## Null 값 확인

null 값을 사용하기 전에 항상 확인해야 합니다. Kotlin은 ?를 제공합니다. (안전 호출 연산자) 및 !! (not-null 어설션 연산자) null 값을 확인하는 데 도움이 됩니다.

?. 연산자는 값에 액세스하기 전에 값이 null인지 확인합니다. 값이 null이면 null을 반환합니다. 그렇지 않으면 값을 반환합니다.

다음은 ?를 사용하는 방법의 예입니다. 운영자:

```kotlin
var name: String? = "John"

// This will print "John"
println(name?.length)

name = null

// This will print "null"
println(name?.length)
```

보시다시피 길이 속성에 액세스하기 전에 name 변수가 null인지 확인했습니다. name 변수가 null이면 ?. 연산자는 null을 반환합니다. 그렇지 않으면 값을 반환합니다.

!! 연산자는 값을 강제로 래핑 해제하는 데 사용됩니다. 즉, null인 경우에도 값을 반환합니다.

값이 실제로 null인 경우 NullPointerException이 발생할 수 있으므로 위험할 수 있습니다.

다음은 !!을 사용하는 방법의 예입니다. 운영자:

```kotlin
var name: String? = "John"

// This will print "John"
println(name!!.length)

name = null

// This will give a NullPointerException
println(name!!.length)
```

보시다시피, 우리는 !! 이름 변수를 강제로 래핑 해제하는 연산자입니다. name 변수가 null인 경우에도 !! 연산자는 여전히 값을 반환합니다.

그러나 이름 변수의 길이 속성에 액세스하려고 하면 이름 변수가 실제로 null이기 때문에 NullPointerException이 발생합니다.

## 결론

이번 포스트에서는 Kotlin의 null 안전성에 대해 알아보았습니다. nullable 및 null이 아닌 유형과 null 값을 할당하는 방법에 대해 배웠습니다. ?에 대해서도 배웠습니다. 그리고 !! 연산자와 이를 사용하여 null 값을 확인하는 방법.