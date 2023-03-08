---
title: 022: Kotlin의 리플렉션: 런타임 시 클래스, 속성 및 함수에 대한 리플렉션
description: 
published: true
date: 2023-02-01T15:36:34.017Z
tags: 
editor: markdown
dateCreated: 2023-02-01T15:36:32.418Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [022: Reflection in Kotlin: Reflecting on Classes, Properties, and Functions at Runtime***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/022-reflection-in-kotlin-reflecting-on-classes-properties-and-functions-at-runtime)
{.links-list}


# Kotlin의 리플렉션

Kotlin 리플렉션은 런타임에 Kotlin 코드를 검사하고 조작하는 데 사용할 수 있는 강력한 도구입니다. 이 기사에서는 리플렉션이 무엇이며 Kotlin 클래스, 속성 및 함수를 검사하는 데 리플렉션을 어떻게 사용할 수 있는지 살펴보겠습니다.

## 리플렉션이란?

리플렉션은 프로그램이 런타임에 자체적으로 검사하고 조작하는 기능입니다. 이것은 프로그램의 구조를 검사하고 동적으로 메서드를 호출하며 런타임에 프로그램의 구조를 변경하는 데 사용할 수 있습니다.

리플렉션은 강력한 도구이지만 비용이 듭니다. 리플렉션은 직접 메서드 호출보다 느린 경우가 많으며 코드를 이해하기 어렵게 만들 수 있습니다. 따라서 꼭 필요한 경우에만 아껴서 사용해야 합니다.

## Kotlin의 리플렉션

Kotlin 리플렉션은 Java Reflection API를 기반으로 합니다. 즉, Java로 작성할 수 있는 모든 코드는 Kotlin으로도 작성할 수 있습니다. 그러나 Kotlin은 리플렉션을 사용하기 쉽게 만드는 여러 기능을 추가합니다.

Kotlin 리플렉션의 가장 중요한 기능 중 하나는 도트 연산자를 사용하여 클래스 멤버에 액세스하는 기능입니다. 예를 들어 다음 Kotlin 클래스를 고려하십시오.

```kotlin
class Foo {
    fun bar() {}
}
```

리플렉션을 사용하여 다음과 같이 이 클래스의 `bar()` 함수에 액세스할 수 있습니다.

```kotlin
val foo = Foo()
val bar = foo::class.memberFunctions.first { it.name == "bar" }
```

이는 다음과 같은 Java의 동등한 코드보다 훨씬 간단합니다.

```java
Foo foo = new Foo();
Method bar = foo.getClass().getDeclaredMethods()[0];
```

도트 연산자 외에도 Kotlin 리플렉션은 일반적인 작업을 더 쉽게 만들어주는 여러 고급 함수를 제공합니다. 예를 들어 `kotlin.reflect.full.declaredMemberProperties` 함수를 사용하여 클래스에 선언된 모든 속성 목록을 가져올 수 있습니다.

```kotlin
val foo = Foo()
val properties = kotlin.reflect.full.declaredMemberProperties(foo)
```

이는 다음 Java 코드와 동일합니다.

```java
Foo foo = new Foo();
Field[] fields = foo.getClass().getDeclaredFields();
```

## 리플렉션 사용 사례

리플렉션은 다양한 작업에 사용할 수 있지만 가장 일반적인 사용 사례는 다음과 같습니다.

* **성찰**: 리플렉션은 Kotlin 프로그램의 구조를 성찰하는 데 사용할 수 있습니다. 예를 들어 Kotlin 라이브러리에 대한 문서를 자동으로 생성하는 데 사용할 수 있습니다.

* **동적 호출**: 리플렉션을 사용하여 Kotlin 메서드를 동적으로 호출할 수 있습니다. 예를 들어 이것은 컴파일 타임에 알려지지 않은 메서드를 호출하는 데 사용할 수 있습니다.

* **런타임 코드 생성**: 리플렉션을 사용하여 런타임에 Kotlin 코드를 생성할 수 있습니다. 예를 들어 사용자 입력을 기반으로 Kotlin 클래스를 동적으로 생성하는 데 사용할 수 있습니다.

## 리플렉션의 한계

리플렉션은 강력한 도구이지만 몇 가지 제한 사항이 있습니다. 가장 중요한 제한 사항 중 일부는 다음과 같습니다.

* **보안**: 리플렉션을 사용하여 Kotlin 컴파일러에서 수행하는 보안 검사를 우회할 수 있습니다. 예를 들어 개인 메서드를 동적으로 호출하거나 개인 필드에 액세스하는 데 사용할 수 있습니다.

* **성능**: 리플렉션은 종종 직접 메서드 호출보다 느립니다. 예를 들어 자주 호출되는 메서드를 동적으로 호출하기 위해 리플렉션을 사용하는 경우 문제가 될 수 있습니다.

* **신뢰성**: 리플렉션을 사용하여 런타임에 Kotlin 프로그램의 구조를 변경할 수 있습니다. 예를 들어 두 개의 코드 조각이 리플렉션을 사용하여 동일한 클래스를 검사하고 그 중 하나가 클래스의 구조를 변경하는 경우 문제가 발생할 수 있습니다.

## 결론

이 기사에서는 리플렉션이 무엇이며 런타임에 Kotlin 코드를 검사하고 조작하는 데 리플렉션을 사용하는 방법을 살펴보았습니다. 우리는 또한 리플렉션의 일부 사용 사례와 리플렉션 사용의 일부 제한 사항을 확인했습니다.