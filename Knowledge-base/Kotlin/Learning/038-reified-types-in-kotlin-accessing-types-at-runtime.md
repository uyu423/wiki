---
title: 038: Kotlin의 구체화된 유형: 런타임에 유형에 액세스
description: 
published: true
date: 2023-02-02T01:57:38.975Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:57:37.397Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [038: Reified Types in Kotlin: Accessing Types at Runtime***English** document is available*](/en/Knowledge-base/Kotlin/Learning/038-reified-types-in-kotlin-accessing-types-at-runtime)
{.links-list}


# 소개

Kotlin은 JVM에서 실행되는 정적 유형 언어입니다. Java와의 상호 운용성이 우수하며 Android 애플리케이션 개발에 탁월한 선택입니다.

Kotlin의 가장 강력한 기능 중 하나는 구체화된 유형에 대한 지원입니다. 이를 통해 런타임 시 유형에 액세스할 수 있으며 이는 Java에서는 불가능합니다.

이 게시물에서는 구체화된 유형이 무엇인지, Kotlin에서 어떻게 사용할 수 있는지 살펴보겠습니다. 또한 구체화된 유형을 사용하여 개발을 더 쉽게 만드는 방법에 대한 몇 가지 예를 볼 것입니다.

# 구체화된 유형이란 무엇입니까?

구체화된 유형은 런타임에 액세스할 수 있는 유형입니다. 컴파일 타임에만 유형을 사용할 수 있는 Java에서는 불가능합니다.

구체화된 유형은 리플렉션 작업에 매우 유용합니다. 리플렉션은 런타임에 클래스와 해당 멤버에 동적으로 액세스하는 방법입니다. 프레임워크와 라이브러리에서 자주 사용됩니다.

Kotlin에서 구체화된 유형은 'reified' 키워드로 선언됩니다. 예를 들어 다음과 같이 구체화된 유형을 선언할 수 있습니다.

```kotlin
reified val myType: String = "Hello, world!"
```

이제 런타임에 `myType` 유형에 액세스할 수 있습니다.

```kotlin
val type = myType::class
```

`type` 변수에는 `String` 클래스가 포함됩니다.

일반 유형의 유형에도 액세스할 수 있습니다.

```kotlin
reified val myList: List<String> = listOf("Hello", "world!")

val type = myList::class
```

`type` 변수는 `List` 클래스를 포함합니다.

# 구체화된 타입은 어떻게 사용할 수 있나요?

구체화된 유형은 여러 가지 방법으로 사용할 수 있습니다. 가장 일반적인 사용 사례 중 일부를 살펴보겠습니다.

## 리플렉션 작업

우리가 본 것처럼 구체화된 유형은 리플렉션 작업에 매우 유용합니다. 리플렉션은 런타임에 클래스와 해당 멤버에 동적으로 액세스하는 방법입니다.

Java에서 리플렉션은 프레임워크와 라이브러리에서 자주 사용됩니다. 예를 들어 Spring 프레임워크는 리플렉션을 사용하여 객체를 동적으로 생성합니다.

Kotlin에서는 리플렉션을 사용하여 클래스 멤버에 액세스할 수 있습니다.

```kotlin
reified val myClass: MyClass = MyClass()

val members = myClass::class.members
```

`members` 변수에는 `MyClass` 클래스의 모든 구성원 목록이 포함됩니다.

리플렉션을 사용하여 클래스의 주석에 액세스할 수도 있습니다.

```kotlin
reified val myClass: MyClass = MyClass()

val annotations = myClass::class.annotations
```

`annotations` 변수에는 `MyClass` 클래스의 모든 주석 목록이 포함됩니다.

## 제네릭 타입으로 작업하기

구체화된 유형은 제네릭 유형으로 작업하는 데에도 매우 유용합니다. Java에서는 런타임에 일반 유형의 유형에 액세스할 수 없습니다. 이로 인해 제네릭 형식으로 작업하기가 어려울 수 있습니다.

Kotlin에서는 구체화된 유형을 사용하여 일반 유형의 유형에 액세스할 수 있습니다.

```kotlin
reified val myList: List<String> = listOf("Hello", "world!")

val type = myList::class
```

`type` 변수는 `List` 클래스를 포함합니다.

구체화된 유형을 사용하여 일반 유형을 만들 수도 있습니다.

```kotlin
inline fun <reified T> createList(): List<T> {
    return listOf()
}

val myList = createList<String>()
```

`myList` 변수에는 빈 `List<String>`이 포함됩니다.

## 코틀린 리플렉션으로 작업하기

Kotlin 리플렉션은 런타임에 Kotlin 클래스와 해당 멤버에 동적으로 액세스하는 방법입니다. Java 리플렉션과 매우 유사하지만 사용하기가 훨씬 쉽습니다.

Kotlin에서는 구체화된 유형을 사용하여 클래스의 멤버에 액세스할 수 있습니다.

```kotlin
reified val myClass: MyClass = MyClass()

val members = myClass::class.members
```

`members` 변수에는 `MyClass` 클래스의 모든 구성원 목록이 포함됩니다.

구체화된 유형을 사용하여 클래스의 주석에 액세스할 수도 있습니다.

```kotlin
reified val myClass: MyClass = MyClass()

val annotations = myClass::class.annotations
```

`annotations` 변수에는 `MyClass` 클래스의 모든 주석 목록이 포함됩니다.

# 결론

이번 포스트에서는 구체화된 유형이 무엇이고 Kotlin에서 어떻게 사용되는지 살펴보았습니다. 우리는 또한 구체화된 유형을 사용하여 개발을 더 쉽게 만드는 방법에 대한 몇 가지 예를 보았습니다.

구체화된 유형은 다양한 방식으로 사용할 수 있는 Kotlin의 강력한 기능입니다. 리플렉션 또는 제네릭 형식으로 작업하는 경우 구체화된 형식이 큰 도움이 될 수 있습니다.