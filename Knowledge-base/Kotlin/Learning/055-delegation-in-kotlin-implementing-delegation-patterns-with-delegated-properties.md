---
title: 055: Kotlin의 위임: 위임된 속성으로 위임 패턴 구현
description: 
published: true
date: 2023-02-16T19:32:28.275Z
tags: 
editor: markdown
dateCreated: 2023-02-16T19:32:26.213Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [055: Delegation in Kotlin: Implementing Delegation Patterns with Delegated Properties***English** document is available*](/en/Knowledge-base/Kotlin/Learning/055-delegation-in-kotlin-implementing-delegation-patterns-with-delegated-properties)
{.links-list}


# Kotlin의 위임: 위임된 속성으로 위임 패턴 구현

Kotlin은 다양한 위임 패턴을 구현하는 데 사용할 수 있는 강력한 위임 메커니즘을 제공합니다. 이 게시물에서는 위임 속성을 사용하여 Kotlin에서 위임 패턴을 구현하는 방법을 살펴보겠습니다.

위임은 개체가 특정 작업에 대한 책임을 다른 개체에 위임할 수 있도록 하는 소프트웨어 설계 패턴입니다. 코드 모듈성과 재사용성을 개선하기 위해 위임을 사용할 수 있습니다.

다양한 위임 패턴이 있지만 가장 일반적인 것은 위임 패턴입니다. 위임 패턴에서 개체("위임자")는 다른 개체("요청자")의 요청을 처리할 책임이 있습니다.

위임 패턴은 객체 지향 프로그래밍에서 코드 모듈성을 개선하기 위해 자주 사용됩니다. 예를 들어 복잡한 작업을 수행해야 하는 클래스가 있는 경우 해당 작업을 다른 클래스에 위임할 수 있습니다. 이렇게 하면 위임 클래스의 코드를 다른 클래스에서 재사용할 수 있습니다.

코드 재사용성을 개선하기 위해 위임을 사용할 수도 있습니다. 예를 들어 클래스에 특정하지 않은 작업을 수행해야 하는 클래스가 있는 경우 해당 작업을 다른 클래스에 위임할 수 있습니다. 이렇게 하면 위임 클래스의 코드를 다른 클래스에서 재사용할 수 있습니다.

위임은 강력한 도구이지만 오용될 수 있습니다. 예를 들어 해당 작업에 적합하지 않은 클래스에 작업을 위임하면 위임 클래스의 코드가 복잡해지고 유지 관리가 어려워질 수 있습니다.

올바르게 사용하면 위임은 코드 모듈성과 재사용성을 향상시키는 매우 강력한 도구가 될 수 있습니다. 이 게시물에서는 위임 속성을 사용하여 Kotlin에서 위임 패턴을 구현하는 방법을 살펴보겠습니다.

위임 속성은 속성에 대한 책임을 다른 개체에 위임할 수 있는 Kotlin의 강력한 기능입니다. 위임된 속성은 by 키워드를 사용하여 선언됩니다. 예를 들어 다음 코드는 String 유형의 위임된 속성을 선언합니다.

```kotlin
class MyClass {
    val delegatedProperty: String by Delegate()
}
```

위의 코드에서 delegatedProperty 속성은 Delegate 클래스의 인스턴스에 위임됩니다. Delegate 클래스는 getValue() 및 setValue() 메서드를 구현해야 합니다. 이러한 메서드는 각각 위임된 속성의 값을 가져오고 설정하는 데 사용됩니다.

getValue() 및 setValue() 메서드는 위임된 속성을 소유하는 클래스의 인스턴스와 위임된 속성의 값이라는 두 가지 인수를 사용합니다. 예를 들어 다음 코드는 getValue() 및 setValue() 메서드를 구현하는 방법을 보여줍니다.

```kotlin
class Delegate {
    fun getValue(thisRef: Any, property: KProperty<*>): String {
        // return the value of the delegated property
    }

    fun setValue(thisRef: Any, property: KProperty<*>, value: String) {
        // set the value of the delegated property
    }
}
```

위의 코드에서 getValue() 및 setValue() 메서드는 Delegate 클래스에서 구현됩니다. 이러한 메서드는 위임된 속성을 소유하는 클래스의 인스턴스와 위임된 속성의 값이라는 두 가지 인수를 사용합니다.

getValue() 메서드는 위임된 속성의 값을 가져오는 데 사용됩니다. setValue() 메서드는 위임된 속성의 값을 설정하는 데 사용됩니다.

위임 속성은 위임 패턴을 구현하는 데 사용할 수 있는 Kotlin의 강력한 기능입니다. 다음 섹션에서는 위임된 속성을 사용하여 간단한 위임 패턴을 구현하는 방법을 살펴보겠습니다.