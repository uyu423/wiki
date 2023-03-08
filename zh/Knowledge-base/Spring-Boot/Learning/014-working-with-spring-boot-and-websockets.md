---
title: 014：使用 Spring Boot 和 WebSockets
description: 
published: true
date: 2023-02-03T09:18:03.826Z
tags: 
editor: markdown
dateCreated: 2023-02-03T09:17:58.706Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [014: Working with Spring Boot and WebSockets***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/014-working-with-spring-boot-and-websockets)
{.links-list}


# 014：使用 Spring Boot 和 WebSockets

WebSockets 是用于构建实时应用程序的强大工具。 Spring Boot 使使用 WebSockets 变得容易。在本文中，我们将学习如何使用 Spring Boot 和 WebSockets。

## 什么是 WebSocket？

WebSockets 是一种允许在客户端和服务器之间进行全双工通信的通信协议。这意味着客户端和服务器可以同时发送和接收数据。

WebSockets 是构建实时应用程序的好方法。它们快速、高效，并且允许您在数据可用时立即将数据推送到客户端。

## 设置Spring Boot

让我们从设置一个简单的 Spring Boot 应用程序开始。我们将使用 Spring Initializr 来创建我们的项目。

转到 Spring Initializr 网站 (https://start.spring.io/)。

选择以下选项：

- 项目：Maven 项目
- 语言：Java
- 春季启动版本：2.1.3
- 组：com.example
- 神器：websockets-demo

单击生成项目。

您现在应该有一个 zip 文件，其中包含您开始使用所需的一切。解压缩文件并在您喜欢的 IDE 中打开它。

## 创建 WebSocket 端点

让我们从创建一个简单的 WebSocket 端点开始。我们将使用@ServerEndpoint 注释来创建我们的端点。

在 com.example.websockets.demo 包中新建一个 Java 类，并将其命名为 MyWebSocketEndpoint.java。

将以下代码添加到 MyWebSocketEndpoint.java 文件中：

```java
@ServerEndpoint("/websocket")
public class MyWebSocketEndpoint {

}
```

@ServerEndpoint 注释用于创建 WebSocket 端点。注释的值是将用于访问端点的路径。

## 发送和接收消息

现在我们有了端点，让我们添加一些代码来发送和接收消息。

将以下代码添加到 MyWebSocketEndpoint.java 文件中：

```java
@ServerEndpoint("/websocket")
public class MyWebSocketEndpoint {

@OnOpen
public void onOpen(Session session) {
    // do something when the connection is opened
}

@OnMessage
public void onMessage(String message, Session session) {
    // do something when a message is received
}

@OnClose
public void onClose(Session session) {
    // do something when the connection is closed
}

@OnError
public void onError(Throwable error) {
    // do something when there is an error
}
}
```

@OnOpen 注释用于指定在打开连接时将调用的方法。 @OnMessage 注释用于指定在收到消息时将调用的方法。 @OnClose 注释用于指定关闭连接时将调用的方法。 @OnError 注解用于指定出现错误时将调用的方法。

## 配置端点

现在我们有了端点，让我们配置它。

将以下代码添加到 MyWebSocketEndpoint.java 文件中：

```java
@ServerEndpoint("/websocket")
public class MyWebSocketEndpoint {

@OnOpen
public void onOpen(Session session) {
    // do something when the connection is opened
}

@OnMessage
public void onMessage(String message, Session session) {
    // do something when a message is received
}

@OnClose
public void onClose(Session session) {
    // do something when the connection is closed
}

@OnError
public void onError(Throwable error) {
    // do something when there is an error
}
}
```

@ServerEndpoint 注释用于创建 WebSocket 端点。注释的值是将用于访问端点的路径。

@OnOpen 注释用于指定在打开连接时将调用的方法。 @OnMessage 注释用于指定在收到消息时将调用的方法。 @OnClose 注释用于指定关闭连接时将调用的方法。 @OnError 注解用于指定出现错误时将调用的方法。

## 测试端点

现在我们有了端点，让我们测试它。

在 com.example.websockets.demo 包中新建一个 Java 类，并将其命名为 MyWebSocketEndpointTest.java。

将以下代码添加到 MyWebSocketEndpointTest.java 文件：

```java
@Test
public void testMyWebSocketEndpoint() throws Exception {
    URI uri = new URI("ws://localhost:8080/websocket");
    WebSocketContainer container = ContainerProvider.getWebSocketContainer();
    Session session = container.connectToServer(MyWebSocketEndpoint.class, uri);
    session.getBasicRemote().sendText("Hello world!");
    session.close();
}
```

在 testMyWebSocketEndpoint() 方法中，我们为 WebSocket 端点创建一个 URI。然后我们创建一个 WebSocketContainer 并连接到我们的端点。我们向服务器发送一条消息，然后关闭连接。

如果运行测试，您应该会看到以下输出：

```
Hello world!
```

## 结论

在本文中，我们学习了如何使用 Spring Boot 和 WebSockets。我们创建了一个简单的 WebSocket 端点并对其进行了测试。