---
title: 065：将 Spring Boot 与 RabbitMQ 集成以进行消息传递
description: 
published: true
date: 2023-02-03T19:55:29.895Z
tags: 
editor: markdown
dateCreated: 2023-02-03T19:55:28.244Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [065: Integrating Spring Boot with RabbitMQ for Messaging***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/065-integrating-spring-boot-with-rabbitmq-for-messaging)
{.links-list}


# 065：将 Spring Boot 与 RabbitMQ 集成以进行消息传递

在本文中，我们将学习如何将 Spring Boot 与 RabbitMQ 集成以生成和使用消息。我们还将探讨如何使用 RabbitMQ 设置简单的消息队列。

RabbitMQ 是一个消息代理，允许客户端连接和交换消息。它是处理消息队列的流行选择，并且与 Spring Boot 集成良好。

## 设置 RabbitMQ

在开始使用 RabbitMQ 之前，我们需要对其进行设置。我们将使用 Docker 在容器中运行 RabbitMQ 服务器。

首先，我们需要拉取 RabbitMQ Docker 镜像：

```
$ docker pull rabbitmq:3.6.5-management
```

接下来，我们将使用刚刚拉取的镜像启动一个 Docker 容器：

```
$ docker run -d --name rabbitmq -p 15672:15672 -p 5672:5672 rabbitmq:3.6.5-management
```

这将在容器中启动 RabbitMQ 服务器，并在端口 15672 上公开管理 UI 并在端口 5672 上公开消息代理。

## 创建一个 Spring Boot 项目

现在我们已经启动并运行了 RabbitMQ，我们可以创建一个 Spring Boot 项目来生成和使用消息。

我们将使用 Spring Initializr 来创建我们的项目。我们需要选择以下依赖项：

* 网络
* AMQP

我们可以将其他选项保留为默认值。

生成项目后，我们需要将以下依赖项添加到我们的 `pom.xml` 中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```

## 配置 Spring Boot

现在我们已经设置了项目，我们需要配置 Spring Boot 以连接到我们的 RabbitMQ 服务器。我们将通过将以下内容添加到我们的 application.properties 中来做到这一点：

```
spring.rabbitmq.host=localhost
spring.rabbitmq.port=5672
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```

## 创建生产者

现在我们的项目已经设置和配置好了，我们可以创建一个生产者来将消息发送到我们的 RabbitMQ 服务器。

我们将创建一个带有 sendMessage 方法的 `MessageProducer` 类，该方法采用 `String` 并将其发送到 RabbitMQ `Queue`。

```java
@Component
public class MessageProducer {

    @Autowired
    private AmqpTemplate amqpTemplate;

    public void sendMessage(String message) {
        amqpTemplate.convertAndSend("queue", message);
    }

}
```

在这个类中，我们使用 `AmqpTemplate` 将我们的 `String` 消息转换为 `AMQP` 消息并将其发送到 `queue`。

## 创建消费者

现在我们有了一个生产者，我们需要一个消费者来接收来自队列的消息。

我们将创建一个带有 `receiveMessage` 方法的 `MessageConsumer` 类，该方法从 `queue` 接收 `AMQP` 消息并将其转换为 `String`。

```java
@Component
public class MessageConsumer {

    @Autowired
    private AmqpTemplate amqpTemplate;

    public String receiveMessage() {
        return (String) amqpTemplate.receiveAndConvert("queue");
    }

}
```

在此类中，我们使用 `AmqpTemplate` 从 `queue` 接收 `AMQP` 消息并将其转换为 `String`。

## 测试我们的生产者和消费者

现在我们已经设置了生产者和消费者，让我们编写一个测试，将消息从我们的生产者发送到我们的消费者。

我们将创建一个带有 testSendReceiveMessage 方法的 MessageProducerConsumerTest 类，该方法将消息从我们的生产者发送到我们的消费者。

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class MessageProducerConsumerTest {

    @Autowired
    private MessageProducer messageProducer;

    @Autowired
    private MessageConsumer messageConsumer;

    @Test
    public void testSendReceiveMessage() {
        String message = "Hello, world!";
        messageProducer.sendMessage(message);
        String receivedMessage = messageConsumer.receiveMessage();
        assertThat(receivedMessage, is(message));
    }

}
```

在此测试中，我们从生产者向消费者发送一条消息，并断言接收到的消息与我们发送的消息相同。

## 附加信息

* 有关 RabbitMQ 的更多信息，请查看 [RabbitMQ 网站](https://www.rabbitmq.com/)。
* 有关 Spring Boot 的更多信息，请查看 [Spring Boot 网站](https://spring.io/projects/spring-boot)。