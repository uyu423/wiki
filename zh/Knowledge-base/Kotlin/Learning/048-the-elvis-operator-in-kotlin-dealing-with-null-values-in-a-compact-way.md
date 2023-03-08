---
title: 048：Kotlin 中的猫王运算符：以紧凑的方式处理空值
description: 
published: true
date: 2023-02-02T09:57:28.106Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:57:26.489Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [048: The Elvis Operator in Kotlin: Dealing with Null Values in a Compact Way***English** document is available*](/en/Knowledge-base/Kotlin/Learning/048-the-elvis-operator-in-kotlin-dealing-with-null-values-in-a-compact-way)
{.links-list}


# Kotlin 中的猫王运算符：以紧凑的方式处理空值

在任何编程语言中处理空值都是一件痛苦的事情。在 Kotlin 中，Elvis 运算符提供了一种简洁且安全的方式来处理空值。

## 什么是猫王运算符？

Elvis 运算符是一个空安全运算符，它返回其操作数的非空值，如果操作数为空，则返回默认值。 Elvis算子的写法如下：

```kotlin
val result = operand ?: defaultValue
```

如果操作数不为空，则 Elvis 运算符返回它。如果操作数为空，则 Elvis 运算符返回默认值。

## Elvis Operator 是如何工作的？

Elvis 运算符由两部分组成：空安全运算符 (`?.`) 和 Elvis 运算符 (`?:`)。

空安全运算符 (`?.`) 用于安全地访问可为空对象的成员。如果对象为 null，则 null 安全运算符返回 null 而不是抛出 NullPointerException。

Elvis 运算符 (`?:`) 用于在操作数为空时提供默认值。

## 何时使用 Elvis 运算符

Elvis 运算符最常用于以简洁和安全的方式处理空值。

例如，考虑以下代码：

```kotlin
val list: List<String>? = null

val firstItem = list?.get(0) ?: "Default Value"
```

在此代码中，“list”变量可以为空。如果 `list` 为 null，则 `firstItem` 变量将设置为默认值（“默认值”）。如果 `list` 不为空，则 `firstItem` 变量将设置为列表中的第一项。

## 附加信息

以下是一些额外的资源，可用于了解有关 Elvis 运算符的更多信息：

- [Kotlin 文档 - 猫王运算符](https://kotlinlang.org/docs/reference/null-safety.html# the-elvis-operator)
- [Kotlin Academy - 空安全和 Elvis 运算符](https://kotlinacademy.com/kotlin-null-safety-elvis-operator/)
- [Android 开发者 - 在 Kotlin 中处理 null](https://developer.android.com/kotlin/null-safety)