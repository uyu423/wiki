---
title: Kotlin과 Java 간의 상호 운용성
description: 
published: true
date: 2023-02-09T08:55:26.174Z
tags: 
editor: markdown
dateCreated: 2023-02-09T08:55:20.010Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Interoperability Between Kotlin and Java***English** document is available*](/en/Knowledge-base/Kotlin/interoperability-between-kotlin-and-java)
{.links-list}



# 코틀린과 자바의 상호운용성

Java와 Kotlin은 Android 앱 개발에 사용되는 두 가지 인기 있는 프로그래밍 언어입니다. Kotlin은 최신 언어이지만 Java와 완벽하게 상호 운용됩니다. 즉, 동일한 프로젝트에서 Kotlin과 Java를 함께 사용할 수 있고 Java에서 Kotlin 코드를 호출할 수 있으며 그 반대도 가능합니다. 이 기사에서는 Kotlin과 Java가 상호 운용되는 방식과 Android 앱 개발에서 두 언어를 모두 사용할 수 있는 방법을 살펴보겠습니다.

## 자바에서 Kotlin 호출하기

Java에서 Kotlin을 호출하는 것은 원활하고 간단합니다. Java 코드에서 모든 Kotlin 코드를 호출할 수 있으며 그 반대도 가능합니다. 특별한 주석이나 구성을 추가할 필요가 없습니다.

Java에서 Kotlin 코드를 호출하려면 Kotlin 클래스, 메서드 또는 속성의 정규화된 이름을 사용하기만 하면 됩니다. 예를 들어 Java에서 `Foo` 클래스의 `foo()` 함수를 호출하려면 다음 코드를 사용합니다.

```java
FooKt.foo();
```

Kotlin에서 Java 코드를 호출하려면 `@JvmName` 주석을 사용하세요. 이 주석을 사용하면 Java에서 호출할 때 사용할 Kotlin 함수 또는 속성의 이름을 지정할 수 있습니다. 예를 들어 다음 Kotlin 코드는 다음과 같습니다.

```kotlin
@JvmName("bar")
fun foo() {
    // ...
}
```

다음 코드를 사용하여 Java에서 호출할 수 있습니다.

```java
FooKt.bar();
```

## Null 허용 및 Null이 아닌 유형 작업

Kotlin에는 null 포인터 예외를 방지하는 데 도움이 되는 nullable 및 null이 아닌 유형이 있습니다. Kotlin에서는 유형 이름 뒤에 `?`를 추가하여 모든 유형을 nullable로 만들 수 있습니다. 예를 들어 다음 Kotlin 코드는 nullable `String`을 정의합니다.

```kotlin
var s: String? = null
```

Java에서 Kotlin 코드를 호출할 때 null을 허용하는 모든 유형은 자동으로 null이 아닌 유형으로 변환됩니다. 예를 들어 다음 Kotlin 코드는 다음과 같습니다.

```kotlin
fun foo(s: String?) {
    // ...
}
```

다음 코드를 사용하여 Java에서 호출할 수 있습니다.

```java
foo("Hello");
```

## 자바 컬렉션 작업

Kotlin과 Java는 컬렉션에 대한 접근 방식이 매우 다릅니다. Kotlin에서는 모든 컬렉션이 기본적으로 변경할 수 없지만 Java에서는 변경할 수 있습니다. 이는 Java 컬렉션으로 작업하는 데 익숙한 개발자를 방해할 수 있습니다.

다행스럽게도 Kotlin은 Kotlin과 Java 컬렉션 간에 쉽게 변환할 수 있는 방법을 제공합니다. Java 컬렉션을 Kotlin 컬렉션으로 변환하려면 `toMutableList()` 또는 `toList()` 함수를 사용할 수 있습니다. 예를 들어 다음 Java 코드는 다음과 같습니다.

```java
List<String> list = Arrays.asList("a", "b", "c");
```

`toList()` 함수를 사용하여 Kotlin `List`로 변환할 수 있습니다.

```kotlin
val list = list.toList()
```

Kotlin 컬렉션을 Java 컬렉션으로 변환하려면 `toJavaList()` 또는 `toJavaSet()` 함수를 사용할 수 있습니다. 예를 들어 다음 Kotlin 코드는 다음과 같습니다.

```kotlin
val list = listOf("a", "b", "c")
```

`toJavaList()` 함수를 사용하여 Java `List`로 변환할 수 있습니다.

```java
List<String> list = list.toJavaList();
```

## 결론

Kotlin과 Java는 완전히 상호 운용 가능한 두 가지 인기 있는 프로그래밍 언어입니다. 즉, 동일한 프로젝트에서 Kotlin과 Java를 함께 사용할 수 있고 Java에서 Kotlin 코드를 호출할 수 있으며 그 반대도 가능합니다. 이 기사에서는 Kotlin과 Java가 상호 운용되는 방식과 Android 앱 개발에서 두 언어를 모두 사용할 수 있는 방법을 살펴보았습니다.