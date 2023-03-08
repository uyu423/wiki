---
title: 038：使用 Spring Boot 和 WebSockets 构建聊天应用程序
description: 
published: true
date: 2023-02-04T06:32:23.317Z
tags: 
editor: markdown
dateCreated: 2023-02-04T06:32:21.669Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [038: Building a chat application using Spring Boot and WebSockets***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/038-building-a-chat-application-using-spring-boot-and-websockets)
{.links-list}


# 038：使用 Spring Boot 和 WebSockets 构建聊天应用程序

WebSockets 是用于构建实时应用程序（例如聊天应用程序）的强大工具。在本文中，我们将向您展示如何使用 Spring Boot 和 WebSockets 构建聊天应用程序。

## 设置你的项目

首先，您需要创建一个新的 Spring Boot 项目。您可以使用 [Spring Initializr](https://start.spring.io/) 执行此操作。确保选择 Web 和 WebSocket 依赖项。

设置项目后，您需要将以下依赖项添加到 `pom.xml`：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-websocket</artifactId>
</dependency>
```

## 配置 WebSocket

接下来，您需要在 application.properties 文件中配置 WebSockets：

```properties
server.port=8080

spring.websocket.server.port=8081
spring.websocket.server.path=/ws
```

## 创建 WebSocket 端点

现在您已经设置了项目，您可以开始构建 WebSocket 端点。创建一个名为“ChatEndpoint”的新类，并用“@ServerEndpoint”对其进行注释。这个注解会告诉 Spring 这个类是一个 WebSocket 端点。

```java
@ServerEndpoint("/ws")
public class ChatEndpoint {

}
```

## 发送和接收消息

下一步是添加发送和接收消息的方法。 @OnMessage 注释将用于将方法标记为消息处理程序。每次在 WebSocket 端点上收到消息时都会调用此方法。

```java
@OnMessage
public void handleMessage(String message, Session session) {
    // do something with the message
}
```

要发送消息，您可以使用“Session.getBasicRemote().sendText(message)”方法。

```java
@OnMessage
public void handleMessage(String message, Session session) {
    session.getBasicRemote().sendText("Echo: " + message);
}
```

## 测试聊天应用程序

您可以使用 [WebSocket.org Echo Test](https://www.websocket.org/echo.html) 测试您的聊天应用程序。输入您的 WebSocket 端点 (ws://localhost:8081/ws) 并开始发送消息。您应该看到您发送的消息回显给您。

## 结论

在本文中，我们向您展示了如何使用 Spring Boot 和 WebSockets 构建聊天应用程序。 WebSockets 是用于构建实时应用程序的强大工具。