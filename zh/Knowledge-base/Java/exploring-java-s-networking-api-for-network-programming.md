---
title: 探索用于网络编程的 Java 网络 API
description: 
published: true
date: 2023-01-31T04:23:51.480Z
tags: 
editor: markdown
dateCreated: 2023-01-31T04:23:49.860Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Exploring Java's Networking API for Network Programming***English** version of this document is available*](/en/Knowledge-base/Java/exploring-java-s-networking-api-for-network-programming)
{.links-list}

    
Java 编程一直具有强大的网络组件。它是一种通用语言，可用于开发范围广泛的应用程序，从桌面到 Web 再到移动。 Java 平台具有广泛的网络类和接口库，可提供网络编程所需的所有功能。

在本文中，我们将探讨 Java 网络 API 以及可以使用它实现的一些常见网络场景。我们还将了解一些可用的更高级的功能。

Java 平台的网络 API 基于请求/响应模型。客户端发出请求，服务器响应。客户端和服务器可以在同一台机器上，也可以在不同的机器上。请求和响应可以是任何格式，但最常见的格式是 HTTP。

HTTP 是万维网使用的格式。它是一个简单的、基于文本的协议，建立在 TCP/IP 协议之上。 HTTP 是无状态的，这意味着每个请求都独立于任何其他请求。这使它成为 Web 应用程序的一种非常有效的协议。

Java 平台的网络 API 包括一组提供网络编程所需的低级功能的类和接口。 java.net 包包含核心网络类和接口。 javax.net 包包含对核心网络类和接口的扩展。

java.net.URL 类是 Java 平台网络 API 的网关。它代表一个统一资源定位符，这是一种在 Internet 上识别资源的方法。资源可以是网页、图像、文件或任何其他可以通过 URL 识别的内容。

java.net.URL 类有许多用于读取数据和将数据写入 URL 的方法。下面列出了最常用的方法。

- 获取内容()
- 打开连接（）
- 开放流（）
- 获取输入流()

getContent() 方法返回一个表示 URL 内容的对象。 openConnection() 方法返回一个 URLConnection 对象，它表示到 URL 的连接。 openStream() 方法返回一个 InputStream，可用于从 URL 中读取数据。 getInputStream() 方法返回可用于从 URL 读取数据的 InputStream。

java.net.URLConnection 类表示到 URL 的连接。它可用于打开连接并从 URL 读取数据。 URLConnection 类有许多用于读取数据和将数据写入 URL 的方法。下面列出了最常用的方法。

- 获取内容()
- 获取输入流()
- 获取输出流()
- setDoInput()
- setDoOutput()
- 连接（）

getContent() 方法返回一个表示 URL 内容的对象。 getInputStream() 方法返回一个 InputStream，可用于从 URL 中读取数据。 getOutputStream() 方法返回一个 OutputStream，可用于将数据写入 URL。 setDoInput() 方法设置是否应该将 URLConnection 用于输入。 setDoOutput() 方法设置是否应该将 URLConnection 用于输出。 connect() 方法打开到 URL 的连接。

java.net.Socket 类表示一个套接字，它是两台计算机之间的通信端点。套接字可用于读取和写入数据。下面列出了最常用的方法。

- 获取输入流()
- 获取输出流()
- 关闭（）

getInputStream() 方法返回一个 InputStream，可用于从 Socket 读取数据。 getOutputStream() 方法返回一个OutputStream，可用于向Socket 写入数据。 close() 方法关闭套接字。

java.net.ServerSocket 类表示服务器套接字，它是服务器的通信端点。 ServerSocket 可用于接受来自客户端的传入连接。下面列出了最常用的方法。

- 接受（）
- 关闭（）

accept() 方法接受来自客户端的传入连接。 close() 方法关闭 ServerSocket。

为了使用 Java 平台的网络 API，您必须对 TCP/IP 协议有基本的了解。 TCP/IP 是用于在 Internet 上的计算机之间进行通信的协议。它是一个由两部分组成的协议，由传输控制协议 (TCP) 和互联网协议 (IP) 组成。

传输控制协议 (TCP) 负责确保数据以正确的顺序正确传送。它通过在两台计算机之间建立连接然后以小数据包发送数据来实现这一点。然后在目的地将数据包重新组合成正确的顺序。

互联网协议 (IP) 负责将数据包从源路由到目的地。它通过使用一组称为路由表的规则来做到这一点。

Java 平台的网络 API 包括一组提供网络编程所需的低级功能的类和接口。 java.net 包包含核心网络类和接口。 javax.net 包包含对核心网络类和接口的扩展。

java.net.URL 类是 Java 平台网络 API 的网关。它代表一个统一资源定位符，这是一种在 Internet 上识别资源的方法。资源可以是网页、图像、文件或任何其他可以通过 URL 识别的内容。

java.net.URL 类有许多用于读取数据和将数据写入 URL 的方法。下面列出了最常用的方法。

- 获取内容()
- 打开连接（）
- 开放流（）
- 获取输入流()

getContent() 方法返回一个表示 URL 内容的对象。 openConnection() 方法返回一个 URLConnection 对象，它表示到 URL 的连接。 openStream() 方法返回一个 InputStream，可用于从 URL 中读取数据。 getInputStream() 方法返回可用于从 URL 读取数据的 InputStream。

java.net.URLConnection 类表示到 URL 的连接。它可用于打开连接并从 URL 读取数据。 URLConnection 类有许多用于读取数据和将数据写入 URL 的方法。下面列出了最常用的方法。

- 获取内容()
- 获取输入流()
- 获取输出流()
- setDoInput()
- setDoOutput()
- 连接（）

getContent() 方法返回一个表示 URL 内容的对象。 getInputStream() 方法返回一个 InputStream，可用于从 URL 中读取数据。 getOutputStream() 方法返回一个 OutputStream，可用于将数据写入 URL。 setDoInput() 方法设置是否应该将 URLConnection 用于输入。 setDoOutput() 方法设置是否应该将 URLConnection 用于输出。 connect() 方法打开到 URL 的连接。

java.net.Socket 类表示一个套接字，它是两台计算机之间的通信端点。套接字可用于读取和写入数据。下面列出了最常用的方法。

- 获取输入流()
- 获取输出流()
- 关闭（）

getInputStream() 方法返回一个 InputStream，可用于从 Socket 读取数据。 getOutputStream() 方法返回一个OutputStream，可用于向Socket 写入数据。 close() 方法关闭套接字。

java.net.ServerSocket 类表示服务器套接字，它是服务器的通信端点。 ServerSocket 可用于接受来自客户端的传入连接。下面列出了最常用的方法。

- 接受（）
- 关闭（）

accept() 方法接受来自客户端的传入连接。 close() 方法关闭 ServerSocket。

java.net.DatagramSocket 类表示数据报套接字，它是发送和接收数据报的通信端点。数据报是一种小型的独立消息，无需长期连接即可发送。下面列出了最常用的方法。

- 发送（）
- 收到（）
- 关闭（）

send() 方法发送数据报。 receive() 方法接收数据报。 close() 方法关闭 DatagramSocket。

java.net.DatagramPacket 类表示一个数据报包，它是一种小型的独立消息，无需长期连接即可发送。下面列出了最常用的方法。

- 获取数据()
- 获取长度（）
- 获取地址()
- 获取端口()

getData() 方法返回包中包含的数据。 getLength() 方法返回数据包中包含的数据的长度。 getAddress() 方法返回发件人的地址。 getPort() 方法返回发送者的端口。

Java 编程一直具有强大的网络组件。它是一种通用语言，可用于开发范围广泛的应用程序，从桌面到 Web 再到移动。 Java 平台具有广泛的网络类和接口库，可提供网络编程所需的所有功能。

在本文中，我们探索了 Java 网络 API 和一些可以使用它实现的常见网络场景。我们还研究了一些可用的更高级的功能。