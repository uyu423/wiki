---
title: 001：Kotlin 简介：语言概述
description: 
published: true
date: 2023-01-31T06:04:18.159Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:04:16.539Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [001: Introduction to Kotlin: An Overview of the Language***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/001-introduction-to-kotlin-an-overview-of-the-language)
{.links-list}



# 科特林

Kotlin 是一种静态类型的编程语言，运行在 Java 虚拟机上，也可以编译成 JavaScript 源代码。 Kotlin 由 JetBrains 开发，该公司是 IntelliJ IDEA Java IDE 背后的公司。

Kotlin 是一种具有类型推断功能的跨平台、静态类型、通用编程语言。 Kotlin 旨在与 Java 完全互操作，其标准库的 JVM 版本依赖于 Java 类库，但类型推断使其语法更加简洁。

## 特征

科特林具有以下特点：

- **空安全**：Kotlin 的类型系统防止空引用被取消引用。

- **扩展功能**：Kotlin 允许您使用新功能扩展类，而无需从类继承。

- **高阶函数和 lambdas**：Kotlin 提供对高阶函数和 lambdas 的支持。

- **数据类**：Kotlin 提供了一种简洁的方法来创建仅包含数据的类。

- **伴随对象**：Kotlin 允许您在伴随对象中定义类的静态成员。

- **面向对象**：Kotlin 是面向对象的，但也提供了对函数式编程的支持。

- **Kotlin 标准库**：Kotlin 附带一个标准库，其中包含一组丰富的函数和类型。

## 句法

Kotlin 的语法简洁易学。

```kotlin
// Define a function that takes two Int arguments and returns an Int.
fun sum(a: Int, b: Int): Int {
   return a + b
}

// Define a data class.
data class User(val name: String, val age: Int)

// Define a companion object.
object MyClass {
   fun doSomething() { ... }
}

// Define a higher-order function.
fun MyClass.myFunction(a: Int, b: Int, f: (Int, Int) -> Int): Int {
   return f(a, b)
}

// Use a lambda expression.
val result = MyClass.myFunction(1, 2) { a, b -> a + b }

// Define an extension function.
fun String.toUpperCase(): String {
   return this.toUpperCase()
}
```

## 入门

要开始使用 Kotlin，您可以下载适用于 IntelliJ IDEA 或 Eclipse 的 Kotlin 插件。

您还可以使用 Kotlin 命令行编译器将 Kotlin 源代码编译为 JavaScript 或 JVM 字节码。

要了解有关 Kotlin 的更多信息，您可以查看以下资源：

- Kotlin 网站：https://kotlinlang.org

- Kotlin Koans：https://kotlinlang.org/docs/tutorials/koans.html

- Kotlin 标准库文档：https://kotlinlang.org/api/latest/jvm/stdlib/

- Kotlin 参考资料：https://kotlinlang.org/docs/reference/

## 结论

Kotlin 是一种简洁、安全且易于使用的编程语言，它运行在 JVM 上，也可以编译为 JavaScript。