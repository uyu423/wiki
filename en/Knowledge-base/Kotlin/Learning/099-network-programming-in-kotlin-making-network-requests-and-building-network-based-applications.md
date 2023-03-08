---
title: 099: Network Programming in Kotlin: Making Network Requests and Building Network-based Applications
description: 
published: true
date: 2023-02-16T09:17:51.660Z
tags: 
editor: markdown
dateCreated: 2023-02-16T09:17:43.386Z
---

- [099: Programación de red en Kotlin: Realización de solicitudes de red y creación de aplicaciones basadas en red***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/099-network-programming-in-kotlin-making-network-requests-and-building-network-based-applications)
{.links-list}
- [099：Kotlin 中的网络编程：发出网络请求和构建基于网络的应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/099-network-programming-in-kotlin-making-network-requests-and-building-network-based-applications)
{.links-list}
- [099: Kotlin의 네트워크 프로그래밍: 네트워크 요청 및 네트워크 기반 애플리케이션 구축***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/099-network-programming-in-kotlin-making-network-requests-and-building-network-based-applications)
{.links-list}


# 099: Network Programming in Kotlin: Making Network Requests and Building Network-based Applications

Kotlin is a powerful programming language that can be used to build a variety of applications, including network-based applications. In this post, we'll take a look at how to use Kotlin to make network requests and build network-based applications.

## Making Network Requests

One of the most common tasks when working with network-based applications is making network requests. Kotlin makes it easy to make network requests using the built-in [`HttpURLConnection`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/) class.

To make a network request, we first need to create a `HttpURLConnection` instance. We can do this by passing in the URL of the resource we want to request:

```kotlin
val url = "https://www.example.com"
val connection = HttpURLConnection(url)
```

Once we have a `HttpURLConnection` instance, we can use the [`setRequestMethod`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/set-request-method.html) method to set the request method. The request method determines the type of action that will be taken on the resource. The most common request methods are `GET`, `POST`, `PUT`, and `DELETE`.

```kotlin
connection.setRequestMethod("GET")
```

We can also use the [`setRequestProperty`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/set-request-property.html) method to set request headers. Request headers are used to provide additional information about the request, such as the type of content that is being requested.

```kotlin
connection.setRequestProperty("Content-Type", "application/json")
```

Once we have configured the `HttpURLConnection` instance, we can use the [`getInputStream`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/get-input-stream.html) method to get the input stream for the connection. The input stream can be used to read the response from the server.

```kotlin
val inputStream = connection.getInputStream()
```

## Building Network-based Applications

In addition to making network requests, Kotlin can also be used to build network-based applications. Kotlin provides a [`Socket`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/) class that can be used to create socket-based applications.

To create a socket-based application, we first need to create a `Socket` instance. We can do this by passing in the hostname and port number of the server we want to connect to:

```kotlin
val socket = Socket("www.example.com", 80)
```

Once we have a `Socket` instance, we can use the [`getInputStream`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/get-input-stream.html) and [`getOutputStream`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/get-output-stream.html) methods to get the input and output streams for the socket. These streams can be used to send and receive data over the socket connection.

```kotlin
val inputStream = socket.getInputStream()
val outputStream = socket.getOutputStream()
```

Once we have the input and output streams, we can use the [`write`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-output-stream/write.html) and [`read`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-input-stream/read.html) methods to send and receive data over the socket connection.

```kotlin
outputStream.write("Hello, world!".toByteArray())

val response = inputStream.read()
```

Finally, we can use the [`close`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/close.html) method to close the socket connection.

```kotlin
socket.close()
```

## Conclusion

In this post, we've taken a look at how to use Kotlin to make network requests and build network-based applications. Kotlin's support for network programming makes it a great choice for building a variety of applications.