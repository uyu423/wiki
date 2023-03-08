---
title: 038: Building a chat application using Spring Boot and WebSockets
description: 
published: true
date: 2023-02-04T06:32:27.082Z
tags: 
editor: markdown
dateCreated: 2023-02-04T06:32:21.672Z
---

- [038: Creación de una aplicación de chat con Spring Boot y WebSockets***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/038-building-a-chat-application-using-spring-boot-and-websockets)
{.links-list}
- [038：使用 Spring Boot 和 WebSockets 构建聊天应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/038-building-a-chat-application-using-spring-boot-and-websockets)
{.links-list}
- [038: Spring Boot와 WebSocket을 사용하여 채팅 애플리케이션 만들기***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/038-building-a-chat-application-using-spring-boot-and-websockets)
{.links-list}


# 038: Building a chat application using Spring Boot and WebSockets

WebSockets are a powerful tool for building real-time applications, such as chat applications. In this post, we'll show you how to build a chat application using Spring Boot and WebSockets.

## Setting up your project

To get started, you'll need to create a new Spring Boot project. You can do this using the [Spring Initializr](https://start.spring.io/). Make sure to select the Web and WebSocket dependencies.

Once you have your project set up, you'll need to add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-websocket</artifactId>
</dependency>
```

## Configuring WebSockets

Next, you'll need to configure WebSockets in your `application.properties` file:

```properties
server.port=8080

spring.websocket.server.port=8081
spring.websocket.server.path=/ws
```

## Creating the WebSocket endpoint

Now that you have your project set up, you can start building the WebSocket endpoint. Create a new class called `ChatEndpoint` and annotate it with `@ServerEndpoint`. This annotation will tell Spring that this class is a WebSocket endpoint.

```java
@ServerEndpoint("/ws")
public class ChatEndpoint {

}
```

## Sending and receiving messages

The next step is to add methods for sending and receiving messages. The `@OnMessage` annotation will be used to mark a method as a message handler. This method will be called every time a message is received on the WebSocket endpoint.

```java
@OnMessage
public void handleMessage(String message, Session session) {
    // do something with the message
}
```

To send a message, you can use the `Session.getBasicRemote().sendText(message)` method.

```java
@OnMessage
public void handleMessage(String message, Session session) {
    session.getBasicRemote().sendText("Echo: " + message);
}
```

## Testing the chat application

You can test your chat application using the [WebSocket.org Echo Test](https://www.websocket.org/echo.html). Enter your WebSocket endpoint (ws://localhost:8081/ws) and start sending messages. You should see the messages you send echoed back to you.

## Conclusion

In this post, we've shown you how to build a chat application using Spring Boot and WebSockets. WebSockets are a powerful tool for building real-time applications.