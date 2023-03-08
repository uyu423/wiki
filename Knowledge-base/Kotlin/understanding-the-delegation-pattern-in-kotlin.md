---
title: Kotlin의 위임 패턴 이해
description: 
published: true
date: 2023-02-15T04:55:40.936Z
tags: 
editor: markdown
dateCreated: 2023-02-15T04:55:39.179Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Understanding the Delegation Pattern in Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/understanding-the-delegation-pattern-in-kotlin)
{.links-list}


# Kotlin의 위임 패턴 이해

위임 패턴은 소프트웨어 개발에서 다양한 목표를 달성하는 데 사용할 수 있는 강력한 기술입니다. Kotlin에서 위임 패턴은 보기의 수명 주기 관리에서 간단한 속성 위임 생성에 이르기까지 모든 작업에 사용할 수 있습니다. 이 기사에서는 위임 패턴이 무엇이며 Kotlin에서 어떻게 사용할 수 있는지 자세히 살펴보겠습니다.

## 위임 패턴이란 무엇입니까?

위임 패턴은 개체가 특정 작업에 대한 책임을 다른 개체에 위임할 수 있도록 하는 소프트웨어 설계 패턴입니다. 위임하는 객체를 **위임자**라고 하고, 책임을 위임받는 객체를 **위임자**라고 합니다.

위임 패턴은 종종 다음 목표 중 하나 이상을 달성하는 데 사용됩니다.

- 특정 작업에 대한 책임을 다른 개체에 위임하여 개체의 복잡성을 줄입니다.
- 개체가 특정 작업에 대한 책임을 해당 작업을 처리하는 데 더 적합한 다른 개체에 위임할 수 있도록 합니다.
- 객체가 특정 작업 자체를 구현하지 않도록 하기 위해 특정 작업에 대한 책임을 다른 객체에 위임할 수 있도록 합니다.

## 위임 패턴은 어떻게 작동합니까?

위임 패턴은 위임자와 위임자 간의 관계를 생성하여 작동합니다. 위임자는 일반적으로 위임자에게 위임할 수 있는 일련의 작업을 정의하는 인터페이스입니다. 그런 다음 대리인은 대리인 인터페이스를 구현하고 위임된 작업을 수행할 책임이 있습니다.

Kotlin에서는 **by** 키워드를 사용하여 위임 패턴을 구현할 수 있습니다. **by** 키워드는 대리인과 위임자 간의 위임 관계를 만드는 데 사용됩니다. 예를 들어 다음 코드는 속성 대리자와 속성 간에 위임 관계를 만듭니다.

```kotlin
val property by propertyDelegate
```

위의 코드에서 **val** 키워드는 속성을 생성하는 데 사용되고 **by** 키워드는 속성과 propertyDelegate 간의 위임 관계를 생성하는 데 사용되며 propertyDelegate는 위임의 이름입니다.

## 위임 패턴을 사용하는 이유는 무엇입니까?

위임 패턴은 여러 가지 이유로 사용될 수 있습니다. 위임 패턴을 사용하는 일반적인 이유 중 하나는 개체의 복잡성을 줄이는 것입니다. 예를 들어 뷰의 수명 주기 관리를 담당하는 개체는 뷰 생성 책임을 다른 개체에 위임할 수 있습니다. 이렇게 하면 수명 주기 관리 개체의 복잡성을 줄이고 코드를 더 쉽게 이해할 수 있습니다.

위임 패턴을 사용하는 또 다른 일반적인 이유는 개체가 특정 작업에 대한 책임을 해당 작업을 처리하는 데 더 적합한 다른 개체에 위임할 수 있도록 하기 위함입니다. 예를 들어 뷰의 상태를 관리하는 객체는 뷰를 그리는 책임을 다른 객체에 위임할 수 있습니다. 이것은 뷰를 그리는 책임을 다른 개체로 오프로드하여 상태 관리 개체의 성능을 향상시키는 데 도움이 될 수 있습니다.

## 위임 패턴을 사용하는 경우

위임 패턴은 다양한 상황에서 사용할 수 있습니다. 위임 패턴의 몇 가지 일반적인 사용 사례는 다음과 같습니다.

- **수명주기 관리**: 위임 패턴은 View의 수명주기 관리 책임을 다른 개체에 위임하는 데 사용할 수 있습니다. 이것은 코드의 복잡성을 줄이고 이해하기 쉽게 만드는 데 도움이 될 수 있습니다.
- **상태 관리**: 위임 패턴은 뷰의 상태 관리 책임을 다른 개체에 위임하는 데 사용할 수 있습니다. 이렇게 하면 보기를 그리는 책임을 다른 개체로 오프로드하여 코드 성능을 향상하는 데 도움이 될 수 있습니다.
- **이벤트 처리**: 위임 패턴은 이벤트 처리에 대한 책임을 다른 개체에 위임하는 데 사용할 수 있습니다. 이렇게 하면 이벤트 처리에 대한 책임을 다른 개체로 오프로드하여 코드의 성능을 향상하는 데 도움이 될 수 있습니다.
- **로깅**: 위임 패턴을 사용하여 다른 개체에 로깅 책임을 위임할 수 있습니다. 이는 다른 개체에 대한 로깅 책임을 오프로드하여 코드의 성능을 향상시키는 데 도움이 될 수 있습니다.

## Kotlin에서 위임 패턴을 사용하는 방법

Kotlin에서 위임 패턴을 사용하여 다양한 목표를 달성할 수 있습니다. 이 섹션에서는 Kotlin의 위임 패턴에 대한 가장 일반적인 사용 사례 중 일부를 살펴보겠습니다.

### 수명 주기 관리

Kotlin에서 위임 패턴의 일반적인 사용 사례 중 하나는 수명 주기 관리입니다. 위임 패턴은 보기의 수명 주기 관리 책임을 다른 개체에 위임하는 데 사용할 수 있습니다. 이것은 코드의 복잡성을 줄이고 이해하기 쉽게 만드는 데 도움이 될 수 있습니다.

다음 코드는 Kotlin에서 수명 주기 관리에 위임 패턴을 사용하는 방법의 예를 보여줍니다.

```kotlin
class LifecycleManager(val view: View) {

    fun onCreate() {
        // Delegate responsibility for creating the view to the view
        view.onCreate()
    }

    fun onDestroy() {
        // Delegate responsibility for destroying the view to the view
        view.onDestroy()
    }

}
```

위의 코드에서 **LifecycleManager** 클래스는 보기의 수명 주기 관리를 담당합니다. **LifecycleManager** 클래스에는 보기에 대한 참조를 유지하는 데 사용되는 **view** 속성이 있습니다. **LifecycleManager** 클래스에는 뷰의 수명 주기 관리 책임을 뷰에 위임하는 데 사용되는 **onCreate()** 및 **onDestroy()** 메서드도 있습니다.

### 상태 관리

Kotlin에서 위임 패턴의 또 다른 일반적인 사용 사례는 상태 관리입니다. 위임 패턴은 뷰의 상태를 관리하는 책임을 다른 개체에 위임하는 데 사용할 수 있습니다. 이렇게 하면 보기를 그리는 책임을 다른 개체로 오프로드하여 코드 성능을 향상하는 데 도움이 될 수 있습니다.

다음 코드는 Kotlin에서 상태 관리에 위임 패턴을 사용하는 방법의 예를 보여줍니다.

```kotlin
class StateManager(val view: View) {

    fun onCreate() {
        // Delegate responsibility for creating the view to the view
        view.onCreate()
    }

    fun onDestroy() {
        // Delegate responsibility for destroying the view to the view
        view.onDestroy()
    }

    fun onDraw() {
        // Delegate responsibility for drawing the view to the view
        view.onDraw()
    }

}
```

위의 코드에서 **StateManager** 클래스는 보기의 상태를 관리하는 역할을 합니다. **StateManager** 클래스에는 보기에 대한 참조를 유지하는 데 사용되는 **view** 속성이 있습니다. **StateManager** 클래스에는 뷰의 상태 관리 책임을 뷰에 위임하는 데 사용되는 **onCreate()**, **onDestroy()** 및 **onDraw()** 메서드도 있습니다. .

### 이벤트 처리

Kotlin에서 위임 패턴의 또 다른 일반적인 사용 사례는 이벤트 처리입니다. 위임 패턴은 이벤트 처리에 대한 책임을 다른 개체에 위임하는 데 사용할 수 있습니다. 이렇게 하면 이벤트 처리에 대한 책임을 다른 개체로 오프로드하여 코드의 성능을 향상하는 데 도움이 될 수 있습니다.

다음 코드는 Kotlin에서 이벤트 처리에 위임 패턴을 사용하는 방법의 예를 보여줍니다.

```kotlin
class EventManager(val view: View) {

    fun onCreate() {
        // Delegate responsibility for creating the view to the view
        view.onCreate()
    }

    fun onDestroy() {
        // Delegate responsibility for destroying the view to the view
        view.onDestroy()
    }

    fun onEvent(event: Event) {
        // Delegate responsibility for handling the event to the view
        view.onEvent(event)
    }

}
```

위의 코드에서 **EventManager** 클래스는 보기의 이벤트를 관리합니다. **EventManager** 클래스에는 보기에 대한 참조를 보유하는 데 사용되는 **보기** 속성이 있습니다. **EventManager** 클래스에는 View의 이벤트 관리 책임을 View에 위임하는 데 사용되는 **onCreate()**, **onDestroy()** 및 **onEvent()** 메서드도 있습니다. .

### 로깅

Kotlin에서 위임 패턴의 또 다른 일반적인 사용 사례는 로깅입니다. 위임 패턴을 사용하여 로깅 책임을 다른 개체에 위임할 수 있습니다. 이는 다른 개체에 대한 로깅 책임을 오프로드하여 코드의 성능을 향상시키는 데 도움이 될 수 있습니다.

다음 코드는 Kotlin 로그인에 위임 패턴을 사용하는 방법의 예를 보여줍니다.

```kotlin
class LogManager(val logger: Logger) {

    fun onCreate() {
        // Delegate responsibility for creating the logger to the logger
        logger.onCreate()
    }

    fun onDestroy() {
        // Delegate responsibility for destroying the logger to the logger
        logger.onDestroy()
    }

    fun log(message: String) {
        // Delegate responsibility for logging the message to the logger
        logger.log(message)
    }

}
```

위의 코드에서 **LogManager** 클래스는 로깅을 담당합니다. **LogManager** 클래스에는 로거에 대한 참조를 보유하는 데 사용되는 **logger** 속성이 있습니다. **LogManager** 클래스에는 로깅 책임을 로거에 위임하는 데 사용되는 **onCreate()**, **onDestroy()** 및 **log()** 메서드도 있습니다.

## 결론

위임 패턴은 소프트웨어 개발에서 다양한 목표를 달성하는 데 사용할 수 있는 강력한 기술입니다. Kotlin에서 위임 패턴은 보기의 수명 주기 관리에서 간단한 속성 위임 생성에 이르기까지 모든 작업에 사용할 수 있습니다. 이 기사에서는 위임 패턴이 무엇이고 Kotlin에서 어떻게 사용할 수 있는지 자세히 살펴보았습니다.