---
title: 057：Kotlin 中的异常处理：处理错误和异常
description: 
published: true
date: 2023-02-01T16:23:24.557Z
tags: 
editor: markdown
dateCreated: 2023-02-01T16:23:22.984Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [057: Exception Handling in Kotlin: Dealing with Errors and Exceptions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/057-exception-handling-in-kotlin-dealing-with-errors-and-exceptions)
{.links-list}


# Kotlin 异常处理

异常是在程序执行期间发生的中断正常指令流的事件。 Kotlin 提供了强大的异常处理机制。在本文中，我们将了解如何在 Kotlin 中处理异常。

## 什么是异常？

异常是在程序执行期间发生的中断正常指令流的事件。当异常发生时，程序突然终止。

有两种类型的异常：已检查和未检查。已检查异常是在编译时发生的异常，例如未找到文件时。未经检查的异常是在运行时发生的异常，例如发生被零除错误时。

## 处理异常

Kotlin 提供了强大的异常处理机制。 try/catch 块用于处理异常。 try 块包含可能抛出异常的代码。 catch 块包含处理异常的代码。

```kotlin
try {
   // code that may throw an exception
} catch (e: Exception) {
   // code that handles the exception
}
```

如果 try 块中发生异常，则执行 catch 块。如果没有异常发生，则跳过 catch 块。

也可以有多个 catch 块来处理不同类型的异常。

```kotlin
try {
   // code that may throw an exception
} catch (e: FileNotFoundException) {
   // code that handles the FileNotFoundException
} catch (e: IOException) {
   // code that handles the IOException
}
```

## 最后阻止

finally 块是可选的。无论是否发生异常都会执行。

```kotlin
try {
   // code that may throw an exception
} catch (e: Exception) {
   // code that handles the exception
} finally {
   // code that is always executed
}
```

## 抛出异常

可以使用 throw 关键字显式抛出异常。

```kotlin
throw FileNotFoundException()
```

## 创建自定义异常

可以通过扩展 Exception 类来创建自定义异常。

```kotlin
class MyException: Exception() {
}
```

## 资源

- [Kotlin 文档 - 异常处理](https://kotlinlang.org/docs/reference/exceptions.html)
- [JavaWorld - Kotlin 中的异常处理](https://www.javaworld.com/article/3240006/learn-java/exception-handling-in-kotlin.html)
- [Stack Overflow - 如何在 Kotlin 中创建自定义异常？](https://stackoverflow.com/questions/44487193/how-do-i-create-a-custom-exception-in-kotlin)