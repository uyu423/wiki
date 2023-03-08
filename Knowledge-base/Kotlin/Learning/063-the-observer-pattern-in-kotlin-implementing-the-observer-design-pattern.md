---
title: 063: Kotlin의 관찰자 패턴: 관찰자 디자인 패턴 구현
description: 
published: true
date: 2023-02-17T00:32:41.708Z
tags: 
editor: markdown
dateCreated: 2023-02-17T00:32:33.152Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [063: The Observer Pattern in Kotlin: Implementing the Observer Design Pattern***English** document is available*](/en/Knowledge-base/Kotlin/Learning/063-the-observer-pattern-in-kotlin-implementing-the-observer-design-pattern)
{.links-list}


# Kotlin의 옵저버 패턴: 옵저버 디자인 패턴 구현

관찰자 패턴은 주제라고 하는 개체가 관찰자라고 하는 종속 항목 목록을 유지 관리하고 일반적으로 해당 메서드 중 하나를 호출하여 상태 변경을 자동으로 알리는 소프트웨어 디자인 패턴입니다.

이벤트 기반 시스템을 구현하는 데 매우 유용한 패턴이며 동작 디자인 패턴 중 하나이기도 합니다.

## 옵저버 패턴이란?

관찰자 패턴은 주제라고 하는 개체가 관찰자라고 하는 종속 항목 목록을 유지 관리하고 일반적으로 해당 메서드 중 하나를 호출하여 상태 변경을 자동으로 알리는 소프트웨어 디자인 패턴입니다.

이벤트 기반 시스템을 구현하는 데 매우 유용한 패턴이며 동작 디자인 패턴 중 하나이기도 합니다.

관찰자 패턴에는 다음 참가자가 있습니다.
- Subject: 옵저버 목록을 유지하고 상태 변경을 알리는 객체
- 옵저버: 주체의 상태 변화를 통지받기 위해 객체가 구현해야 하는 인터페이스
- ConcreteObserver: Observer 인터페이스를 구현하고 주체의 상태 변화를 알리는 객체

## 옵저버 패턴은 언제 사용하나요?

옵저버 패턴은 다음과 같은 상황에서 사용됩니다.
- 추상화에 두 가지 측면이 있는 경우 하나는 다른 하나에 종속됩니다. 이러한 측면을 별도의 개체에 캡슐화하면 독립적으로 변경하고 재사용할 수 있습니다.
- 하나의 객체를 변경하려면 다른 객체도 변경해야 하고 얼마나 많은 객체를 변경해야 하는지 모를 때
- 객체가 누구인지에 대한 가정 없이 다른 객체에 알릴 수 있어야 하는 경우. 즉, 이러한 객체가 밀접하게 결합되는 것을 원하지 않습니다.

## Kotlin에서 관찰자 패턴을 구현하는 방법은 무엇입니까?

Kotlin에는 Observer Pattern이 내장되어 있지 않지만 구현하기 쉽습니다.

먼저 Subject 인터페이스를 생성해 보겠습니다.

```kotlin
interface Subject {
    fun addObserver(observer: Observer)
    fun removeObserver(observer: Observer)
    fun notifyObservers()
}
```

보시다시피 Subject 인터페이스에는 세 가지 메서드가 있습니다.
- addObserver(observer: Observer): 관찰자 목록에 관찰자를 추가합니다.
- removeObserver(observer: Observer): 관찰자 목록에서 관찰자를 제거합니다.
- notifyObservers(): 주체의 상태가 변경되었음을 모든 관찰자에게 알립니다.

이제 Observer 인터페이스를 생성해 보겠습니다.

```kotlin
interface Observer {
    fun update(subject: Subject)
}
```

Observer 인터페이스에는 하나의 메서드만 있습니다.
- update(subject: Subject): 주체의 상태가 변경되었을 때 호출됩니다. 이 메서드는 관찰자가 필요한 경우 주체의 상태를 쿼리할 수 있도록 주체를 매개 변수로 사용합니다.

이제 Subject 인터페이스를 구현하는 ConcreteSubject 클래스를 생성해 보겠습니다.

```kotlin
class ConcreteSubject : Subject {

    private val observers = mutableListOf<Observer>()
    private var state: Int = 0

    override fun addObserver(observer: Observer) {
        observers.add(observer)
    }

    override fun removeObserver(observer: Observer) {
        observers.remove(observer)
    }

    override fun notifyObservers() {
        for (observer in observers) {
            observer.update(this)
        }
    }

    fun setState(state: Int) {
        this.state = state
        notifyObservers()
    }

    fun getState(): Int {
        return state
    }
}
```

보시다시피 ConcreteSubject 클래스는 관찰자 목록을 유지하고 주제의 상태가 변경되면 이를 알립니다.

마지막으로 Observer 인터페이스를 구현하는 ConcreteObserver 클래스를 생성해 보겠습니다.

```kotlin
class ConcreteObserver : Observer {

    private var state: Int = 0

    override fun update(subject: Subject) {
        state = subject.getState()
    }

    fun getState(): Int {
        return state
    }
}
```

ConcreteObserver 클래스는 단순히 주제의 상태를 저장하고 이에 액세스하기 위한 getter 메소드를 제공합니다.

## 관찰자 패턴 테스트

이제 관찰자 패턴이 작동하는지 확인하는 테스트를 작성해 보겠습니다.

```kotlin
import org.junit.Test
import kotlin.test.assertEquals

class ObserverPatternTest {

    @Test
    fun testObserverPattern() {
        val subject = ConcreteSubject()

        val observer1 = ConcreteObserver()
        val observer2 = ConcreteObserver()

        subject.addObserver(observer1)
        subject.addObserver(observer2)

        subject.setState(1)
        assertEquals(1, observer1.getState())
        assertEquals(1, observer2.getState())

        subject.setState(2)
        assertEquals(2, observer1.getState())
        assertEquals(2, observer2.getState())

        subject.removeObserver(observer1)

        subject.setState(3)
        assertEquals(2, observer1.getState())
        assertEquals(3, observer2.getState())
    }
}
```

이 테스트에서는 먼저 ConcreteSubject와 두 개의 ConcreteObserver를 만듭니다. 그런 다음 주제에 관찰자를 추가하고 주제의 상태를 변경합니다. 그에 따라 관찰자의 상태가 변경되었다고 주장합니다. 마지막으로 관찰자 중 한 명을 제거하고 대상의 상태를 다시 변경합니다. 나머지 관찰자의 상태만 변경되었다고 주장합니다.

## 추가 정보

- 관찰자 패턴은 게시-구독 또는 게시-구독 패턴이라고도 합니다.
- 관찰자 패턴은 버튼 클릭과 같은 이벤트를 처리하기 위해 GUI 응용 프로그램에서 자주 사용됩니다.
- 관찰자 패턴은 MVC(Model-View-Controller) 아키텍처 패턴에서 사용됩니다.
- 옵저버 패턴은 MVVM(Model-View-ViewModel) 아키텍처 패턴에서 사용됩니다.

## 경고

- 종속성이 매우 적은 경우 관찰자 패턴을 사용하지 마십시오. 이 경우 종속 개체의 메서드를 직접 호출하는 것이 더 쉬울 수 있습니다.
- 알림이 전송되는 순서가 중요한 경우 관찰자 패턴을 사용하지 마십시오. 이 경우 중재자 패턴을 사용해야 합니다.

## 위험

- 관찰자 패턴은 종속성이 많은 매우 복잡한 개체 그래프로 이어질 수 있습니다. 유지 관리 및 디버깅이 어려울 수 있습니다.
- 옵저버 패턴은 옵저버가 더 이상 필요하지 않을 때 제대로 등록 해제되지 않으면 메모리 누수로 이어질 수 있습니다.