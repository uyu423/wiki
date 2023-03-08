---
title: 050: Kotlin의 디자인 패턴: 일반적인 디자인 패턴을 코드에 적용
description: 
published: true
date: 2023-02-16T16:32:50.204Z
tags: 
editor: markdown
dateCreated: 2023-02-16T16:32:48.679Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [050: Design Patterns in Kotlin: Applying Common Design Patterns to Your Code.***English** document is available*](/en/Knowledge-base/Kotlin/Learning/050-design-patterns-in-kotlin-applying-common-design-patterns-to-your-code-)
{.links-list}


# 050: Kotlin의 디자인 패턴: 일반적인 디자인 패턴을 코드에 적용

디자인 패턴은 모든 소프트웨어 개발자 툴킷의 중요한 부분입니다. 개발자가 일반적인 문제에 대한 솔루션에 대해 통신하는 데 사용할 수 있는 공통 언어를 제공합니다. 디자인 패턴은 또한 코드를 더 읽기 쉽고 유지 관리하기 쉽게 만드는 데 도움이 됩니다.

Kotlin은 인기가 높아지고 있는 최신 프로그래밍 언어입니다. 디자인 패턴을 적용하기 위한 훌륭한 언어입니다. 이 게시물에서는 가장 일반적인 디자인 패턴과 이를 Kotlin에 적용하는 방법을 살펴보겠습니다.

## 창조적 패턴

생성 패턴은 객체 생성과 관련이 있습니다. 이러한 패턴은 개체 생성 프로세스를 제어하는 데 도움이 됩니다.

### 팩토리 패턴

팩터리 패턴은 객체를 생성하는 데 사용되는 생성 패턴입니다. 팩토리 패턴은 유형은 같지만 데이터가 다른 객체를 생성해야 할 때 유용합니다.

Kotlin에서 팩토리 패턴을 만들려면 팩토리 역할을 할 클래스를 만들어야 합니다. 이 클래스에는 지정한 유형의 객체를 생성하는 메서드가 있습니다.

```kotlin
class ObjectFactory {

 fun createObject(type: String): Any {

when (type) {
 "A" -> return ObjectA()
 "B" -> return ObjectB()
 else -> throw IllegalArgumentException("Unknown type")
}
}
}
```

그런 다음 팩토리를 사용하여 필요한 유형의 객체를 생성할 수 있습니다.

```kotlin
val factory = ObjectFactory()

val objectA = factory.createObject("A")
val objectB = factory.createObject("B")
```

팩토리 패턴은 객체 생성을 제어하는 좋은 방법입니다. 코드를 DRY(Don't Repeat Yourself)로 유지하는 좋은 방법이기도 합니다.

## 구조적 패턴

구조적 패턴은 객체의 구조 및 객체가 구성되는 방식과 관련이 있습니다. 이러한 패턴은 개체 간의 관계를 더 잘 이해하는 데 도움이 됩니다.

### 어댑터 패턴

어댑터 패턴은 하나의 인터페이스를 다른 인터페이스에 적응시키는 데 사용되는 구조적 패턴입니다. 어댑터 패턴은 기존 클래스를 사용해야 하지만 해당 인터페이스가 필요한 인터페이스와 일치하지 않을 때 유용합니다.

Kotlin에서 어댑터 패턴을 만들려면 어댑터 역할을 할 클래스를 만들어야 합니다. 이 클래스는 필요한 인터페이스를 구현하고 호출을 기존 클래스에 위임합니다.

```kotlin
class Adapter(val existingClass: ExistingClass) : InterfaceX {

override fun method1() {
 existingClass.method1()
}

override fun method2() {
 existingClass.method2()
}
}
```

그런 다음 어댑터를 사용하여 기존 클래스의 메서드에 액세스할 수 있습니다.

```kotlin
val adapter = Adapter(existingClass)

adapter.method1()
adapter.method2()
```

어댑터 패턴은 기존 코드를 재사용하는 좋은 방법입니다. 또한 코드를 더 읽기 쉽고 유지 관리하기 쉽게 만드는 좋은 방법입니다.

## 행동 패턴

행동 패턴은 객체의 행동과 관련이 있습니다. 이러한 패턴은 개체의 동작과 서로 상호 작용하는 방식을 더 잘 이해하는 데 도움이 됩니다.

### 관찰자 패턴

관찰자 패턴은 개체 간의 일대다 관계를 정의하는 데 사용되는 동작 패턴입니다. 옵저버 패턴은 특정 객체의 변경 사항을 여러 객체에 알려야 할 때 유용합니다.

Kotlin에서 옵저버 패턴을 만들려면 대상 역할을 할 클래스를 만들어야 합니다. 이 클래스에는 관찰자를 등록하는 방법과 관찰자에게 변경 사항을 알리는 방법이 있습니다.

```kotlin
class Subject {

private val observers = mutableListOf<Observer>()

fun registerObserver(observer: Observer) {
 observers.add(observer)
}

fun notifyObservers() {
 for (observer in observers) {
  observer.update()
 }
}
}
```

그런 다음 주제를 사용하여 관찰자에게 변경 사항을 알릴 수 있습니다.

```kotlin
val subject = Subject()

val observer1 = Observer1()
val observer2 = Observer2()

subject.registerObserver(observer1)
subject.registerObserver(observer2)

subject.notifyObservers()
```

관찰자 패턴은 객체를 분리하는 좋은 방법입니다. 또한 코드를 더 읽기 쉽고 유지 관리하기 쉽게 만드는 좋은 방법입니다.

## 결론

디자인 패턴은 모든 소프트웨어 개발자 툴킷의 중요한 부분입니다. 개발자가 일반적인 문제에 대한 솔루션에 대해 통신하는 데 사용할 수 있는 공통 언어를 제공합니다. 디자인 패턴은 또한 코드를 더 읽기 쉽고 유지 관리하기 쉽게 만드는 데 도움이 됩니다.

Kotlin은 디자인 패턴을 적용하기 위한 훌륭한 언어입니다. 이 게시물에서는 가장 일반적인 디자인 패턴과 이를 Kotlin에 적용하는 방법을 살펴보았습니다.