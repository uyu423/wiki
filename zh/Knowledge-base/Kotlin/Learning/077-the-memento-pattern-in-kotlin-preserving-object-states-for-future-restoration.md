---
title: 077：Kotlin 中的 Memento 模式：为将来的恢复保留对象状态
description: 
published: true
date: 2023-02-16T22:55:28.711Z
tags: 
editor: markdown
dateCreated: 2023-02-16T22:55:26.914Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [077: The Memento Pattern in Kotlin: Preserving Object States for Future Restoration***English** document is available*](/en/Knowledge-base/Kotlin/Learning/077-the-memento-pattern-in-kotlin-preserving-object-states-for-future-restoration)
{.links-list}


# Kotlin 中的 Memento 模式：为将来的恢复保留对象状态

备忘录模式是一种软件设计模式，它提供了保存和恢复对象状态的能力。它通常与撤消/重做操作结合使用。

纪念品模式是一个三层结构，由发起者、看管者和纪念品组成。

发起者是需要保存其状态的对象。看守者是负责保存和恢复发起者状态的对象。备忘录是一个不可变的对象，用于存储发起者的状态。

纪念品模式用于：

- 保存和恢复对象的状态
- 保存和恢复对象属性的状态
- 保存和恢复对象关联的状态

## 在 Kotlin 中实现 Memento 模式

在 Kotlin 中有两种方式实现备忘录模式：

- 使用数据类
- 使用密封类

### 使用数据类

数据类是设计用来保存数据的类。数据类有许多特性使它们成为实现备忘录模式的理想选择：

- 数据类是不可变的
- 数据类有一个 `copy` 方法
- 可以使用 `data` 关键字声明数据类

要使用数据类实现备忘录模式，我们需要创建一个 Memento 类来存储 Originator 类的状态。 `Originator` 类有一个创建 `Memento` 对象的 `createMemento` 方法和一个从 `Memento` 对象恢复 `Originator` 状态的 `restoreMemento` 方法。

下面是一个如何使用数据类实现备忘录模式的示例：

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

### 使用密封类

密封类是可以有一个或多个子类的类。密封类是实现备忘录模式的理想选择，因为它们：

- 可以使用 `sealed` 关键字声明
- 可以有子类
- 可以声明为“抽象”

要使用密封类实现备忘录模式，我们需要创建一个“备忘录”密封类，该类对于“发起者”的每个状态都有一个子类。 `Originator` 类有一个创建 `Memento` 对象的 `createMemento` 方法和一个从 `Memento` 对象恢复 `Originator` 状态的 `restoreMemento` 方法。

下面是一个如何使用密封类实现备忘录模式的示例：

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

## 结论

在本文中，我们了解了备忘录模式以及如何使用数据类和密封类在 Kotlin 中实现它。