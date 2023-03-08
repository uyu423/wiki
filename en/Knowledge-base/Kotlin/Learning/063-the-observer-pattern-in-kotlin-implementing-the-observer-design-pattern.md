---
title: 063: The Observer Pattern in Kotlin: Implementing the Observer Design Pattern
description: 
published: true
date: 2023-02-17T00:32:35.625Z
tags: 
editor: markdown
dateCreated: 2023-02-17T00:32:33.165Z
---

- [063: El patrón Observer en Kotlin: Implementando el patrón de diseño Observer***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/063-the-observer-pattern-in-kotlin-implementing-the-observer-design-pattern)
{.links-list}
- [063：Kotlin 中的观察者模式：实施观察者设计模式***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/063-the-observer-pattern-in-kotlin-implementing-the-observer-design-pattern)
{.links-list}
- [063: Kotlin의 관찰자 패턴: 관찰자 디자인 패턴 구현***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/063-the-observer-pattern-in-kotlin-implementing-the-observer-design-pattern)
{.links-list}


# The Observer Pattern in Kotlin: Implementing the Observer Design Pattern 

The Observer Pattern is a software design pattern in which an object, called the subject, maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods.

It's a very useful pattern for implementing event-driven systems, and it's also one of the behavioral design patterns.

## What is the Observer Pattern? 

The Observer Pattern is a software design pattern in which an object, called the subject, maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods.

It's a very useful pattern for implementing event-driven systems, and it's also one of the behavioral design patterns.

The Observer Pattern has the following participants: 
- Subject: the object that maintains a list of observers and notifies them of state changes 
- Observer: the interface that objects must implement to be notified of state changes in the subject 
- ConcreteObserver: the object that implements the Observer interface and is notified of state changes in the subject 

## When to Use the Observer Pattern? 

The Observer Pattern is used in the following situations: 
- When an abstraction has two aspects, one dependent on the other. Encapsulating these aspects in separate objects lets you vary and reuse them independently 
- When a change to one object requires changing others, and you don't know how many objects need to be changed 
- When an object should be able to notify other objects without making assumptions about who these objects are. In other words, you don't want these objects tightly coupled 

## How to Implement the Observer Pattern in Kotlin? 

Kotlin doesn't have a built-in Observer Pattern, but it's easy to implement it.

First, let's create the Subject interface: 

```kotlin
interface Subject {
    fun addObserver(observer: Observer)
    fun removeObserver(observer: Observer)
    fun notifyObservers()
}
```

As you can see, the Subject interface has three methods: 
- addObserver(observer: Observer): to add an observer to the list of observers 
- removeObserver(observer: Observer): to remove an observer from the list of observers 
- notifyObservers(): to notify all observers that the subject's state has changed 

Now let's create the Observer interface: 

```kotlin
interface Observer {
    fun update(subject: Subject)
}
```

The Observer interface has only one method: 
- update(subject: Subject): to be called when the subject's state has changed. This method takes the subject as a parameter so that the observer can query the subject's state if necessary 

Let's now create a ConcreteSubject class that implements the Subject interface: 

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

As you can see, the ConcreteSubject class maintains a list of observers and notifies them when the subject's state changes.

Finally, let's create a ConcreteObserver class that implements the Observer interface: 

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

The ConcreteObserver class simply stores the state of the subject and provides a getter method to access it.

## Testing the Observer Pattern 

Let's now write a test to see the Observer Pattern in action: 

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

In this test, we first create a ConcreteSubject and two ConcreteObservers. We then add the observers to the subject and change the subject's state. We assert that the observers' states have changed accordingly. Finally, we remove one of the observers and change the subject's state again. We assert that only the remaining observer's state has changed.

## Additional Information 

- The Observer Pattern is also known as the Publish-Subscribe or Pub-Sub Pattern 
- The Observer Pattern is often used in GUI applications to handle events such as button clicks 
- The Observer Pattern is used in the Model-View-Controller (MVC) architectural pattern 
- The Observer Pattern is used in the Model-View-ViewModel (MVVM) architectural pattern 

## Warnings 

- Don't use the Observer Pattern when the number of dependencies is very small. In this case, it's probably easier to just call the dependent object's methods directly 
- Don't use the Observer Pattern when the order in which the notifications are sent is important. In this case, you should use the Mediator Pattern 

## Dangers 

- The Observer Pattern can lead to very complex object graphs with a large number of dependencies. This can be hard to maintain and debug 
- The Observer Pattern can lead to memory leaks if observers are not properly unregistered when they're no longer needed