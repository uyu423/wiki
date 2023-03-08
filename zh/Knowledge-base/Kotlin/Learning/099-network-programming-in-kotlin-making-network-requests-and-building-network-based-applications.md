---
title: 099：Kotlin 中的网络编程：发出网络请求和构建基于网络的应用程序
description: 
published: true
date: 2023-02-16T09:17:45.664Z
tags: 
editor: markdown
dateCreated: 2023-02-16T09:17:43.381Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [099: Network Programming in Kotlin: Making Network Requests and Building Network-based Applications***English** document is available*](/en/Knowledge-base/Kotlin/Learning/099-network-programming-in-kotlin-making-network-requests-and-building-network-based-applications)
{.links-list}


# 099：Kotlin 中的网络编程：发出网络请求和构建基于网络的应用程序

Kotlin 是一种功能强大的编程语言，可用于构建各种应用程序，包括基于网络的应用程序。在本文中，我们将了解如何使用 Kotlin 发出网络请求和构建基于网络的应用程序。

## 发起网络请求

使用基于网络的应用程序时最常见的任务之一是发出网络请求。 Kotlin 使用内置的 [`HttpURLConnection`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/) 类可以轻松发出网络请求。

要发出网络请求，我们首先需要创建一个 HttpURLConnection 实例。我们可以通过传入我们想要请求的资源的 URL 来做到这一点：

```kotlin
val url = "https://www.example.com"
val connection = HttpURLConnection(url)
```

一旦我们有了 `HttpURLConnection` 实例，我们就可以使用 [`setRequestMethod`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/set-request- method.html) 方法来设置请求方法。请求方法确定将对资源采取的操作类型。最常见的请求方法是“GET”、“POST”、“PUT”和“DELETE”。

```kotlin
connection.setRequestMethod("GET")
```

我们也可以使用 [`setRequestProperty`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/set-request-property.html) 方法来设置请求标题。请求标头用于提供有关请求的附加信息，例如请求的内容类型。

```kotlin
connection.setRequestProperty("Content-Type", "application/json")
```

一旦我们配置了 `HttpURLConnection` 实例，我们就可以使用 [`getInputStream`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/get-input -stream.html) 方法获取连接的输入流。输入流可用于读取来自服务器的响应。

```kotlin
val inputStream = connection.getInputStream()
```

## 构建基于网络的应用程序

除了发出网络请求，Kotlin 还可以用来构建基于网络的应用程序。 Kotlin 提供了一个 [`Socket`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/) 类，可用于创建基于套接字的应用程序。

要创建基于套接字的应用程序，我们首先需要创建一个 `Socket` 实例。我们可以通过传入要连接的服务器的主机名和端口号来完成此操作：

```kotlin
val socket = Socket("www.example.com", 80)
```

一旦我们有了一个 `Socket` 实例，我们就可以使用 [`getInputStream`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/get-input-stream.html)和 [`getOutputStream`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/get-output-stream.html) 方法来获取套接字的输入和输出流。这些流可用于通过套接字连接发送和接收数据。

```kotlin
val inputStream = socket.getInputStream()
val outputStream = socket.getOutputStream()
```

一旦我们有了输入和输出流，我们就可以使用 [`write`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-output-stream/write.html) 和 [ `read`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-input-stream/read.html) 通过套接字连接发送和接收数据的方法。

```kotlin
outputStream.write("Hello, world!".toByteArray())

val response = inputStream.read()
```

最后，我们可以使用 [`close`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/close.html) 方法关闭套接字连接。

```kotlin
socket.close()
```

## 结论

在本文中，我们了解了如何使用 Kotlin 发出网络请求和构建基于网络的应用程序。 Kotlin 对网络编程的支持使其成为构建各种应用程序的绝佳选择。