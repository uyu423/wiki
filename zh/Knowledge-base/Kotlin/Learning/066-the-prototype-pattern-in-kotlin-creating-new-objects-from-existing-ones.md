---
title: 066：Kotlin 中的原型模式：从现有对象创建新对象
description: 
published: true
date: 2023-01-31T10:17:35.759Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:17:32.308Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [066: The Prototype Pattern in Kotlin: Creating New Objects from Existing Ones***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/066-the-prototype-pattern-in-kotlin-creating-new-objects-from-existing-ones)
{.links-list}


  066：Kotlin 中的原型模式：从现有对象创建新对象

原型模式是一种在软件开发中使用的创建设计模式，当要创建的对象类型由原型实例确定时，原型实例被克隆以产生新对象。此模式用于：

- 避免从头开始创建新对象的开销，
- 避免需要“工厂”对象来管理对象创建，
- 避免需要“构建器”对象来组装对象。

原型模式是工厂方法和抽象工厂模式的替代方案，通常与它们结合使用。

原型模式的主要优点是它允许创建新对象而无需指定要创建的对象的确切类型。当事先不知道要创建的对象的类型，或者从头开始创建新对象的成本过高时，这会很有用。

原型模式的主要缺点是很难维护和更新原型，因为对原型的任何更改都会传播到所有克隆。

何时使用原型模式

在以下情况下应使用原型模式：

- 事先不知道要创建的对象的类型，
- 从头开始创建新对象的成本高得令人望而却步，
- 要创建的对象数量很大。

如何实现原型模式

可以使用以下步骤在 Kotlin 中实现原型模式：

1.创建一个类来表示原型。这个类应该有一个 clone() 方法，它返回原型的副本。

2. 创建扩展原型类的具体类。

3. 创建一个 main() 方法来实例化和克隆原型。

4. 通过从原型创建新对象并验证它们是克隆来测试原型模式。

这是 Kotlin 中原型模式的示例：

```kotlin
// The Prototype class

abstract class Prototype {

abstract fun clone(): Prototype

}

// The Concrete Prototype classes

class ConcretePrototypeA: Prototype {

override fun clone(): Prototype {

return ConcretePrototypeA()

}

}

class ConcretePrototypeB: Prototype {

override fun clone(): Prototype {

return ConcretePrototypeB()

}

}

// The main() method

fun main(args: Array<String>) {

val prototypeA = ConcretePrototypeA()

val prototypeB = ConcretePrototypeB()

// Clone the prototypes

val cloneA = prototypeA.clone()

val cloneB = prototypeB.clone()

// Verify that the prototypes have been cloned

println("cloneA is a clone of prototypeA: ${cloneA === prototypeA}")

println("cloneB is a clone of prototypeB: ${cloneB === prototypeB}")

}
```

在此示例中，Prototype 类是抽象的，并定义了一个由具体类实现的 clone() 方法。具体原型类是原型类的具体子类，它们覆盖了 clone() 方法以返回对象的副本。

main() 方法实例化两个原型，ConcretePrototypeA 和 ConcretePrototypeB，并克隆它们。然后验证克隆是原件的副本。

程序的输出如下：

```
cloneA is a clone of prototypeA: false

cloneB is a clone of prototypeB: false
```

从输出中可以看出，克隆与原型不是同一个对象，而是原型的副本。

何时使用原型模式

在以下情况下应使用原型模式：

- 事先不知道要创建的对象的类型，
- 从头开始创建新对象的成本高得令人望而却步，
- 要创建的对象数量很大。

原型模式的主要优点是它允许创建新对象而无需指定要创建的对象的确切类型。当事先不知道要创建的对象的类型，或者从头开始创建新对象的成本过高时，这会很有用。

原型模式的主要缺点是很难维护和更新原型，因为对原型的任何更改都会传播到所有克隆。

外部链接

- 维基百科上的原型模式 (https://en.wikipedia.org/wiki/Prototype_pattern)

- Java 中的原型设计模式 (https://www.geeksforgeeks.org/prototype-design-pattern/)

- Python 中的原型设计模式 (https://fkhadra.github.io/2017/02/01/python-prototype/)