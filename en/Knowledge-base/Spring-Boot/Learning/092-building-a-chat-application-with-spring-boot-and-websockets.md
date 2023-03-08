---
title: 092: Building a Chat Application with Spring Boot and WebSockets
description: 
published: true
date: 2023-02-05T22:32:35.685Z
tags: 
editor: markdown
dateCreated: 2023-02-05T22:32:30.227Z
---

- [092: Creación de una aplicación de chat con Spring Boot y WebSockets***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/092-building-a-chat-application-with-spring-boot-and-websockets)
{.links-list}
- [092：使用 Spring Boot 和 WebSockets 构建聊天应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/092-building-a-chat-application-with-spring-boot-and-websockets)
{.links-list}
- [092: Spring Boot와 WebSocket으로 채팅 애플리케이션 만들기***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/092-building-a-chat-application-with-spring-boot-and-websockets)
{.links-list}


# 092: Building a Chat Application with Spring Boot and WebSockets

In this post, we'll be looking at how to build a chat application with Spring Boot and WebSockets.

WebSockets are a bi-directional, full-duplex, persistent connection between a web browser and a server. They allow for real-time communication between the two.

Spring Boot is a Java-based framework that makes it easy to create stand-alone, production-grade Spring-based applications.

## Setting up the Project

We'll be using the Spring Initializr to set up our project. Go to https://start.spring.io/ and select the following:

* Web
* WebSocket
* Thymeleaf

Name the project "chat-application" and click "Generate Project."

## Dependencies

Spring Boot will automatically configure the necessary dependencies for our project.

## WebSockets

WebSockets are handled by a controller. In our project, we'll create a controller named `ChatController.java`.

```java
@Controller
public class ChatController {

    @MessageMapping("/chat")
    @SendTo("/topic/messages")
    public String sendMessage(String message) {
        return message;
    }
}
```

The `@MessageMapping` annotation maps a specific URL to the controller method. The `@SendTo` annotation specifies the URL of the WebSocket server endpoint. The message is then broadcasted to all the clients connected to that endpoint.

In our HTML file, we'll add a form with an input field and a submit button. The form will POST to the `/chat` endpoint.

```html
<form action="/chat" th:action="@{/chat}" th:object="${message}" method="post">
    <input type="text" th:field="*{text}"/>
    <input type="submit" value="Send"/>
</form>
```

The input field is bound to the `text` property of the `message` object. When the form is submitted, the `message` object is passed to the `sendMessage` method of the `ChatController` and the `text` property is used as the message to be broadcasted.

## Broadcasting Messages

We can use the `SimpMessagingTemplate` to broadcast messages to a specific destination.

```java
@Autowired
private SimpMessagingTemplate template;

@MessageMapping("/chat")
@SendTo("/topic/messages")
public String sendMessage(String message) {
    this.template.convertAndSend("/topic/messages", message);
    return message;
}
```

The `convertAndSend` method converts the message to JSON and sends it to the specified destination.

## Receiving Messages

We can use the `@SubscribeMapping` annotation to map a specific URL to a method. The method will be invoked when a client subscribes to the URL.

```java
@Controller
public class ChatController {

    @Autowired
    private SimpMessagingTemplate template;

    @MessageMapping("/chat")
    @SendTo("/topic/messages")
    public String sendMessage(String message) {
        this.template.convertAndSend("/topic/messages", message);
        return message;
    }

    @SubscribeMapping("/topic/messages")
    public List<String> subscribe() {
        List<String> messages = new ArrayList<>();
        messages.add("Hello");
        messages.add("Welcome");
        return messages;
    }
}
```

The `subscribe` method returns a list of messages that will be sent to the client when it subscribes to the `/topic/messages` destination.

## Testing the Application

We can test our application by running it and going to http://localhost:8080/. We should see the form and the list of messages.

We can also open the browser's developer tools and go to the Network tab. We should see the WebSocket connection being established.

## Conclusion

In this post, we've seen how to build a chat application with Spring Boot and WebSockets.