---
title: 用于异步服务器端开发的 Kotlin 协程
description: 
published: true
date: 2023-02-04T10:17:45.250Z
tags: 
editor: markdown
dateCreated: 2023-02-04T10:17:43.635Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kotlin Coroutines for Asynchronous Server-side Development***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-coroutines-for-asynchronous-server-side-development)
{.links-list}


# 用于异步服务器端开发的 Kotlin 协程

Kotlin 协程提供了一种在服务器端管理并发的有效方法。通过使用协程，开发人员可以编写更能响应用户输入的代码，同时仍能提供丰富的用户体验。

协程是在 Kotlin 1.1 中引入的，自 Kotlin 1.3 以来一直是一个稳定的特性。在协程上下文中，协程是一个轻量级线程，可用于从主线程卸载工作。这允许开发人员编写更能响应用户输入的代码，同时仍提供丰富的用户体验。

协程可以与任何现有的 Java 库一起使用，使它们成为异步服务器端开发的绝佳工具。在本文中，我们将了解如何在 Java Web 应用程序中使用协程。

## 设置项目

我们将从设置一个简单的 Maven 项目开始。将以下依赖项添加到您的 `pom.xml`：

```xml
<dependencies>
    <dependency>
        <groupId>org.jetbrains.kotlin</groupId>
        <artifactId>kotlin-stdlib-jdk8</artifactId>
        <version>1.3.72</version>
    </dependency>
    <dependency>
        <groupId>org.jetbrains.kotlinx</groupId>
        <artifactId>kotlinx-coroutines-core</artifactId>
        <version>1.3.7</version>
    </dependency>
</dependencies>
```

我们正在使用 Kotlin 1.3.72 和 Kotlinx Coroutines 1.3.7。 “kotlin-stdlib-jdk8”依赖项包括 Kotlin 标准库，而“kotlinx-coroutines-core”依赖项提供核心协程功能。

## 创建协程

可以使用 `kotlinx.coroutines` 包中的 `launch` 或 `async` 函数创建协程。 `launch` 函数创建一个新协程并立即启动它。 `async` 函数创建一个新协程，但不会立即启动它。相反，它返回一个 Deferred 类的实例，稍后可用于启动协程。

例如，我们可以使用 `launch` 函数创建一个休眠一秒钟的协程：

```kotlin
import kotlinx.coroutines.*

fun main() {
    launch {
        // Suspend this coroutine for one second
        delay(1000)
        println("Hello, world!")
    }
}
```

我们还可以使用 `async` 函数创建协程：

```kotlin
import kotlinx.coroutines.*

fun main() {
    val deferred = async {
        // Suspend this coroutine for one second
        delay(1000)
        println("Hello, world!")
    }
    // Start the coroutine
    deferred.start()
}
```

`launch` 函数是一个挂起函数，这意味着它可以在另一个协程中使用。 `async` 函数不是挂起函数，因此只能在协程中使用。

## 取消协程

可以使用 `cancel` 函数取消协程。此函数将导致协程抛出“CancellationException”。

例如，我们可以使用 `cancel` 函数取消休眠一秒的协程：

```kotlin
import kotlinx.coroutines.*

fun main() {
    val deferred = launch {
        try {
            // Suspend this coroutine for one second
            delay(1000)
            println("Hello, world!")
        } catch (e: CancellationException) {
            println("Coroutine was cancelled")
        }
    }
    // Cancel the coroutine after half a second
    delay(500)
    deferred.cancel()
}
```

## 超时

协程可以使用 `withTimeout` 函数超时。如果未在指定时间内完成，此函数将导致协程抛出“TimeoutCancellationException”。

例如，我们可以使用 `withTimeout` 函数使正在休眠一秒钟的协程超时：

```kotlin
import kotlinx.coroutines.*

fun main() {
    try {
        withTimeout(500) {
            // Suspend this coroutine for one second
            delay(1000)
            println("Hello, world!")
        }
    } catch (e: TimeoutCancellationException) {
        println("Coroutine timed out")
    }
}
```

## 异常处理

协程可以使用 supervisorScope 函数进行监督。该函数将捕获协程抛出的任何异常，并继续执行剩余的代码。

例如，我们可以使用 supervisorScope 函数监督一个休眠了一秒钟的协程：

```kotlin
import kotlinx.coroutines.*

fun main() {
    supervisorScope {
        val deferred = launch {
            // Suspend this coroutine for one second
            delay(1000)
            println("Hello, world!")
        }
        // Cancel the coroutine after half a second
        delay(500)
        deferred.cancel()
    }
}
```

## 异步 Web 应用程序

协程可用于编写异步 Web 应用程序。在本节中，我们将了解如何在 Java Web 应用程序中使用协程。

我们将从创建一个简单的 servlet 开始，它使用协程休眠一秒钟：

```java
@WebServlet("/sleep")
public class SleepServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // Create a new coroutine
        launch {
            // Suspend this coroutine for one second
            delay(1000)
            // Send a response to the client
            resp.getWriter().println("Hello, world!");
        }
    }
}
```

在这个 servlet 中，我们使用 `launch` 函数来创建一个新的协程。这个协程休眠一秒钟，然后向客户端发送响应。

我们还可以使用 `async` 函数来创建一个新的协程。但是，在这种情况下，我们需要手动启动协程：

```java
@WebServlet("/sleep")
public class SleepServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // Create a new coroutine
        val deferred = async {
            // Suspend this coroutine for one second
            delay(1000)
            // Send a response to the client
            resp.getWriter().println("Hello, world!");
        }
        // Start the coroutine
        deferred.start()
    }
}
```

在这个 servlet 中，我们使用 `async` 函数来创建一个新的协程。这个协程休眠一秒钟，然后向客户端发送响应。我们使用 `start` 函数来启动协程。

也可以使用 `withTimeout` 函数使协程超时：

```java
@WebServlet("/sleep")
public class SleepServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        try {
            // Time out the coroutine after 500 milliseconds
            withTimeout(500) {
                // Create a new coroutine
                launch {
                    // Suspend this coroutine for one second
                    delay(1000)
                    // Send a response to the client
                    resp.getWriter().println("Hello, world!");
                }
            }
        } catch (e: TimeoutCancellationException) {
            // Send a timeout response to the client
            resp.getWriter().println("Request timed out");
        }
    }
}
```

在这个 servlet 中，我们使用 `withTimeout` 函数使协程超时。如果协程在 500 毫秒内没有完成，它将被取消并向客户端发送超时响应。

也可以使用 `supervisorScope` 函数来监督协程：

```java
@WebServlet("/sleep")
public class SleepServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // Supervisor the coroutine
        supervisorScope {
            val deferred = launch {
                // Suspend this coroutine for one second
                delay(1000)
                // Send a response to the client
                resp.getWriter().println("Hello, world!");
            }
            // Cancel the coroutine after half a second
            delay(500)
            deferred.cancel()
        }
    }
}
```

在这个 servlet 中，我们使用 `supervisorScope` 函数来监督协程。半秒后该协程被取消，但执行 servlet 中的剩余代码。

## 结论

Kotlin 协程提供了一种在服务器端管理并发的有效方法。它们可以与任何现有的 Java 库一起使用，使它们成为异步服务器端开发的绝佳工具。