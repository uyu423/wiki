---
title: 042: Sealed Classes in Kotlin: Restricting Class Hierarchies
description: 
published: true
date: 2023-01-31T10:36:19.068Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:36:15.740Z
---

- [042: Kotlin의 봉인된 클래스: 클래스 계층 구조 제한***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/042-sealed-classes-in-kotlin-restricting-class-hierarchies)
{.links-list}
- [042: Kotlin の封印されたクラス: クラス階層の制限***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/042-sealed-classes-in-kotlin-restricting-class-hierarchies)
{.links-list}
- [042：Kotlin 中的密封类：限制类层次结构***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/042-sealed-classes-in-kotlin-restricting-class-hierarchies)
{.links-list}



# 042: Sealed Classes in Kotlin: Restricting Class Hierarchies

Sealed classes are a powerful tool in Kotlin for restricting class hierarchies. By sealing a class, we can prevent it from being extended by any other class. This can be useful in a number of situations, for example, when we want to restrict a class to only be extended by classes in the same file.

Sealed classes are declared using the sealed keyword:

```kotlin
sealed class MySealedClass
```

Once a class is sealed, it cannot be extended by any other class, except for those classes that are declared in the same file as the sealed class. For example, the following code will not compile:

```kotlin
// MySealedClass.kt

sealed class MySealedClass

class MySubclass : MySealedClass() // Will not compile
```

In order to extend a sealed class, the subclass must be declared in the same file as the sealed class. This is known as *local sealed class*

```kotlin
// MySealedClass.kt

sealed class MySealedClass

class MySubclass : MySealedClass() // Compiles
```

Sealed classes can also be *nested* inside other classes or objects. In this case, the sealed class can only be extended by classes that are declared *inside* the same parent class or object. For example:

```kotlin
// MyOuterClass.kt

class MyOuterClass {

    sealed class MySealedClass

    class MySubclass : MySealedClass() // Compiles
}

class MyOtherSubclass : MyOuterClass.MySealedClass() // Will not compile
```

Sealed classes are a useful tool for restricting class hierarchies, and can be used in a number of different situations. In particular, they can be helpful for ensuring that a class can only be extended by classes in the same file.