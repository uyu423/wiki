---
title: 063：Kotlin 中的观察者模式：实施观察者设计模式
description: 
published: true
date: 2023-02-17T00:32:41.708Z
tags: 
editor: markdown
dateCreated: 2023-02-17T00:32:33.154Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [063: The Observer Pattern in Kotlin: Implementing the Observer Design Pattern***English** document is available*](/en/Knowledge-base/Kotlin/Learning/063-the-observer-pattern-in-kotlin-implementing-the-observer-design-pattern)
{.links-list}


# Kotlin 中的观察者模式：实施观察者设计模式

观察者模式是一种软件设计模式，其中一个对象（称为主题）维护其从属列表（称为观察者），并自动通知它们任何状态更改，通常是通过调用它们的方法之一。

它是实现事件驱动系统非常有用的模式，也是行为设计模式之一。

## 什么是观察者模式？

观察者模式是一种软件设计模式，其中一个对象（称为主题）维护其从属列表（称为观察者），并自动通知它们任何状态更改，通常是通过调用它们的方法之一。

它是实现事件驱动系统非常有用的模式，也是行为设计模式之一。

观察者模式有以下参与者：
- Subject：维护观察者列表并通知他们状态变化的对象
- 观察者：对象必须实现的接口，以通知主题的状态变化
- ConcreteObserver：实现Observer接口的对象，被通知主体状态变化

## 何时使用观察者模式？

观察者模式用于以下情况：
- 当一个抽象有两个方面时，一个依赖于另一个。将这些方面封装在单独的对象中可以让您独立地改变和重用它们
- 当对一个对象的更改需要更改其他对象，而您不知道需要更改多少对象时
- 当一个对象应该能够通知其他对象而不假设这些对象是谁时。换句话说，您不希望这些对象紧密耦合

## 如何在 Kotlin 中实现观察者模式？

Kotlin 没有内置观察者模式，但很容易实现。

首先，让我们创建 Subject 接口：

```kotlin
interface Subject {
    fun addObserver(observer: Observer)
    fun removeObserver(observer: Observer)
    fun notifyObservers()
}
```

可以看到，Subject接口有3个方法：
- addObserver(observer: Observer): 添加一个观察者到观察者列表
- removeObserver(observer: Observer): 从观察者列表中移除一个观察者
- notifyObservers()：通知所有观察者主体的状态已经改变

现在让我们创建 Observer 接口：

```kotlin
interface Observer {
    fun update(subject: Subject)
}
```

Observer 接口只有一个方法：
- update(subject: Subject)：当主题的状态改变时被调用。此方法将主题作为参数，以便观察者可以在必要时查询主题的状态

现在让我们创建一个实现 Subject 接口的 ConcreteSubject 类：

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

如您所见，ConcreteSubject 类维护了一个观察者列表，并在主体的状态发生变化时通知他们。

最后，让我们创建一个实现 Observer 接口的 ConcreteObserver 类：

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

ConcreteObserver 类仅存储主题的状态并提供访问它的 getter 方法。

## 测试观察者模式

现在让我们编写一个测试来查看观察者模式的运行情况：

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

在这个测试中，我们首先创建一个 ConcreteSubject 和两个 ConcreteObservers。然后我们将观察者添加到主题并更改主题的状态。我们断言观察者的状态已相应改变。最后，我们移除其中一个观察者并再次改变对象的状态。我们断言只有剩下的观察者的状态发生了变化。

## 附加信息

- 观察者模式也称为发布-订阅或发布-订阅模式
- 观察者模式常用于 GUI 应用程序来处理按钮点击等事件
- 观察者模式用于模型-视图-控制器 (MVC) 架构模式
- 观察者模式用于模型-视图-视图模型（MVVM）架构模式

## 警告

- 当依赖数量很少时不要使用观察者模式。在这种情况下，直接调用依赖对象的方法可能更容易
- 当发送通知的顺序很重要时，不要使用观察者模式。在这种情况下，您应该使用中介者模式

## 危险

- 观察者模式会导致具有大量依赖关系的非常复杂的对象图。这可能很难维护和调试
- 如果观察者在不再需要时未正确注销，则观察者模式可能导致内存泄漏