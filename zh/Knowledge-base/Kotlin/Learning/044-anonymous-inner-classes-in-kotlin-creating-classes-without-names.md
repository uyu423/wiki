---
title: 044：Kotlin 中的匿名内部类：创建没有名称的类
description: 
published: true
date: 2023-02-15T10:17:49.510Z
tags: 
editor: markdown
dateCreated: 2023-02-15T10:17:47.788Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [044: Anonymous Inner Classes in Kotlin: Creating Classes Without Names***English** document is available*](/en/Knowledge-base/Kotlin/Learning/044-anonymous-inner-classes-in-kotlin-creating-classes-without-names)
{.links-list}


# Kotlin 中的匿名内部类：创建没有名称的类

在 Kotlin 中，您可以创建匿名内部类而无需为其命名。当您需要创建一次性对象时，或者当您需要仅在有限范围内使用的对象时，通常会使用这些类。

匿名内部类使用 `object` 关键字声明：

```kotlin
object: SomeClass() {
    // Body of the anonymous inner class
}
```

您还可以使用 `object` 关键字指定匿名内部类的超类型：

```kotlin
object: SomeInterface {
    // Body of the anonymous inner class
}
```

## 创建一个扩展类的匿名内部类

让我们创建一个扩展“Animal”类的匿名内部类。我们将创建一个具有“makeNoise”方法的“Animal”类。该方法将在匿名内部类中被重写。

```kotlin
open class Animal {
    open fun makeNoise() {
        println("Some noise")
    }
}

val animal = object: Animal() {
    override fun makeNoise() {
        println("Bark")
    }
}

animal.makeNoise() // Prints "Bark"
```

在上面的代码中，我们创建了一个 Animal 类和一个扩展它的匿名内部类。我们重写匿名内部类中的 makeNoise 方法。当我们在 `animal` 对象上调用 `makeNoise` 方法时，它会打印“Bark”。

## 创建一个实现接口的匿名内部类

您还可以创建实现接口的匿名内部类。让我们使用 `makeNoise` 方法创建一个 `Animal` 界面。我们将创建一个实现此接口的匿名内部类。

```kotlin
interface Animal {
    fun makeNoise()
}

val animal = object: Animal {
    override fun makeNoise() {
        println("Some noise")
    }
}

animal.makeNoise() // Prints "Some noise"
```

在上面的代码中，我们创建了一个 Animal 接口和一个实现它的匿名内部类。我们重写匿名内部类中的 makeNoise 方法。当我们在 `animal` 对象上调用 `makeNoise` 方法时，它会打印出“Some noise”。

## 创建一个扩展类并实现接口的匿名内部类

您还可以创建扩展类并实现接口的匿名内部类。让我们使用 `makeNoise` 方法创建一个 `Animal` 界面。我们还将创建一个具有“makeNoise”方法的“Animal”类。我们将创建一个匿名内部类，它扩展了“Animal”类并实现了“Animal”接口。

```kotlin
interface Animal {
    fun makeNoise()
}

open class Animal {
    open fun makeNoise() {
        println("Some noise")
    }
}

val animal = object: Animal(), Animal {
    override fun makeNoise() {
        println("Bark")
    }
}

animal.makeNoise() // Prints "Bark"
```

在上面的代码中，我们创建了一个 `Animal` 类和一个 `Animal` 接口。我们创建了一个匿名内部类，它扩展了“Animal”类并实现了“Animal”接口。我们重写匿名内部类中的 makeNoise 方法。当我们在 `animal` 对象上调用 `makeNoise` 方法时，它会打印“Bark”。

## 创建一个匿名内部类的对象

创建匿名内部类时，也会创建该类的一个对象。您可以使用 `object` 关键字访问该对象。

```kotlin
interface Animal {
    fun makeNoise()
}

open class Animal {
    open fun makeNoise() {
        println("Some noise")
    }
}

val animal = object: Animal(), Animal {
    override fun makeNoise() {
        println("Bark")
    }
}

println(animal.javaClass) // Prints "class com.example.Animal$1"
```

在上面的代码中，我们创建了一个 `Animal` 类和一个 `Animal` 接口。我们创建了一个匿名内部类，它扩展了“Animal”类并实现了“Animal”接口。我们使用 javaClass 属性打印了 animal 对象的类。如您所见，`animal` 对象是匿名内部类的一个实例。

## 创建静态嵌套类

您还可以在 Kotlin 中创建静态嵌套类。静态嵌套类使用 `static` 关键字声明：

```kotlin
class OuterClass {
    class NestedClass
}
```

静态嵌套类可以访问外部类的成员。它们也可以声明为“抽象”或“密封”。

```kotlin
class OuterClass {
    class NestedClass {
        fun someMethod() {
            println("Some method")
        }
    }
}

val nestedClass = OuterClass.NestedClass()
nestedClass.someMethod() // Prints "Some method"
```

在上面的代码中，我们创建了一个静态嵌套类和该类的一个实例。我们在 nestedClass 对象上调用了 someMethod 方法。

## 创建一个内部类

内部类是非静态嵌套类。内部类可以访问外部类的成员。它们也可以声明为“抽象”或“密封”。

```kotlin
class OuterClass {
    inner class InnerClass {
        fun someMethod() {
            println("Some method")
        }
    }
}

val outerClass = OuterClass()
val innerClass = outerClass.InnerClass()
innerClass.someMethod() // Prints "Some method"
```

在上面的代码中，我们创建了一个内部类和该类的一个实例。我们在 `innerClass` 对象上调用了 `someMethod` 方法。

## 结论

在这篇文章中，我们了解了 Kotlin 中的匿名内部类。我们看到了如何创建扩展类、实现接口以及扩展类和实现接口的匿名内部类。我们还看到了如何创建静态嵌套类和内部类。