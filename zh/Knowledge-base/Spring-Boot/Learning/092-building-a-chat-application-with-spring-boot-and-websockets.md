---
title: 092：使用 Spring Boot 和 WebSockets 构建聊天应用程序
description: 
published: true
date: 2023-02-05T22:32:31.907Z
tags: 
editor: markdown
dateCreated: 2023-02-05T22:32:30.220Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [092: Building a Chat Application with Spring Boot and WebSockets***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/092-building-a-chat-application-with-spring-boot-and-websockets)
{.links-list}


# 092：使用 Spring Boot 和 WebSockets 构建聊天应用程序

在本文中，我们将研究如何使用 Spring Boot 和 WebSockets 构建聊天应用程序。

WebSocket 是 Web 浏览器和服务器之间的双向、全双工、持久连接。它们允许两者之间进行实时通信。

Spring Boot 是一个基于 Java 的框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序。

## 设置项目

我们将使用 Spring Initializr 来设置我们的项目。转到 https://start.spring.io/ 并选择以下内容：

* 网络
* 网络套接字
*百里香叶

将项目命名为“聊天应用程序”，然后单击“生成项目”。

## 依赖

Spring Boot 会自动为我们的项目配置必要的依赖。

## WebSockets

WebSocket 由控制器处理。在我们的项目中，我们将创建一个名为“ChatController.java”的控制器。

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

`@MessageMapping` 注释将特定 URL 映射到控制器方法。 `@SendTo` 注释指定 WebSocket 服务器端点的 URL。然后将消息广播到连接到该端点的所有客户端。

在我们的 HTML 文件中，我们将添加一个带有输入字段和提交按钮的表单。该表单将 POST 到 `/chat` 端点。

```html
<form action="/chat" th:action="@{/chat}" th:object="${message}" method="post">
    <input type="text" th:field="*{text}"/>
    <input type="submit" value="Send"/>
</form>
```

输入字段绑定到“消息”对象的“文本”属性。提交表单时，将 `message` 对象传递给 `ChatController` 的 `sendMessage` 方法，并将 `text` 属性用作要广播的消息。

## 广播消息

我们可以使用 SimpMessagingTemplate 将消息广播到特定目的地。

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

`convertAndSend` 方法将消息转换为 JSON 并将其发送到指定的目的地。

## 接收消息

我们可以使用 @SubscribeMapping 注释将特定 URL 映射到方法。当客户端订阅 URL 时将调用该方法。

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

`subscribe` 方法返回一个消息列表，当它订阅到 `/topic/messages` 目的地时，这些消息将被发送到客户端。

## 测试应用程序

我们可以通过运行它并转到 http://localhost:8080/ 来测试我们的应用程序。我们应该看到表格和消息列表。

我们也可以打开浏览器的开发者工具，然后转到网络选项卡。我们应该看到正在建立的 WebSocket 连接。

## 结论

在本文中，我们了解了如何使用 Spring Boot 和 WebSockets 构建聊天应用程序。