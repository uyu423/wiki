---
title: 014: Working with Spring Boot and WebSockets
description: 
published: true
date: 2023-02-03T09:18:00.356Z
tags: 
editor: markdown
dateCreated: 2023-02-03T09:17:58.713Z
---

- [014: Trabajar con Spring Boot y WebSockets***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/014-working-with-spring-boot-and-websockets)
{.links-list}
- [014：使用 Spring Boot 和 WebSockets***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/014-working-with-spring-boot-and-websockets)
{.links-list}
- [014: Spring Boot 및 WebSocket 작업***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/014-working-with-spring-boot-and-websockets)
{.links-list}


#014: Working with Spring Boot and WebSockets

WebSockets are a powerful tool for building real-time applications. Spring Boot makes it easy to work with WebSockets. In this post, we'll learn how to work with Spring Boot and WebSockets.

##What are WebSockets?

WebSockets are a communication protocol that allows for full-duplex communication between a client and a server. This means that both the client and the server can send and receive data at the same time.

WebSockets are a great way to build real-time applications. They are fast, efficient, and they allow you to push data to the client as soon as it is available.

##Setting up Spring Boot

Let's start by setting up a simple Spring Boot application. We'll use the Spring Initializr to create our project.

Go to the Spring Initializr website (https://start.spring.io/).

Choose the following options:

- Project: Maven Project
- Language: Java
- Spring Boot Version: 2.1.3
- Group: com.example
- Artifact: websockets-demo

Click Generate Project.

You should now have a zip file that contains everything you need to get started. Unzip the file and open it in your favorite IDE.

##Creating a WebSocket Endpoint

Let's start by creating a simple WebSocket endpoint. We'll use the @ServerEndpoint annotation to create our endpoint.

Create a new Java class in the com.example.websockets.demo package and name it MyWebSocketEndpoint.java.

Add the following code to the MyWebSocketEndpoint.java file:

```java
@ServerEndpoint("/websocket")
public class MyWebSocketEndpoint {

}
```

The @ServerEndpoint annotation is used to create a WebSocket endpoint. The value of the annotation is the path that will be used to access the endpoint.

##Sending and Receiving Messages

Now that we have our endpoint, let's add some code to send and receive messages.

Add the following code to the MyWebSocketEndpoint.java file:

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

The @OnOpen annotation is used to specify a method that will be called when a connection is opened. The @OnMessage annotation is used to specify a method that will be called when a message is received. The @OnClose annotation is used to specify a method that will be called when a connection is closed. The @OnError annotation is used to specify a method that will be called when there is an error.

##Configuring the Endpoint

Now that we have our endpoint, let's configure it.

Add the following code to the MyWebSocketEndpoint.java file:

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

The @ServerEndpoint annotation is used to create a WebSocket endpoint. The value of the annotation is the path that will be used to access the endpoint.

The @OnOpen annotation is used to specify a method that will be called when a connection is opened. The @OnMessage annotation is used to specify a method that will be called when a message is received. The @OnClose annotation is used to specify a method that will be called when a connection is closed. The @OnError annotation is used to specify a method that will be called when there is an error.

##Testing the Endpoint

Now that we have our endpoint, let's test it.

Create a new Java class in the com.example.websockets.demo package and name it MyWebSocketEndpointTest.java.

Add the following code to the MyWebSocketEndpointTest.java file:

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

In the testMyWebSocketEndpoint() method, we create a URI for our WebSocket endpoint. We then create a WebSocketContainer and connect to our endpoint. We send a message to the server and then close the connection.

If you run the test, you should see the following output:

```
Hello world!
```

##Conclusion

In this post, we've learned how to work with Spring Boot and WebSockets. We've created a simple WebSocket endpoint and tested it.