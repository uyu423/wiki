---
title: 081: Kotlin의 Reflection: 성찰 및 조작을 위한 Reflection API 이해
description: 
published: true
date: 2023-02-14T18:17:28.327Z
tags: 
editor: markdown
dateCreated: 2023-02-14T18:17:20.879Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [081: Reflection in Kotlin: Understanding the Reflection API for Introspection and Manipulation***English** document is available*](/en/Knowledge-base/Kotlin/Learning/081-reflection-in-kotlin-understanding-the-reflection-api-for-introspection-and-manipulation)
{.links-list}


# Kotlin의 Reflection: 성찰 및 조작을 위한 Reflection API 이해

Kotlin 리플렉션은 검사 및 조작에 사용할 수 있는 강력한 도구입니다. 이번 포스트에서는 리플렉션이 무엇인지, 그리고 Kotlin에서 어떻게 사용되는지 살펴보겠습니다. 또한 Kotlin Reflection API를 살펴보고 Kotlin 코드를 검사하고 조작하는 데 어떻게 사용할 수 있는지 알아봅니다.

## 리플렉션이란?

리플렉션은 내부 검사 또는 런타임에 코드를 검사하는 프로세스입니다. 이는 디버깅 또는 코드 생성과 같은 여러 가지 이유로 유용할 수 있습니다. 리플렉션은 메서드를 동적으로 호출하거나 필드 값을 변경하는 데에도 사용할 수 있습니다.

Kotlin에서 리플렉션은 주로 다음 두 가지 용도로 사용됩니다.

* 클래스와 그 구성원의 구조를 성찰하기 위해
* 메소드를 동적으로 호출하기 위해

## Kotlin에서 리플렉션 사용

Kotlin에서 리플렉션을 사용하려면 Kotlin 리플렉션 API를 가져와야 합니다.

```kotlin
import kotlin.reflect.*
```

리플렉션 API를 가져오면 이제 Kotlin 코드 검사를 시작할 수 있습니다.

## Kotlin 클래스 살펴보기

Kotlin 리플렉션 API로 가장 먼저 할 수 있는 일은 Kotlin 클래스를 살펴보는 것입니다. Kotlin 클래스를 검사하려면 먼저 해당 클래스에 대한 참조를 가져와야 합니다. `::class` 연산자를 사용하여 이를 수행할 수 있습니다.

```kotlin
val klass = MyClass::class
```

Kotlin 클래스에 대한 참조를 통해 이제 해당 구조를 검사할 수 있습니다. 예를 들어 클래스의 모든 구성원 목록을 얻을 수 있습니다.

```kotlin
val members = klass.members
```

클래스의 모든 속성 목록을 얻을 수도 있습니다.

```kotlin
val properties = klass.properties
```

그리고 클래스의 모든 기능 목록을 얻을 수 있습니다.

```kotlin
val functions = klass.functions
```

## Kotlin 클래스 조작

인트로스펙션 외에도 Kotlin 리플렉션 API를 조작에도 사용할 수 있습니다. 예를 들어 클래스의 인스턴스를 동적으로 생성할 수 있습니다.

```kotlin
val klass = MyClass::class
val instance = klass.createInstance()
```

또한 동적으로 클래스에서 메서드를 호출할 수 있습니다.

```kotlin
val klass = MyClass::class
val method = klass.getMethod("myMethod")
method.invoke(instance)
```

필드 값을 변경할 수 있습니다.

```kotlin
val klass = MyClass::class
val field = klass.getField("myField")
field.set(instance, "new value")
```

## 결론

이번 포스팅에서는 리플렉션이 무엇인지, 그리고 Kotlin에서 어떻게 사용되는지 알아보았습니다. 또한 Kotlin Reflection API를 살펴보고 Kotlin 코드를 검사하고 조작하는 데 어떻게 사용할 수 있는지 살펴보았습니다.