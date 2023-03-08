---
title: 用于实时通信的 Spring Boot 和 WebSockets
description: 
published: true
date: 2023-02-04T10:56:44.340Z
tags: 
editor: markdown
dateCreated: 2023-02-04T10:56:42.580Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot and WebSockets for Real-Time Communication***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-websockets-for-real-time-communication)
{.links-list}


# 用于实时通信的 Spring Boot 和 WebSockets

作为在 Web 浏览器和 Web 服务器之间提供实时通信的一种方式，Websocket 正变得越来越流行。 Spring Boot 提供了一种非常方便的方式来开发和部署使用 Websockets 的 Web 应用程序。

## 什么是 WebSocket？

WebSockets 是一项相对较新的技术，它通过单个 TCP 连接提供全双工通信通道。这意味着客户端和服务器可以同时发送和接收数据。

WebSockets 特别适合需要低延迟的应用程序，例如聊天应用程序和在线游戏。

## 为什么要使用 Spring Boot？

Spring Boot 是一个非常流行的 Java 应用程序开发框架。它使得创建和部署基于 Spring 的应用程序变得非常容易。

Spring Boot 还提供了一种非常方便的方式来开发和部署使用 Websockets 的 Web 应用程序。

## 入门

在本节中，我们将创建一个使用 WebSockets 的非常简单的聊天应用程序。

我们将使用以下工具和技术：

- 弹簧靴
- WebSockets
- 爪哇

### 先决条件

在开始之前，我们需要确保安装了以下工具：

- Java 8
- 专家

### 创建项目

我们将使用 Spring Initializr 来创建我们的项目。 Spring Initializr 是一个 Web 应用程序，可帮助您创建基于 Spring 的项目。

转到 http://start.spring.io 并选择以下选项：

- 使用 Java 和 Spring Boot 1.4 生成 Maven 项目
- 网络
- 网络套接字
- 百里香叶

单击“生成项目”以下载项目。

### 设置项目

拥有项目后，您需要将其导入到您最喜欢的 IDE 中。我正在使用 IntelliJ IDEA。

导入项目后，您应该会看到以下项目结构：

```
├── pom.xml
└── src
    └── main
        ├── java
        │   └── com
        │       └── example
        │           └── websockets
        │               └── Application.java
        └── resources
            ├── application.properties
            └── templates
                └── index.html
```

### 实现 WebSocket 处理程序

我们将从实现 WebSocket 处理程序开始。这是将从客户端接收消息并向客户端发送消息的组件。

在 com.example.websockets 包中创建一个名为 MessageHandler 的新 Java 类。

将以下代码添加到“MessageHandler”类中：

```java
@Component
public class MessageHandler {

    private final SimpMessagingTemplate messagingTemplate;

    @Autowired
    public MessageHandler(SimpMessagingTemplate messagingTemplate) {
        this.messagingTemplate = messagingTemplate;
    }

    @MessageMapping("/send/message")
    public void onReceiveMessage(String message) {
        System.out.println("Received message: " + message);
        messagingTemplate.convertAndSend("/topic/messages", message);
    }
}
```

让我们来看看 MessageHandler 类中发生了什么。

首先，我们用 @Component 注释这个类。这告诉 Spring 这是一个可以注入到其他组件中的组件。

接下来，我们创建一个“SimpMessagingTemplate”字段并用“@Autowired”对其进行注释。这告诉 Spring 将 `SimpMessagingTemplate` 的实例注入到该字段中。

`SimpMessagingTemplate` 是 Spring 提供的一个组件，用于通过 WebSockets 向客户端发送消息。

接下来，我们创建一个将“SimpMessagingTemplate”作为参数的构造函数。当 Spring 将 `SimpMessagingTemplate` 的实例注入到 `messagingTemplate` 字段中时，将调用此构造函数。

最后，我们有一个名为“onReceiveMessage”的“@MessageMapping”注释方法。当消息发送到“/send/message”端点时调用此方法。

`@MessageMapping` 注释告诉 Spring，当在 `/send/message` 端点上接收到消息时应该调用此方法。

`onReceiveMessage` 方法采用 `String` 参数。这是从客户端发送的消息。

在 `onReceiveMessage` 方法中，我们将消息打印到控制台，然后使用 `messagingTemplate` 将消息发送到 `/topic/messages` 端点。

`/topic/messages` 端点是所有客户端都订阅的主题。将消息发送到此端点时，订阅该主题的所有客户端都将收到该消息。

### 实现 WebSocket 配置

接下来，我们需要实现 WebSocket 配置。这是将配置 WebSocket 连接的组件。

在 com.example.websockets 包中创建一个名为 WebSocketConfig 的新 Java 类。

将以下代码添加到“WebSocketConfig”类：

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {

    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {
        registry.enableSimpleBroker("/topic");
        registry.setApplicationDestinationPrefixes("/app");
    }

    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        registry.addEndpoint("/websocket").withSockJS();
    }
}
```

让我们看看“WebSocketConfig”类中发生了什么。

首先，我们用“@Configuration”和“@EnableWebSocketMessageBroker”注释类。 `@Configuration` 注解告诉 Spring 这是一个配置类。 `@EnableWebSocketMessageBroker` 注释启用 WebSocket 消息代理。

接下来，我们实现 WebSocketMessageBrokerConfigurer 接口。此接口提供用于配置 WebSocket 消息代理的方法。

我们覆盖了 `configureMessageBroker` 方法。此方法用于配置消息代理。

在 `configureMessageBroker` 方法中，我们启用简单代理并设置应用程序目标前缀。

简单代理是支持发布/订阅消息传递的消息代理。它使用起来非常简单，这就是我们将在本例中使用的。

应用程序目标前缀用于为从客户端发送的所有消息的目标添加前缀。

最后，我们覆盖 `registerStompEndpoints` 方法。此方法用于注册 STOMP 端点。 STOMP 是一种简单的面向文本的消息传递协议。

在 `registerStompEndpoints` 方法中，我们添加一个映射到 `/websocket` URL 的端点。我们还将端点配置为使用 SockJS。

SockJS 是一个客户端 JavaScript 库，它提供了一种通过 WebSockets 使用 STOMP 的便捷方式。

### 实现 Web 控制器

接下来，我们需要实现网络控制器。这是将处理 Web 请求的组件。

在 com.example.websockets 包中创建一个名为 WebController 的新 Java 类。

将以下代码添加到 `WebController` 类：

```java
@Controller
public class WebController {

    @GetMapping("/")
    public String index() {
        return "index";
    }
}
```

让我们看一下 WebController 类中发生了什么。

首先，我们用 @Controller 注释这个类。这告诉 Spring 这是一个 Web 控制器。

接下来，我们有一个名为 index 的 @GetMapping 注释方法。当对 `/` URL 发出 GET 请求时调用此方法。

在 `index` 方法中，我们返回 `index` 模板。 `index` 模板位于 `resources/templates` 目录中。

### 实现索引模板

接下来，我们需要实现 `index` 模板。

打开 `resources/templates/index.html` 文件并添加以下代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>WebSocket Chat</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/sockjs-client/1.1.2/sockjs.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/stomp.js/2.3.3/stomp.min.js"></script>
</head>
<body>

<h1>WebSocket Chat</h1>

<form id="message-form">
    <label for="message-input">Message:</label>
    <input type="text" id="message-input" placeholder="Enter a message">
    <button type="submit">Send</button>
</form>

<ul id="messages">
    <!-- Messages will be inserted here -->
</ul>

<script>
    var stompClient = null;

    function connect() {
        var socket = new SockJS('/websocket');
        stompClient = Stomp.over(socket);

        stompClient.connect({}, function (frame) {
            console.log('Connected: ' + frame);
            stompClient.subscribe('/topic/messages', function (message) {
                showMessage(JSON.parse(message.body).message);
            });
        });
    }

    function disconnect() {
        if (stompClient !== null) {
            stompClient.disconnect();
        }
        console.log("Disconnected");
    }

    function sendMessage() {
        var message = document.getElementById('message-input').value;
        stompClient.send("/app/send/message", {}, JSON.stringify({'message': message}));
    }

    function showMessage(message) {
        var messages = document.getElementById('messages');
        var li = document.createElement('li');
        li.appendChild(document.createTextNode(message));
        messages.appendChild(li);
    }

    connect();
</script>

</body>
</html>
```

让我们来看看 `index` 模板中发生了什么。

首先，我们包括 `sockjs` 和 `stomp` JavaScript 库。客户端使用这些库连接到 WebSocket 服务器。

接下来，我们有一个 `<form>` 元素，其 `id` 为 `message-form`。此 `<form>` 元素用于向服务器提交消息。

在 `<form>` 元素中，我们有一个 `<label>` 元素和一个 `<input>` 元素。 `<input>` 元素用于输入将发送到服务器的消息。

最后，我们有一个 `<ul>` 元素，其 `id` 为 `messages`。此 `<ul>` 元素用于显示从服务器接收到的消息。

在 `<ul>` 元素下方，我们有一个 JavaScript `<script>` 元素。此 `<script>` 元素包含用于连接到 WebSocket 服务器以及发送和接收消息的代码。

首先，我们创建一个 stompClient 变量。该变量用于存储 STOMP 客户端。

接下来，我们有一个 `connect` 函数。此函数用于连接到 WebSocket 服务器。

在 `connect` 函数中，我们创建一个新的 `SockJS` 实例并将 `/websocket` URL 传递给构造函数。此 URL 是我们在 WebSocketConfig 类中配置的端点。

然后我们创建一个新的 `stompClient` 实例并将 `SockJS` 实例传递给构造函数。

接下来，我们在 stompClient 实例上调用 connect 方法。此方法有两个参数。第一个参数是一个空对象，第二个参数是一个回调函数。

建立连接时调用回调函数。

在回调函数中，我们订阅了“/topic/messages”主题。这是 `MessageHandler` 类正在向其发布消息的主题。

当收到有关此主题的消息时，将调用回调函数并将该消息作为参数。

在回调函数中，我们调用 `showMessage` 函数并将消息传递给该函数。

`showMessage` 函数将消息作为参数并将消息添加到 `messages` `<ul>` 中。

最后，我们有一个 `disconnect` 函数。此函数用于断开与 WebSocket 服务器的连接。

在 disconnect 函数中，我们检查 stompClient 变量是否不为 null。如果它不是“null”，我们将在“stompClient”实例上调用“disconnect”方法。

我们还有一个 sendMessage 函数。该函数用于向服务器发送消息。

在 `sendMessage` 函数中，我们从 `message-input` `<input>` 元素获取消息并将其存储在名为 `message` 的变量中。

然后，我们在 stompClient 实例上调用 send 方法，并将目标、标头和正文传递给该方法。

目的地是我们要将消息发送到的端点。在这种情况下，我们希望将消息发送到“/app/send/message”端点。这是我们在 MessageHandler 类中配置的端点。

标头和正文是可选的。我们不需要在这个例子中设置标题，所以我们只传递一个空对象。

正文是我们要发送到服务器的消息。我们使用 `JSON.stringify` 函数将消息转换为 JSON 字符串。

最后，我们有一个 showMessage 函数。此函数用于在 `messages` `<ul>` 中显示消息。

在 `showMessage` 函数中，我们获取 `messages` `<ul>` 并将其存储在名为 `messages` 的变量中。

然后我们创建一个新的 `<li>` 元素并将其存储在一个名为 `li` 的变量中。

然后我们用消息作为文本创建一个新的 TextNode 并将其附加到 <li> 元素。

最后，我们将 `<li>` 元素附加到 `messages` `<ul>` 中。

在 index 模板的末尾，我们调用 connect 函数。这会将客户端连接到 WebSocket 服务器。

### 测试应用程序

现在我们已经实现了应用程序，让我们测试它。

通过运行 Application 类启动应用程序。

应用程序启动后，打开 Web 浏览器并转到 http://localhost:8080。

您应该会看到以下页面：

![WebSocket聊天页面](https://i.imgur.com/uGjTtqP.png)

在“消息”字段中输入一条消息，然后单击“发送”按钮。

您应该会看到消息出现在“消息”列表中。

![带有消息的 WebSocket 聊天页面](https://i.imgur.com/DVnWql6.png)

## 结论

在本文中，我们了解了如何使用 Spring Boot 和 WebSockets 创建实时聊天应用程序。

我们还研究了如何使用 SimpMessagingTemplate 通过 WebSockets 向客户端发送消息。

## 参考

- [Spring Boot 参考文档](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
- [WebSocket](https://en.wikipedia.org/wiki/WebSocket)
- [Spring Boot 和 WebSockets](https://spring.io/guides/gs/messaging-stomp-websocket/)
- [使用 WebSockets 构建聊天应用程序