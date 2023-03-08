---
title: Spring Boot and WebSockets for Real-Time Communication
description: 
published: true
date: 2023-02-04T10:56:48.064Z
tags: 
editor: markdown
dateCreated: 2023-02-04T10:56:42.587Z
---

- [Spring Boot y WebSockets para comunicación en tiempo real***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-and-websockets-for-real-time-communication)
{.links-list}
- [用于实时通信的 Spring Boot 和 WebSockets***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-and-websockets-for-real-time-communication)
{.links-list}
- [실시간 통신을 위한 Spring Boot 및 WebSocket***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-and-websockets-for-real-time-communication)
{.links-list}


# Spring Boot and WebSockets for Real-Time Communication

Websockets are becoming increasingly popular as a means of providing real-time communication between web browsers and web servers. Spring Boot provides a very convenient way to develop and deploy web applications that use Websockets.

## What are WebSockets?

WebSockets are a relatively new technology that provides full-duplex communication channels over a single TCP connection. This means that both the client and server can send and receive data at the same time.

WebSockets are particularly well suited for applications that require low latency, such as chat applications and online games.

## Why Use Spring Boot?

Spring Boot is a very popular framework for developing Java applications. It makes it very easy to create and deploy Spring-based applications.

Spring Boot also provides a very convenient way to develop and deploy web applications that use Websockets.

## Getting Started

In this section, we'll create a very simple chat application that uses WebSockets.

We'll be using the following tools and technologies:

- Spring Boot
- WebSockets
- Java

### Prerequisites

Before we get started, we need to make sure that we have the following tools installed:

- Java 8
- Maven

### Creating the Project

We're going to use Spring Initializr to create our project. Spring Initializr is a web application that helps you create Spring-based projects.

Go to http://start.spring.io and select the following options:

- Generate a Maven Project with Java and Spring Boot 1.4
- Web
- WebSocket
- Thymeleaf

Click "Generate Project" to download the project.

### Setting up the Project

Once you have the project, you need to import it into your favorite IDE. I'm using IntelliJ IDEA.

Once the project is imported, you should see the following project structure:

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

### Implementing the WebSocket Handler

We'll start by implementing the WebSocket handler. This is the component that will receive messages from the client and send messages to the client.

Create a new Java class called `MessageHandler` in the `com.example.websockets` package.

Add the following code to the `MessageHandler` class:

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

Let's take a look at what's going on in the `MessageHandler` class.

First, we annotate the class with `@Component`. This tells Spring that this is a component that can be injected into other components.

Next, we create a `SimpMessagingTemplate` field and annotate it with `@Autowired`. This tells Spring to inject an instance of `SimpMessagingTemplate` into this field.

`SimpMessagingTemplate` is a component that is provided by Spring for sending messages to clients over WebSockets.

Next, we create a constructor that takes `SimpMessagingTemplate` as a parameter. This constructor is called when Spring injects an instance of `SimpMessagingTemplate` into the `messagingTemplate` field.

Finally, we have a `@MessageMapping` annotated method called `onReceiveMessage`. This method is called when a message is sent to the `/send/message` endpoint.

The `@MessageMapping` annotation tells Spring that this method should be called when a message is received on the `/send/message` endpoint.

The `onReceiveMessage` method takes a `String` parameter. This is the message that was sent from the client.

Inside the `onReceiveMessage` method, we print the message to the console and then use the `messagingTemplate` to send the message to the `/topic/messages` endpoint.

The `/topic/messages` endpoint is a topic that all clients are subscribed to. When a message is sent to this endpoint, all clients that are subscribed to the topic will receive the message.

### Implementing the WebSocket Configuration

Next, we need to implement the WebSocket configuration. This is the component that will configure the WebSocket connection.

Create a new Java class called `WebSocketConfig` in the `com.example.websockets` package.

Add the following code to the `WebSocketConfig` class:

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

Let's take a look at what's going on in the `WebSocketConfig` class.

First, we annotate the class with `@Configuration` and `@EnableWebSocketMessageBroker`. The `@Configuration` annotation tells Spring that this is a configuration class. The `@EnableWebSocketMessageBroker` annotation enables the WebSocket message broker.

Next, we implement the `WebSocketMessageBrokerConfigurer` interface. This interface provides methods for configuring the WebSocket message broker.

We override the `configureMessageBroker` method. This method is used to configure the message broker.

In the `configureMessageBroker` method, we enable the simple broker and set the application destination prefix.

The simple broker is a message broker that supports pub/sub messaging. It's very simple to use and it's what we'll be using in this example.

The application destination prefix is used to prefix the destination of all messages that are sent from the client.

Finally, we override the `registerStompEndpoints` method. This method is used to register STOMP endpoints. STOMP is a simple text-oriented messaging protocol.

In the `registerStompEndpoints` method, we add an endpoint that is mapped to the `/websocket` URL. We also configure the endpoint to use SockJS.

SockJS is a client-side JavaScript library that provides a convenient way to use STOMP over WebSockets.

### Implementing the Web Controller

Next, we need to implement the web controller. This is the component that will handle web requests.

Create a new Java class called `WebController` in the `com.example.websockets` package.

Add the following code to the `WebController` class:

```java
@Controller
public class WebController {

    @GetMapping("/")
    public String index() {
        return "index";
    }
}
```

Let's take a look at what's going on in the `WebController` class.

First, we annotate the class with `@Controller`. This tells Spring that this is a web controller.

Next, we have a `@GetMapping` annotated method called `index`. This method is called when a GET request is made to the `/` URL.

Inside the `index` method, we return the `index` template. The `index` template is located in the `resources/templates` directory.

### Implementing the Index Template

Next, we need to implement the `index` template.

Open the `resources/templates/index.html` file and add the following code:

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

Let's take a look at what's going on in the `index` template.

First, we include the `sockjs` and `stomp` JavaScript libraries. These libraries are used by the client to connect to the WebSocket server.

Next, we have a `<form>` element with an `id` of `message-form`. This `<form>` element is used to submit messages to the server.

Inside the `<form>` element, we have a `<label>` element and a `<input>` element. The `<input>` element is used to enter the message that will be sent to the server.

Finally, we have a `<ul>` element with an `id` of `messages`. This `<ul>` element is used to display the messages that are received from the server.

Below the `<ul>` element, we have a JavaScript `<script>` element. This `<script>` element contains the code for connecting to the WebSocket server and sending and receiving messages.

First, we create a `stompClient` variable. This variable is used to store the STOMP client.

Next, we have a `connect` function. This function is used to connect to the WebSocket server.

Inside the `connect` function, we create a new `SockJS` instance and pass the `/websocket` URL to the constructor. This URL is the endpoint that we configured in the `WebSocketConfig` class.

We then create a new `stompClient` instance and pass the `SockJS` instance to the constructor.

Next, we call the `connect` method on the `stompClient` instance. This method takes two arguments. The first argument is an empty object and the second argument is a callback function.

The callback function is called when the connection is established.

Inside the callback function, we subscribe to the `/topic/messages` topic. This is the topic that the `MessageHandler` class is publishing messages to.

When a message is received on this topic, the callback function is called with the message as an argument.

In the callback function, we call the `showMessage` function and pass the message to the function.

The `showMessage` function takes a message as an argument and adds the message to the `messages` `<ul>`.

Finally, we have a `disconnect` function. This function is used to disconnect from the WebSocket server.

Inside the `disconnect` function, we check if the `stompClient` variable is not `null`. If it is not `null`, we call the `disconnect` method on the `stompClient` instance.

We also have a `sendMessage` function. This function is used to send a message to the server.

Inside the `sendMessage` function, we get the message from the `message-input` `<input>` element and store it in a variable called `message`.

We then call the `send` method on the `stompClient` instance and pass the destination, headers, and body to the method.

The destination is the endpoint that we want to send the message to. In this case, we want to send the message to the `/app/send/message` endpoint. This is the endpoint that we configured in the `MessageHandler` class.

The headers and body are optional. We don't need to set the headers in this example, so we just pass an empty object.

The body is the message that we want to send to the server. We use the `JSON.stringify` function to convert the message to a JSON string.

Finally, we have a `showMessage` function. This function is used to display a message in the `messages` `<ul>`.

Inside the `showMessage` function, we get the `messages` `<ul>` and store it in a variable called `messages`.

We then create a new `<li>` element and store it in a variable called `li`.

We then create a new `TextNode` with the message as the text and append it to the `<li>` element.

Finally, we append the `<li>` element to the `messages` `<ul>`.

At the end of the `index` template, we call the `connect` function. This will connect the client to the WebSocket server.

### Testing the Application

Now that we've implemented the application, let's test it.

Start the application by running the `Application` class.

Once the application is started, open a web browser and go to http://localhost:8080.

You should see the following page:

![WebSocket Chat Page](https://i.imgur.com/uGjTtqP.png)

Enter a message in the `Message` field and click the `Send` button.

You should see the message appear in the `Messages` list.

![WebSocket Chat Page with Message](https://i.imgur.com/DVnWql6.png)

## Conclusion

In this article, we've looked at how to use Spring Boot and WebSockets to create a real-time chat application.

We've also looked at how to use the `SimpMessagingTemplate` to send messages to clients over WebSockets.

## References

- [Spring Boot Reference Documentation](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
- [WebSocket](https://en.wikipedia.org/wiki/WebSocket)
- [Spring Boot and WebSockets](https://spring.io/guides/gs/messaging-stomp-websocket/)
- [Using WebSockets to Build a Chat Application