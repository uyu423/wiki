---
title: Kotlin 和输入验证：最佳实践和常见陷阱
description: 
published: true
date: 2023-02-05T11:17:24.322Z
tags: 
editor: markdown
dateCreated: 2023-02-05T11:17:22.754Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kotlin and Input Validation: Best Practices and Common Pitfalls***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-input-validation-best-practices-and-common-pitfalls)
{.links-list}


# Kotlin 和输入验证：最佳实践和常见陷阱

## 介绍

输入验证是任何应用程序的关键部分，无论是 Web 应用程序、移动应用程序还是桌面应用程序。如果没有适当的输入验证，应用程序很容易受到各种攻击，包括 SQL 注入、跨站点脚本 (XSS) 和中间人 (MITM) 攻击。

在本文中，我们将了解 Kotlin 中输入验证的一些最佳实践，以及需要避免的一些常见陷阱。

## 最佳实践

### 1. 为工作使用正确的工具

Kotlin 中有许多不同的库和框架可用于输入验证。根据项目的要求，为工作选择合适的工具很重要。

例如，kotlinx.html 库提供了一组用于验证 HTML 输入的函数和对象。 kotlinx.validation 库提供了一组用于验证 XML 输入的函数和对象。

### 2.预先定义验证规则

在开始编码之前，定义需要实施的验证规则非常重要。这将有助于避免代码重复，并使代码更易于维护。

### 3. 使用显式类型

定义验证规则时，最好使用显式类型。例如，与其使用 Any 类型，不如使用特定类型，例如 String 或 Int。

### 4. 避免使用可空类型

应尽可能避免可空类型，因为它们会导致意外结果。如果绝对需要可空类型，最好使用提供空安全的库，例如 kotlinx.validation 库。

### 5.使用肯定断言

编写验证代码时，最好使用肯定断言。换句话说，验证代码应该检查特定值的存在，而不是值的缺失。

### 6.注意短路

当与输入验证结合使用时，Kotlin 的短路行为可能会导致意外结果。例如，考虑以下代码：

```kotlin
fun validateInput(input: String): Boolean {
    // Validation code here
}

fun main() {
    val input = "test"
    if (validateInput(input) && input.isNotEmpty()) {
        // Do something with the input
    }
}
```

在这段代码中，首先调用了 validateInput() 函数，然后调用了 input.isNotEmpty() 函数。但是，由于 Kotlin 的短路行为，如果 validateInput() 函数返回 false，则永远不会调用 input.isNotEmpty() 函数。

为避免此问题，最好使用 let() 函数，如下所示：

```kotlin
fun validateInput(input: String): Boolean {
    // Validation code here
}

fun main() {
    val input = "test"
    input.let {
        if (validateInput(it) && it.isNotEmpty()) {
            // Do something with the input
        }
    }
}
```

在此代码中，let() 函数用于调用 validateInput() 函数和 input.isNotEmpty() 函数。这可确保始终调用这两个函数，而不管 validateInput() 函数的返回值如何。

## 常见陷阱

### 1. 不验证输入

编码时最常见的错误之一是不验证输入。这可能会导致各种安全问题以及数据损坏。

始终验证输入很重要，即使它来自可信来源。

### 2.依赖客户端验证

另一个常见的错误是依赖客户端验证，例如 HTML5 表单验证。虽然客户端验证很有用，但绝不应将其用作唯一的验证方式。

这是因为恶意用户可以绕过客户端验证。因此，始终在服务器端验证输入也很重要。

### 3.只验证特定字符

验证输入时的一个常见陷阱是只检查特定字符，例如字母数字字符。但是，这可能会导致安全问题，因为恶意用户可以通过使用其他字符来绕过验证。

始终根据允许字符的白名单而不是禁止字符的黑名单来验证输入很重要。

### 4. 不清理输出

另一个常见的错误是忘记清理输出。这可能会导致安全问题，例如跨站点脚本 (XSS) 攻击。

在将输出显示给用户之前始终对输出进行清理很重要。

### 5. 对所有输入使用单个正则表达式

使用正则表达式 (regex) 进行输入验证时的一个常见错误是对所有输入使用单个正则表达式。但是，这可能会导致性能问题，因为需要为每个输入重新编译正则表达式。

最好为每个输入使用不同的正则表达式，或者预先编译正则表达式。

## 结论

输入验证是任何应用程序的关键部分。在本文中，我们介绍了 Kotlin 中输入验证的一些最佳实践，以及需要避免的一些常见陷阱。