---
title: 026：使用 Spring Boot 和 Apache Kafka
description: 
published: true
date: 2023-02-03T18:32:23.616Z
tags: 
editor: markdown
dateCreated: 2023-02-03T18:32:21.993Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [026: Working with Spring Boot and Apache Kafka***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/026-working-with-spring-boot-and-apache-kafka)
{.links-list}


# 使用 Spring Boot 和 Apache Kafka

在本文中，我们将了解如何使用 Spring Boot 和 Apache Kafka。我们将涵盖以下主题：

- 什么是 Apache Kafka？
- 什么是 Spring Boot？
- 如何将 Spring Boot 与 Apache Kafka 结合使用
- 附加信息
- 警告
- 危险

## 什么是 Apache Kafka？

Apache Kafka 是一个分布式流媒体平台。它用于构建实时数据管道和流式应用程序。它具有水平可扩展性、容错性和快速性。

Kafka 是用 Scala 和 Java 编写的。它具有发布-订阅消息传递模型。它是一个高性能系统。

## 什么是 Spring Boot？

Spring Boot 是一个基于 Java 的框架，用于创建微服务。它用于简化新 Spring 应用程序的引导和开发。

Spring Boot 固执己见。它提供了一组默认配置。它使创建独立的、生产级的基于 Spring 的应用程序变得容易。

## 如何将 Spring Boot 与 Apache Kafka 结合使用

为了将 Spring Boot 与 Apache Kafka 一起使用，我们需要将以下依赖项添加到我们的项目中：

```xml
<dependency>
    <groupId>org.springframework.kafka</groupId>
    <artifactId>spring-kafka</artifactId>
</dependency>
```

如果我们想将 Apache Kafka 与 Avro 一起使用，我们还需要添加以下依赖项：

```xml
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-avro-serializer</artifactId>
</dependency>
```

现在我们已经有了依赖项，让我们来看看如何将 Spring Boot 与 Apache Kafka 结合使用。

### 配置

首先，我们需要配置 Apache Kafka 代理。我们可以通过在 application.properties 文件中设置以下属性来做到这一点：

```properties
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.producer.retries=0
spring.kafka.producer.batch-size=16384
spring.kafka.producer.buffer-memory=33554432
spring.kafka.consumer.group-id=test
spring.kafka.consumer.auto-offset-reset=earliest
spring.kafka.consumer.enable-auto-commit=false
```

在上面的配置中，我们设置了以下属性：

- Apache Kafka 代理地址
- 生产者的重试次数
- 生产者批量大小
- 生产者缓冲存储器
- 消费者组id
- 消费者自动偏移重置
- 消费者自动提交

### 制作人

现在让我们看看如何创建生产者。我们可以通过创建一个 Producer 类来做到这一点：

```java
@Component
public class Producer {

    private static final Logger LOGGER = LoggerFactory.getLogger(Producer.class);

    @Autowired
    private KafkaTemplate<String, String> kafkaTemplate;

    public void send(String topic, String message) {
        LOGGER.info("sending message='{}' to topic='{}'", message, topic);
        kafkaTemplate.send(topic, message);
    }

}
```

在上面的生产者中，我们使用 KafkaTemplate 向 Kafka 代理发送消息。

### 消费者

现在让我们看一下如何创建消费者。我们可以通过创建一个 Consumer 类来做到这一点：

```java
@Component
public class Consumer {

    private static final Logger LOGGER = LoggerFactory.getLogger(Consumer.class);

    @KafkaListener(topics = "test", groupId = "test")
    public void listen(String message) {
        LOGGER.info("received message='{}'", message);
    }

}
```

在上面的消费者中，我们使用@KafkaListener 注释来监听关于“test”主题的消息。

## 附加信息

- 春季启动：https://spring.io/projects/spring-boot
- 阿帕奇卡夫卡：https://kafka.apache.org/

## 警告

- 确保将 Apache Kafka 代理地址添加到 application.properties 文件中。
- 确保将 spring-kafka 依赖项添加到项目中。

## 危险

- 不要在消费者中手动提交偏移量。