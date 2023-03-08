---
title: 020：Kotlin 中的委托属性：实施委托模式
description: 
published: true
date: 2023-02-16T06:33:37.730Z
tags: 
editor: markdown
dateCreated: 2023-02-16T06:33:27.992Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [020: Delegated Properties in Kotlin: Implementing Delegation Patterns***English** document is available*](/en/Knowledge-base/Kotlin/Learning/020-delegated-properties-in-kotlin-implementing-delegation-patterns)
{.links-list}


# Kotlin 中的委托属性：实施委托模式

Kotlin 的委托模型建立在逐委托委托的思想之上。在此模式中，一个对象（委托）负责处理来自另一个对象（委托者）的请求。委托人可以将其全部或部分职责委托给委托人。

在 Kotlin 中，委托是一流的语言特性。您可以使用委托来实现常见的设计模式，例如观察者模式、装饰者模式和工厂模式。委派也可用于提高代码的性能。

在这篇文章中，我们将仔细研究 Kotlin 中的委托属性。我们将学习如何创建和使用委托属性，并探索使用委托的一些好处。

## 什么是委托属性？

委托属性是其值由委托计算的属性。委托是一个知道如何计算属性值的对象。在 Kotlin 中，您可以使用 `by` 关键字创建委托属性。

例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by lazy {
        // compute the name
    }
}
```

在此示例中，“名称”属性是委托属性。委托是 `Lazy` 类的一个实例。 `Lazy` 类知道如何计算 `name` 属性的值。

当您访问“name”属性时，“Lazy”实例将计算该属性的值并将其返回。该值将被缓存，以便后续对该属性的访问会很快。

## 创建委托属性

正如我们在上一节中看到的，您可以使用 `by` 关键字创建委托属性。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by lazy {
        // compute the name
    }
}
```

在此示例中，“名称”属性是委托属性。委托是 `Lazy` 类的一个实例。 `Lazy` 类知道如何计算 `name` 属性的值。

当您访问“name”属性时，“Lazy”实例将计算该属性的值并将其返回。该值将被缓存，以便后续对该属性的访问会很快。

您还可以使用属性委托创建委托属性。属性委托是一个知道如何计算属性值的对象。在 Kotlin 中，您可以使用 `by` 关键字创建属性委托。

例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用属性委托来创建此属性：

```kotlin
class User {
    val name: String by NameDelegate()
}
```

在此示例中，“名称”属性是委托属性。委托是 NameDelegate 类的一个实例。 `NameDelegate` 类知道如何计算 `name` 属性的值。

当您访问“name”属性时，“NameDelegate”实例将计算该属性的值并将其返回。该值将被缓存，以便后续对该属性的访问会很快。

## 实现委托

在 Kotlin 中，您可以使用 `by` 关键字创建委托。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by lazy {
        // compute the name
    }
}
```

在此示例中，“名称”属性是委托属性。委托是 `Lazy` 类的一个实例。 `Lazy` 类知道如何计算 `name` 属性的值。

当您访问“name”属性时，“Lazy”实例将计算该属性的值并将其返回。该值将被缓存，以便后续对该属性的访问会很快。

您还可以使用属性委托创建委托。属性委托是一个知道如何计算属性值的对象。在 Kotlin 中，您可以使用 `by` 关键字创建属性委托。

例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用属性委托来创建此属性：

```kotlin
class User {
    val name: String by NameDelegate()
}
```

在此示例中，“名称”属性是委托属性。委托是 NameDelegate 类的一个实例。 `NameDelegate` 类知道如何计算 `name` 属性的值。

当您访问“name”属性时，“NameDelegate”实例将计算该属性的值并将其返回。该值将被缓存，以便后续对该属性的访问会很快。

## 委托给地图

在 Kotlin 中，您可以使用 `by` 关键字来委托给地图。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by mapOf("id" to 1, "name" to "John")
}
```

在此示例中，“名称”属性是委托属性。代表是一张地图。当您访问 `name` 属性时，将在地图中搜索键 `name`。如果找到key，则返回相应的值。如果找不到密钥，将抛出异常。

## 委托给一个属性

在 Kotlin 中，您可以使用 `by` 关键字来委托给一个属性。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by lazy {
        firstName + " " + lastName
    }
}
```

在此示例中，“名称”属性是委托属性。委托是一个属性。当您访问 `name` 属性时，将访问并连接 `firstName` 和 `lastName` 属性。结果将被返回。

## 委托给函数

在 Kotlin 中，您可以使用 `by` 关键字来委托给一个函数。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by lazy {
        computeName()
    }
}
```

在此示例中，“名称”属性是委托属性。委托是一个函数。当您访问 `name` 属性时，将调用 `computeName()` 函数。结果将被返回。

## 委托给一个对象

在 Kotlin 中，您可以使用 `by` 关键字来委托给一个对象。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by NameDelegate()
}
```

在此示例中，“名称”属性是委托属性。委托是一个对象。当您访问“name”属性时，“NameDelegate”对象将用于计算该属性的值。结果将被返回。

## 委托给一个类

在 Kotlin 中，您可以使用 `by` 关键字来委托给一个类。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by lazy {
        NameDelegate.computeName()
    }
}
```

在此示例中，“名称”属性是委托属性。委托是一个类。当您访问 `name` 属性时，将调用 `NameDelegate.computeName()` 方法。结果将被返回。

## 委托给超类

在 Kotlin 中，您可以使用 `by` 关键字来委托给超类。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User : SuperUser() {
    val name: String by lazy {
        super.name
    }
}
```

在此示例中，“名称”属性是委托属性。委托是超类的“名称”属性。当您访问 `name` 属性时，将访问超类的 `name` 属性。结果将被返回。

## 委托给伴随对象

在 Kotlin 中，您可以使用 `by` 关键字来委托给伴生对象。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by lazy {
        User.name
    }
}
```

在此示例中，“名称”属性是委托属性。委托是伴随对象的“名称”属性。当您访问 `name` 属性时，将访问伴生对象的 `name` 属性。结果将被返回。

## 委托给接口

在 Kotlin 中，您可以使用 `by` 关键字来委托给接口。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by NameDelegate()
}
```

在此示例中，“名称”属性是委托属性。委托是一个接口。当您访问 `name` 属性时，`NameDelegate` 接口将用于计算该属性的值。结果将被返回。

## 委托给一个抽象类

在 Kotlin 中，您可以使用 `by` 关键字来委托给抽象类。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by lazy {
        NameDelegate.computeName()
    }
}
```

在此示例中，“名称”属性是委托属性。委托是一个抽象类。当您访问 `name` 属性时，将调用 `NameDelegate.computeName()` 方法。结果将被返回。

## 委托给一个对象字面量

在 Kotlin 中，您可以使用“by”关键字来委托给对象字面量。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by mapOf("id" to 1, "name" to "John")
}
```

在此示例中，“名称”属性是委托属性。委托是一个对象字面量。当您访问 `name` 属性时，将在地图中搜索键 `name`。如果找到key，则返回相应的值。如果找不到密钥，将抛出异常。

## 委托给嵌套类

在 Kotlin 中，您可以使用 `by` 关键字来委托给嵌套类。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by lazy {
        NestedClass.name
    }
}
```

在此示例中，“名称”属性是委托属性。委托是一个嵌套类。当您访问 `name` 属性时，将访问 `NestedClass.name` 属性。结果将被返回。

## 委托给内部类

在 Kotlin 中，您可以使用 `by` 关键字来委托给内部类。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by lazy {
        InnerClass.name
    }
}
```

在此示例中，“名称”属性是委托属性。委托是一个内部类。当您访问 `name` 属性时，将访问 `InnerClass.name` 属性。结果将被返回。

## 委托给匿名对象

在 Kotlin 中，您可以使用 `by` 关键字来委托给匿名对象。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by lazy {
        object: NameDelegate {
            override fun computeName(): String {
                // compute the name
            }
        }
    }
}
```

在此示例中，“名称”属性是委托属性。委托是一个匿名对象。当您访问 `name` 属性时，将调用匿名对象的 `computeName()` 方法。结果将被返回。

## 委托给 Lambda

在 Kotlin 中，您可以使用 `by` 关键字委托给 lambda。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by lazy {
        // compute the name
    }
}
```

在此示例中，“名称”属性是委托属性。委托是一个 lambda。当您访问 name 属性时，将调用 lambda。结果将被返回。

## 委托给方法引用

在 Kotlin 中，您可以使用 `by` 关键字来委托给方法引用。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性。您可以使用“by”关键字创建此属性：

```kotlin
class User {
    val name: String by lazy {
        User::name
    }
}
```

在此示例中，“名称”属性是委托属性。委托是一个方法引用。当您访问 `name` 属性时，将调用 `User` 类的 `name` 方法。结果将被返回。

## 委托给构造函数

在 Kotlin 中，您可以使用 `by` 关键字委托给构造函数。例如，假设您有一个表示用户的类。您可能想要创建一个存储用户名的属性