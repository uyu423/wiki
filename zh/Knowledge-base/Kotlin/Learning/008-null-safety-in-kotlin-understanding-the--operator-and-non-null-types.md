---
title: 008：Kotlin 中的空安全：理解 ?运算符和非空类型
description: 
published: true
date: 2023-01-31T05:24:38.873Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:24:37.194Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [008: Null Safety in Kotlin: Understanding the ? Operator and Non-Null Types***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/008-null-safety-in-kotlin-understanding-the--operator-and-non-null-types)
{.links-list}




# Kotlin 中的空安全：理解 ?运算符和非空类型

Kotlin 是一种在 JVM 上运行的静态类型编程语言。它与 Java 完全互操作，经常被用作 Android 开发的 Java 替代品。空安全是 Kotlin 的关键特性之一。它消除了空指针异常的风险，空指针异常可能是 Java 程序中的主要错误来源。

在 Kotlin 中，每个变量都必须声明为可空或非空。可空变量可以保存空值，而非空变量不能。这是在编译时强制执行的，因此不可能将空值分配给非空变量。

理解 Kotlin 中空安全的关键是 ?操作员。此运算符用于将变量标记为可为空。例如，以下变量可以包含空值或非空值：

```kotlin
var str: String? = "Hello, world!"
```

可空变量的类型通过添加 ?在类型名称之后。在上面的示例中，变量的类型是 String?。

如果您在不首先检查它是否为空的情况下尝试访问可为空的变量，则会出现编译时错误。例如，下面的代码将不会编译：

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str.length)
}
```

编译器知道 str 可以为 null，因此它不允许您调用它的 length 属性。要解决此问题，您需要在访问之前检查 str 是否为空：

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    if (str != null) {
        println(str.length)
    }
}
```

或者，您可以使用 ?运算符安全地访问可为 null 的变量。这将在访问变量之前检查变量是否为空。如果它为空，则整个表达式的计算结果将为空。例如：

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str?.length)
}
```

在上面的代码中，如果 str 为空，则表达式 str?.length 的计算结果为空。否则，它将评估为字符串的长度。

也可以使用 ?运算符指定变量为 null 时使用的默认值。例如：

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str?.length ?: 0)
}
```

在上面的代码中，如果 str 为 null，则表达式的计算结果为 0。否则，它将计算为字符串的长度。

从可空类型创建非空类型通常很有用。这可以使用 !!操作员。此运算符将可空类型转换为非空类型。但是，如果可空类型实际上为空，则会抛出异常。例如：

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str!!.length)
}
```

在上面的代码中，如果 str 为 null，则会抛出异常。否则，将打印字符串的长度。

也可以使用 ?运算符与 !!操作员。这将首先检查可空变量是否为空。如果为 null，它将返回 null。否则，它将可空变量转换为非空类型并返回它。例如：

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str?.length ?: 0)
}
```

在上面的代码中，如果 str 为 null，则表达式的计算结果将为 null。否则，它将评估为字符串的长度。

空安全是 Kotlin 的一个重要特性，可以帮助你避免空指针异常。通过仔细使用？运算符，您可以使您的代码更健壮并避免这些类型的错误。