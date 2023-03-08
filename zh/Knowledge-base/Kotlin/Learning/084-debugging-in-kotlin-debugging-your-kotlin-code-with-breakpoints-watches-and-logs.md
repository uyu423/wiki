---
title: 084：在 Kotlin 中调试：使用断点、监视和日志调试 Kotlin 代码
description: 
published: true
date: 2023-02-14T22:17:16.470Z
tags: 
editor: markdown
dateCreated: 2023-02-14T22:17:14.486Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [084: Debugging in Kotlin: Debugging Your Kotlin Code with Breakpoints, Watches, and Logs***English** document is available*](/en/Knowledge-base/Kotlin/Learning/084-debugging-in-kotlin-debugging-your-kotlin-code-with-breakpoints-watches-and-logs)
{.links-list}


# 在 Kotlin 中调试：使用断点、监视和日志调试您的 Kotlin 代码

调试是任何开发人员的基本技能。它允许您查找并修复代码中的错误，以便您的程序正确运行。

Kotlin 是一种在 Java 虚拟机 (JVM) 上运行的编程语言。它是一种静态类型语言，旨在与 Java 互操作。 Kotlin 是一种简洁、安全且功能强大的语言，越来越受欢迎。

在本文中，我们将学习如何使用断点、监视和日志来调试 Kotlin 代码。我们还将了解调试 Kotlin 代码的一些最佳实践。

## 什么是断点？

断点是代码中的一个点，您的程序将在此处暂停执行。这使您可以检查程序的状态并查看发生了什么。断点对于调试非常有用，因为它们可以让您缩小代码中出现问题的范围。

有两种类型的断点：行断点和方法断点。行断点设置在特定的代码行上，当到达该行时将暂停程序的执行。方法断点设置在特定方法上，并会在调用该方法时暂停程序的执行。

您可以使用以下语法在 Kotlin 中设置断点：

```kotlin
val x = 5

x.setBreakpoint() // line breakpoint

fun foo() {
    // ...
}

foo.setBreakpoint() // method breakpoint
```

## 什么是手表？

监视是您在程序运行时监视的变量。您可以使用以下语法在 Kotlin 中设置监视：

```kotlin
val x = 5

x.watch() // watch x

fun foo() {
    // ...
}

foo.watch() // watch foo
```

## 什么是日志？

日志是您可以在程序运行时打印出来的消息。这对于调试很有用，因为您可以在特定时间点查看代码中发生的情况。您可以使用以下语法在 Kotlin 中设置日志：

```kotlin
val x = 5

x.log() // print x

fun foo() {
    // ...
}

foo.log() // print foo
```

## 调试 Kotlin 代码的最佳实践

以下是调试 Kotlin 代码的一些最佳实践：

- 使用断点缩小代码中问题所在的范围。
- 在程序运行时使用手表监视变量。
- 在程序运行时使用日志打印消息。
- 调试时要有耐心和有条不紊。这可能令人沮丧，但慢慢来，您最终会找到问题所在。

## 附加信息

- [Kotlin 调试文档](https://kotlinlang.org/docs/reference/debugging.html)
- [IntelliJ IDEA 调试文档](https://www.jetbrains.com/help/idea/debugging.html)
- [Eclipse 调试文档](https://help.eclipse.org/2018-09/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Fconcepts%2Fconcepts-debug.htm)