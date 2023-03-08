---
title: 012：将 Spring Boot 与消息代理 (RabbitMQ) 结合使用
description: 
published: true
date: 2023-02-01T20:26:40.211Z
tags: 
editor: markdown
dateCreated: 2023-02-01T20:26:38.529Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [012: Using Spring Boot with message brokers (RabbitMQ)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/012-using-spring-boot-with-message-brokers-rabbitmq)
{.links-list}


# 012：将 Spring Boot 与消息代理 (RabbitMQ) 结合使用

在这篇文章中，我们将看看如何将 Spring Boot 与消息代理一起使用，特别是 RabbitMQ。我们将介绍什么是消息代理、如何将它们与 Spring Boot 一起使用以及一些最佳实践。

## 什么是消息代理？

消息代理是一种软件，可帮助管理不同应用程序之间的通信。它通过充当应用程序之间的中间人来做到这一点。应用程序可以将消息发送到代理，然后代理将消息转发到适当的应用程序。

## 为什么要使用消息代理？

您可能想要使用消息代理的原因有几个。

### 1.解耦应用

使用消息代理的主要原因之一是解耦应用程序。通过解耦，我们的意思是应用程序不直接相互依赖。这有一些好处。

首先，这意味着应用程序可以独立开发。如果您有一个大型团队在系统的不同部分工作，这可能是一个很大的优势。

其次，它使应用程序更具弹性。如果一个应用程序出现故障，其他应用程序仍然可以继续工作。

### 2.可扩展性

使用消息代理的另一个原因是可伸缩性。如果流量很大，可以添加更多代理来处理负载。这比尝试扩展单个应用程序要容易得多。

## 如何在 Spring Boot 中使用消息代理

现在我们已经了解了使用消息代理的一些原因，让我们看看如何将消息代理与 Spring Boot 一起使用。

Spring Boot 对消息代理有很好的支持。我们可以使用 `spring-boot-starter-amqp` 依赖来添加对 RabbitMQ 的支持。

要使用 RabbitMQ，我们需要将以下内容添加到我们的 application.properties 文件中：

```properties
spring.rabbitmq.host=localhost
spring.rabbitmq.port=5672
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```

将 `localhost` 替换为您的 RabbitMQ 服务器的主机名。默认端口为“5672”。用户名和密码是 RabbitMQ 的默认值。

一旦我们添加了属性，我们就可以在我们的代码中注入一个“RabbitTemplate”。这是我们将用来发送和接收消息的类。

以下是如何使用模板发送消息的简单示例：

```java
@Autowired
private RabbitTemplate rabbitTemplate;

public void sendMessage(String message) {
    rabbitTemplate.convertAndSend("exchange", "routingKey", message);
}
```

`convertAndSend` 方法采用交换、路由密钥和消息。 exchange 是要使用的交换的名称。路由键用于将消息路由到正确的队列。消息可以是任何可以转换为字节数组的对象。

我们还可以使用 `receiveAndConvert` 方法接收消息：

```java
@Autowired
private RabbitTemplate rabbitTemplate;

public String receiveMessage() {
    return (String)rabbitTemplate.receiveAndConvert("queue");
}
```

此方法采用队列名称并返回一个对象。我们需要将对象转换为正确的类型。

## 最佳实践

现在我们已经了解了如何将消息代理与 Spring Boot 结合使用，让我们来看看一些最佳实践。

### 1.使用消息转换器

Spring Boot 带有许多消息转换器。这些转换器可用于在不同的消息格式之间进行转换。例如，我们可以使用 StringMessageConverter 在字符串和字节数组之间进行转换。

在发送和接收消息时使用消息转换器是个好主意。这样，我们就不必担心将消息转换为正确的格式。

### 2.使用消息监听器

另一个最佳实践是使用消息监听器。消息侦听器是实现“MessageListener”接口的类。这个接口有一个 onMessage 方法：

```java
public interface MessageListener {
    void onMessage(Message message);
}
```

收到消息时调用此方法。消息作为参数传入。

消息侦听器是在收到消息时处理消息的好方法。我们不必担心轮询消息或将消息转换为正确的格式。

### 3.使用消息队列

使用消息代理时，最好使用消息队列。消息队列是一种存储消息的数据结构。消息按照收到的顺序存储。

消息队列可用于存储需要处理的消息。例如，我们可以在收到消息时将消息添加到队列中。然后我们可以一次处理队列中的消息。

消息队列可用于提高性能。如果我们要处理很多消息，我们可以并行处理它们。这样，我们就不必等待一条消息处理完毕再开始处理下一条消息。

## 附加信息

- [Spring Boot 参考指南](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
- [RabbitMQ 文档](https://www.rabbitmq.com/documentation.html)

## 警告

- 确保在发送和接收消息时使用正确的消息转换器。否则，您可能会得到意想不到的结果。
- 确保在接收消息时使用正确的消息监听器。否则，您可能会错过消息或获得意想不到的结果。

## 危险

- 如果您没有使用消息队列，您的消息可能会被乱序处理。
- 如果您没有使用消息转换器，您的消息可能无法转换为正确的格式。