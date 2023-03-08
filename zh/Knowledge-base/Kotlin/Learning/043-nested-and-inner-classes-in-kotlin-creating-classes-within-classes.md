---
title: 043：Kotlin 中的嵌套类和内部类：在类中创建类
description: 
published: true
date: 2023-02-16T13:32:31.290Z
tags: 
editor: markdown
dateCreated: 2023-02-16T13:32:29.312Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [043: Nested and Inner Classes in Kotlin: Creating Classes within Classes***English** document is available*](/en/Knowledge-base/Kotlin/Learning/043-nested-and-inner-classes-in-kotlin-creating-classes-within-classes)
{.links-list}


# 043：Kotlin 中的嵌套类和内部类：在类中创建类

Kotlin 支持两种可以在另一个类中创建的类：嵌套类和内部类。在这篇文章中，我们将了解 Kotlin 中嵌套类和内部类之间的区别，以及如何创建每种类型的类。

## 嵌套类

嵌套类是在另一个类中定义的类。嵌套类不是定义它们的类的成员。它们只是在另一个类中定义的类。

下面是 Kotlin 中嵌套类的示例：

```kotlin
class OuterClass {
    class NestedClass {
        // ...
    }
}
```

在上面的示例中，`NestedClass` 不是 `OuterClass` 的成员。它只是一个在 OuterClass 中定义的类。

嵌套类可用于将相关类组合在一起。例如，如果您有一个代表汽车的类，您可以创建一个代表汽车引擎的嵌套类。

嵌套类也可用于创建类的静态成员。在下面的示例中，“NestedClass”有一个名为“foo”的静态成员：

```kotlin
class OuterClass {
    class NestedClass {
        companion object {
            val foo = "bar"
        }
    }
}
```

在上面的示例中，“NestedClass”有一个名为“foo”的静态成员。这意味着可以在没有 OuterClass 实例的情况下访问 `NestedClass`。

## 内部类

内部类是在另一个类中定义的类，并且是该类的成员。内部类可以访问定义它们的类的成员。

这是 Kotlin 内部类的示例：

```kotlin
class OuterClass {
    inner class InnerClass {
        // ...
    }
}
```

在上面的示例中，“InnerClass”是“OuterClass”的成员。这意味着 `InnerClass` 可以访问 `OuterClass` 的成员。

内部类可用于创建与类的特定实例关联的对象。例如，如果您有一个代表汽车的类，您可以创建一个代表汽车引擎的内部类。

内部类也可以用来创建匿名类。匿名类是没有名称定义的类。匿名类对于创建不与类的任何特定实例相关联的对象很有用。

这是 Kotlin 中匿名内部类的示例：

```kotlin
class OuterClass {
    val anonymousInnerClass = object: SomeType {
        // ...
    }
}
```

在上面的示例中，创建了一个匿名内部类，它实现了 `SomeType` 接口。

## 结论

在这篇文章中，我们了解了 Kotlin 中嵌套类和内部类之间的区别。我们还看到了如何创建每种类型的类。