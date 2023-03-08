---
title: 056：Kotlin 中的 When 表达式：综合指南
description: 
published: true
date: 2023-02-16T19:17:32.115Z
tags: 
editor: markdown
dateCreated: 2023-02-16T19:17:30.009Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [056: The When Expression in Kotlin: A Comprehensive Guide***English** document is available*](/en/Knowledge-base/Kotlin/Learning/056-the-when-expression-in-kotlin-a-comprehensive-guide)
{.links-list}


## 介绍

Kotlin 的 when 表达式是一个强大的工具，可以用来匹配各种不同类型的数据。在本指南中，我们将了解如何在 Kotlin 中使用 when 表达式并探索其一些更高级的功能。

## 基本用法

when 表达式在 Kotlin 中相当于其他语言中的 switch 语句。它允许您匹配一个值并根据该值执行一段代码。

这是一个简单的例子：

```kotlin
when (x) {
    1 -> println("x is 1")
    2 -> println("x is 2")
    else -> println("x is neither 1 nor 2")
}
```

在这个例子中，我们匹配变量“x”的值。如果 `x` 等于 `1`，将执行与该情况关联的代码块。同样，如果 `x` 等于 `2`，则将执行与该情况关联的代码块。如果 `x` 既不是 1 也不是 2 ，则将执行与 else 情况关联的代码块。

重要的是要注意 `else` 的情况不是必需的。如果省略 else 情况，则 when 表达式将不会匹配其他情况中未明确列出的任何值：

```kotlin
when (x) {
    1 -> println("x is 1")
    2 -> println("x is 2")
}
```

在此示例中，如果“x”既不是“1”也不是“2”，则不会执行与“else”情况关联的代码块。

## 类型匹配

除了匹配值之外，when 表达式还可以用于匹配类型。这在处理可空类型时特别有用。

考虑以下示例：

```kotlin
fun process(value: Any) {
    when (value) {
        is String -> println(value.length)
        is Int -> println(value * 2)
        else -> println("I don't know what this is")
    }
}
```

在此示例中，我们有一个函数接受“Any”类型并以某种方式处理它。我们使用 when 表达式来匹配 `value` 参数的类型。

如果 `value` 是一个 `String`，我们打印出它的长度。如果 `value` 是 `Int`，我们打印它的值乘以 2。如果 `value` 既不是 `String` 也不是 `Int`，我们打印一条消息说我们不知道它是什么.

您还可以使用 when 表达式来匹配可为 null 的类型。这对于避免可怕的“NullPointerException”非常有用。

考虑以下示例：

```kotlin
fun process(value: Any?) {
    when (value) {
        is String -> println(value.length)
        is Int -> println(value * 2)
        null -> println("value is null")
        else -> println("I don't know what this is")
    }
}
```

在此示例中，我们已将“value”参数的类型从“Any”更改为“Any?”。这使得参数可以为空，这意味着它现在可以取值“null”。

我们在 when 表达式中添加了一个 case 来处理“null”值。如果 `value` 为 `null`，我们会打印出一条消息说明这一点。

重要的是要注意“null” case 必须在“else” case 之前。这是因为“else”大小写将匹配任何值，包括“null”。

如果 `null` 情况发生在 `else` 情况之后，它永远不会被执行。

## 结论

在本指南中，我们了解了如何在 Kotlin 中使用 when 表达式。我们已经了解了如何匹配值和类型，还了解了如何处理可空类型。