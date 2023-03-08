---
title: 将 Kafka 与 Spring Boot 集成以进行实时处理
description: 
published: true
date: 2023-02-17T18:04:54.059Z
tags: 
editor: markdown
dateCreated: 2023-01-30T13:32:55.920Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Integrating Kafka with Spring Boot for Real-time Processing***English** version of this document is available*](/en/Knowledge-base/Backend/integrating-kafka-with-spring-boot-for-real-time-processing)
{.links-list}




# 将 Kafka 与 Spring Boot 集成进行实时处理

如果您正在阅读本文，那么您可能熟悉数据流的概念以及该过程中涉及的各种工具和技术。在本文中，我们将重点介绍一种特定的流数据工具：Apache Kafka。我们将向您展示如何将 Kafka 与 Spring Boot 集成以进行实时处理。在我们开始之前，让我们回顾一些基础知识。

数据流是将数据记录从源连续传输到目的地的过程。数据记录是实时生成的，可以是任何大小或格式。源可以是任何东西，从简单的日志文件到复杂的事件处理系统。目标可以是数据仓库、NoSQL 数据库，甚至是简单的文件系统。数据流的主要优点是它允许您在数据到达时对其进行处理，而不是在开始处理之前等待收集完所有数据。

Kafka 是一种流行的开源数据流工具。它最初由 LinkedIn 开发，后来捐赠给 Apache 软件基金会。 Kafka 是用 Java 和 Scala 编写的。它是一个发布-订阅消息传递系统，提供三个关键功能：

- **持久性：** Kafka 消息持久保存在磁盘上并在集群内复制。
- **低延迟：** Kafka 可以在消息到达时以非常低的延迟进行处理。
- **可扩展性：** Kafka 是水平可扩展的，这意味着它可以通过向集群添加更多代理来处理不断增加的吞吐量。

Kafka 与 Spring Boot 配合得很好，因为它提供了与 Java 生态系统的干净集成。 Spring Boot 是一种流行的 Java 框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序。 Spring Boot 提供了许多对数据流应用程序有用的功能，例如自动配置和嵌入式服务器。

在本文中，我们将向您展示如何使用 Kafka 和 Spring Boot 构建一个简单的消息生产者和消费者应用程序。我们还将向您展示如何使用 Spring Cloud Stream，这是一个用于构建消息驱动的微服务的库。


## 设置卡夫卡

在我们开始开发我们的应用程序之前，我们需要设置一个 Kafka 代理。 Kafka 经纪人是 Kafka 系统的核心。他们负责维护主题列表以及接受和复制来自生产者的消息。我们将使用 Apache Kafka 版本 2.4.0，您可以[在此处下载](https://kafka.apache.org/downloads?view=release-2.4.0)。

下载 Kafka 二进制文件后，将其解压缩到您选择的位置。出于本文的目的，我们假设 Kafka 二进制文件已解压缩到以下位置：

```
/kafka_2.12-2.4.0
```

我们现在可以通过运行以下命令来启动 Kafka 代理：

```
bin/zookeeper-server-start.sh config/zookeeper.properties
bin/kafka-server-start.sh config/server.properties
```

这将启动 ZooKeeper 服务器和 Kafka 代理。默认情况下，Kafka 代理将监听端口 9092。

## 创建一个 Kafka 主题

现在 Kafka 代理已启动并运行，我们可以创建一个 Kafka 主题。 Kafka 主题是消息存储的逻辑单元。它由名称标识，并分为多个分区。分区分布在 Kafka 集群中。

我们可以使用以下命令创建一个名为“test”的具有两个分区的 Kafka 主题：

```
bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 2 --topic test
```

## 生成消息

现在我们有了一个 Kafka 主题，我们可以开始生成消息了。我们将使用 Kafka 控制台生产者，这是一个可用于生产消息的命令行工具。控制台生产者将从标准输入读取消息并将它们发送到 Kafka 代理。

我们可以使用以下命令启动控制台生产者：

```
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
```

控制台生产者现在将等待消息。我们可以键入一条消息，然后按 Enter 键发送它。该消息将发送到 Kafka 代理，并将复制到分配的分区。

## 消费消息

现在我们有了一个 Kafka 主题并且正在生成消息，我们可以开始使用它们了。我们将使用 Kafka 控制台消费者，这是一个可用于消费消息的命令行工具。控制台消费者将从 Kafka 代理读取消息并将它们写入标准输出。

我们可以使用以下命令启动控制台消费者：

```
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning
```

控制台消费者现在将开始从 Kafka 代理读取消息并将它们写入标准输出。您应该会看到使用控制台生成器发送的消息。

## Spring Boot 和 Kafka

现在我们已经了解了如何设置 Kafka 以及如何生成和使用消息，我们将看看如何将 Kafka 与 Spring Boot 结合使用。 Spring Boot 提供了许多对数据流应用程序有用的功能，例如自动配置和嵌入式服务器。

Spring Boot 还提供了许多 Starter POM，它们是可以包含在您的应用程序中的预配置依赖项。例如，`spring-kafka-starter` Starter POM 包括 Kafka 和 Spring Kafka 的依赖项。

在本节中，我们将向您展示如何使用 `spring-kafka-starter` Starter POM 开发一个简单的消息生产者和消费者应用程序。

## 消息生产者

我们需要做的第一件事是创建一个 Spring Boot 应用程序。我们将使用 `spring-boot-starter-parent` Starter POM 作为我们应用程序的父级。 `spring-boot-starter-parent` Starter POM 提供了许多我们可以继承的依赖和插件管理功能。

我们可以使用 Spring Initializr 创建 Spring Boot 应用程序。 Spring Initializr 是一个基于 Web 的工具，可用于创建 Spring Boot 应用程序。我们可以使用 Spring Initializr 通过 `spring-kafka-starter` Starter POM 创建基于 Maven 的 Spring Boot 应用程序。

生成应用程序后，我们可以将以下依赖项添加到 `pom.xml` 文件中：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.kafka</groupId>
        <artifactId>spring-kafka</artifactId>
    </dependency>
    <dependency>
        <groupId>org.apache.kafka</groupId>
        <artifactId>kafka-clients</artifactId>
        <version>2.4.0</version>
    </dependency>
</dependencies>
```

`spring-kafka-starter` Starter POM 将为我们引入`kafka-clients` 依赖项。我们需要指定 `kafka-clients` 依赖项的版本，因为 `spring-kafka-starter` Starter POM 中包含的版本与 Apache Kafka 2.4.0 不兼容。

现在我们有了依赖项，我们可以创建一个配置类。配置类将用于配置 Kafka 生产者。我们可以使用 @EnableKafka 注释在我们的 Spring Boot 应用程序中启用 Kafka。

我们还将创建一个 `KafkaTemplate` bean。 `KafkaTemplate` 是一个辅助类，可用于向 Kafka 发送消息。

```java
@Configuration
@EnableKafka
public class KafkaConfig {

    @Bean
    public KafkaTemplate<String, String> kafkaTemplate(
            ProducerFactory<String, String> producerFactory) {
        return new KafkaTemplate<>(producerFactory);
    }
}
```

我们现在可以创建消息生产者 bean。消息生产者 bean 将用于向 Kafka 发送消息。我们将把 `KafkaTemplate` 注入到消息生产者 bean 中。

```java
@Component
public class MessageProducer {

    private KafkaTemplate<String, String> kafkaTemplate;

    @Autowired
    public MessageProducer(KafkaTemplate<String, String> kafkaTemplate) {
        this.kafkaTemplate = kafkaTemplate;
    }

    public void sendMessage(String topic, String message) {
        kafkaTemplate.send(topic, message);
    }
}
```

`sendMessage` 方法可用于向 Kafka 主题发送消息。我们将在我们的消息消费者中使用这个方法。

## 消息消费者

我们现在可以创建一个消息消费者 bean。消息消费者 bean 将用于消费来自 Kafka 的消息。我们将把 `KafkaTemplate` 和 `MessageProducer` 注入到消息消费者 bean 中。

```java
@Component
public class MessageConsumer {

    private KafkaTemplate<String, String> kafkaTemplate;
    private MessageProducer messageProducer;

    @Autowired
    public MessageConsumer(
            KafkaTemplate<String, String> kafkaTemplate,
            MessageProducer messageProducer) {
        this.kafkaTemplate = kafkaTemplate;
        this.messageProducer = messageProducer;
    }

    @KafkaListener(topics = "test")
    public void processMessage(String message) {
        messageProducer.sendMessage("test2", message);
    }
}
```

`processMessage` 方法用`@KafkaListener` 注释。此注释用于配置 Kafka 消息侦听器。 @KafkaListener 注释可用于注释从 Kafka 主题接收到消息时将调用的方法。在此示例中，我们使用 @KafkaListener 注释为“test”主题配置消息侦听器。

`@KafkaListener` 注释有许多可用于配置消息监听器的属性：

- `topics`：要收听的 Kafka 主题列表。
- `groupId`：Kafka 消费者组 ID。
- `containerFactory`：要使用的 `KafkaListenerContainerFactory`。

当从“测试”主题收到消息时，将调用 `processMessage` 方法。该消息将被处理，然后发送到“test2”主题。

我们现在可以运行我们的应用程序并向“测试”主题生成消息。消息将被处理并发送到“test2”主题。我们可以使用 Kafka 控制台消费者使用来自“test2”主题的消息。

## 结论

在本文中，我们向您展示了如何使用 Kafka 和 Spring Boot 构建一个简单的消息生产者和消费者应用程序。我们还向您展示了如何使用 Spring Cloud Stream，这是一个用于构建消息驱动的微服务的库。