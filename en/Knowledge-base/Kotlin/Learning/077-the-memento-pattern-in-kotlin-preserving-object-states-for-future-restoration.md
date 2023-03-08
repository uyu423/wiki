---
title: 077: The Memento Pattern in Kotlin: Preserving Object States for Future Restoration
description: 
published: true
date: 2023-02-16T22:55:34.687Z
tags: 
editor: markdown
dateCreated: 2023-02-16T22:55:26.918Z
---

- [077: El patrón Memento en Kotlin: Preservar los estados de los objetos para futuras restauraciones***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/077-the-memento-pattern-in-kotlin-preserving-object-states-for-future-restoration)
{.links-list}
- [077：Kotlin 中的 Memento 模式：为将来的恢复保留对象状态***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/077-the-memento-pattern-in-kotlin-preserving-object-states-for-future-restoration)
{.links-list}
- [077: Kotlin의 Memento 패턴: 향후 복원을 위해 객체 상태 보존***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/077-the-memento-pattern-in-kotlin-preserving-object-states-for-future-restoration)
{.links-list}


# The Memento Pattern in Kotlin: Preserving Object States for Future Restoration

The memento pattern is a software design pattern that provides the ability to save and restore an object's state. It is often used in conjunction with undo/redo operations.

The memento pattern is a three-tier structure consisting of the originator, the caretaker, and the memento. 

The originator is the object whose state needs to be saved. The caretaker is the object responsible for saving and restoring the originator's state. The memento is an immutable object that stores the originator's state. 

The memento pattern is used to:

- Save and restore the state of an object
- Save and restore the state of an object's attributes
- Save and restore the state of an object's associations

## Implementing the Memento Pattern in Kotlin

There are two ways to implement the memento pattern in Kotlin:

- Using a data class
- Using a sealed class

### Using a Data Class

A data class is a class that is designed to hold data. Data classes have a number of features that make them ideal for implementing the memento pattern:

- Data classes are immutable
- Data classes have a `copy` method
- Data classes can be declared using the `data` keyword

To implement the memento pattern using a data class, we need to create a `Memento` class that stores the state of the `Originator` class. The `Originator` class has a `createMemento` method that creates a `Memento` object and a `restoreMemento` method that restores the state of the `Originator` from a `Memento` object.

Here is an example of how to implement the memento pattern using a data class:

```kotlin
data class Originator(var state: String) {
  
  fun createMemento(): Memento {
    return Memento(state)
  }
  
  fun restoreMemento(memento: Memento) {
    state = memento.state
  }
  
  data class Memento(val state: String)
}
```

### Using a Sealed Class

A sealed class is a class that can have one or more subclasses. Sealed classes are ideal for implementing the memento pattern because they:

- Can be declared using the `sealed` keyword
- Can have subclasses
- Can be declared `abstract`

To implement the memento pattern using a sealed class, we need to create a `Memento` sealed class that has a subclass for each state of the `Originator`. The `Originator` class has a `createMemento` method that creates a `Memento` object and a `restoreMemento` method that restores the state of the `Originator` from a `Memento` object.

Here is an example of how to implement the memento pattern using a sealed class:

```kotlin
sealed class Memento

class Originator(var state: String) {
  
  fun createMemento(): Memento {
    return when (state) {
      "state1" -> State1()
      "state2" -> State2()
      else -> throw IllegalArgumentException("Invalid state")
    }
  }
  
  fun restoreMemento(memento: Memento) {
    state = when (memento) {
      is State1 -> "state1"
      is State2 -> "state2"
      else -> throw IllegalArgumentException("Invalid memento")
    }
  }
  
  class State1 : Memento
  class State2 : Memento
}
```

## Conclusion

In this article, we have learned about the memento pattern and how to implement it in Kotlin using data classes and sealed classes.