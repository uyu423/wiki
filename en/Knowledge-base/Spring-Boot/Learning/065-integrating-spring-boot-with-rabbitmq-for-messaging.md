---
title: 065: Integrating Spring Boot with RabbitMQ for Messaging
description: 
published: true
date: 2023-02-03T19:55:33.379Z
tags: 
editor: markdown
dateCreated: 2023-02-03T19:55:28.246Z
---

- [065: Integración de Spring Boot con RabbitMQ para mensajería***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/065-integrating-spring-boot-with-rabbitmq-for-messaging)
{.links-list}
- [065：将 Spring Boot 与 RabbitMQ 集成以进行消息传递***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/065-integrating-spring-boot-with-rabbitmq-for-messaging)
{.links-list}
- [065: 메시징을 위해 Spring Boot와 RabbitMQ 통합***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/065-integrating-spring-boot-with-rabbitmq-for-messaging)
{.links-list}


# 065: Integrating Spring Boot with RabbitMQ for Messaging

In this post, we'll learn how to integrate Spring Boot with RabbitMQ to produce and consume messages. We'll also explore how to set up a simple message queue using RabbitMQ.

RabbitMQ is a message broker that allows clients to connect and exchange messages. It's a popular choice for handling message queues, and it has good integration with Spring Boot.

## Setting up RabbitMQ

Before we can start using RabbitMQ, we need to set it up. We'll use Docker to run a RabbitMQ server in a container.

First, we need to pull the RabbitMQ Docker image:

```
$ docker pull rabbitmq:3.6.5-management
```

Next, we'll start a Docker container using the image we just pulled:

```
$ docker run -d --name rabbitmq -p 15672:15672 -p 5672:5672 rabbitmq:3.6.5-management
```

This will start a RabbitMQ server in a container and expose the management UI on port 15672 and the message broker on port 5672.

## Creating a Spring Boot Project

Now that we have RabbitMQ up and running, we can create a Spring Boot project to produce and consume messages.

We'll use the Spring Initializr to create our project. We'll need to select the following dependencies:

* Web
* AMQP

We can leave the other options at their defaults.

Once the project is generated, we'll need to add the following dependency to our `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```

## Configuring Spring Boot

Now that we have our project set up, we need to configure Spring Boot to connect to our RabbitMQ server. We'll do this by adding the following to our `application.properties`:

```
spring.rabbitmq.host=localhost
spring.rabbitmq.port=5672
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```

## Creating a Producer

Now that our project is set up and configured, we can create a producer to send messages to our RabbitMQ server.

We'll create a `MessageProducer` class with a `sendMessage` method that takes a `String` and sends it to a RabbitMQ `Queue`.

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

In this class, we're using the `AmqpTemplate` to convert our `String` message to an `AMQP` message and send it to the `queue`.

## Creating a Consumer

Now that we have a producer, we need a consumer to receive the messages from the queue.

We'll create a `MessageConsumer` class with a `receiveMessage` method that receives an `AMQP` message from the `queue` and converts it to a `String`.

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

In this class, we're using the `AmqpTemplate` to receive an `AMQP` message from the `queue` and convert it to a `String`.

## Testing Our Producer and Consumer

Now that we have our producer and consumer set up, let's write a test to send a message from our producer to our consumer.

We'll create a `MessageProducerConsumerTest` class with a `testSendReceiveMessage` method that sends a message from our producer to our consumer.

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

In this test, we're sending a message from our producer to our consumer and asserting that the received message is the same as the message we sent.

## Additional Information

* For more information on RabbitMQ, check out the [RabbitMQ website](https://www.rabbitmq.com/).
* For more information on Spring Boot, check out the [Spring Boot website](https://spring.io/projects/spring-boot).