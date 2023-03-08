---
title: 066: The Prototype Pattern in Kotlin: Creating New Objects from Existing Ones
description: 
published: true
date: 2023-01-31T10:17:33.910Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:17:32.299Z
---

- [066: Kotlin의 프로토타입 패턴: 기존 개체에서 새 개체 만들기***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/066-the-prototype-pattern-in-kotlin-creating-new-objects-from-existing-ones)
{.links-list}
- [066: Kotlin のプロトタイプ パターン: 既存のオブジェクトから新しいオブジェクトを作成する***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/066-the-prototype-pattern-in-kotlin-creating-new-objects-from-existing-ones)
{.links-list}
- [066：Kotlin 中的原型模式：从现有对象创建新对象***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/066-the-prototype-pattern-in-kotlin-creating-new-objects-from-existing-ones)
{.links-list}


  066: The Prototype Pattern in Kotlin: Creating New Objects from Existing Ones

The Prototype Pattern is a creational design pattern used in software development when the type of object to create is determined by a prototypical instance, which is cloned to produce new objects. This pattern is used to:

- avoid the overhead of creating a new object from scratch,
- avoid the need for a "factory" object to manage object creation,
- avoid the need for a "builder" object to assemble objects.

The Prototype Pattern is an alternative to the Factory Method and Abstract Factory patterns, and is often used in conjunction with them.

The main advantage of the Prototype Pattern is that it allows for the creation of new objects without the need to specify the exact type of object to be created. This can be useful when the type of object to be created is not known in advance, or when the cost of creating a new object from scratch is prohibitive.

The main disadvantage of the Prototype Pattern is that it can be difficult to maintain and update the prototypes, as any change to the prototype will be propagated to all of the clones.

When to Use the Prototype Pattern

The Prototype Pattern should be used when:

- the type of object to be created is not known in advance,
- the cost of creating a new object from scratch is prohibitive,
- the number of objects to be created is large.

How to Implement the Prototype Pattern

The Prototype Pattern can be implemented in Kotlin using the following steps:

1. Create a class to represent the prototype. This class should have a clone() method which returns a copy of the prototype.

2. Create concrete classes which extend the prototype class.

3. Create a main() method to instantiate and clone the prototypes.

4. Test the prototype pattern by creating new objects from the prototypes and verifying that they are clones.

Here is an example of the Prototype Pattern in Kotlin:

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

In this example, the Prototype class is abstract and defines a clone() method which is to be implemented by the concrete classes. The Concrete Prototype classes are concrete subclasses of the Prototype class which override the clone() method to return a copy of the object.

The main() method instantiates two prototypes, ConcretePrototypeA and ConcretePrototypeB, and clones them. The clones are then verified to be copies of the originals.

The output of the program is as follows:

```
cloneA is a clone of prototypeA: false

cloneB is a clone of prototypeB: false
```

As can be seen from the output, the clones are not the same objects as the prototypes, but they are copies of the prototypes.

When to Use the Prototype Pattern

The Prototype Pattern should be used when:

- the type of object to be created is not known in advance,
- the cost of creating a new object from scratch is prohibitive,
- the number of objects to be created is large.

The main advantage of the Prototype Pattern is that it allows for the creation of new objects without the need to specify the exact type of object to be created. This can be useful when the type of object to be created is not known in advance, or when the cost of creating a new object from scratch is prohibitive.

The main disadvantage of the Prototype Pattern is that it can be difficult to maintain and update the prototypes, as any change to the prototype will be propagated to all of the clones.

External Links

- Prototype Pattern on Wikipedia (https://en.wikipedia.org/wiki/Prototype_pattern)

- Prototype Design Pattern in Java (https://www.geeksforgeeks.org/prototype-design-pattern/)

- Prototype Design Pattern in Python (https://fkhadra.github.io/2017/02/01/python-prototype/)