---
title: 使用 Kafka 的 Spring Boot 和事件驱动架构
description: 
published: true
date: 2023-02-08T02:32:38.848Z
tags: 
editor: markdown
dateCreated: 2023-02-08T02:32:37.165Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot and Event-Driven Architecture with Kafka***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-event-driven-architecture-with-kafka)
{.links-list}


# Spring Boot 和 Kafka 的事件驱动架构

事件驱动架构 (EDA) 是一种流行的设计模式，用于构建可扩展的高性能应用程序。在事件驱动系统中，事件由用户或系统组件在事件发生时生成。然后将这些事件传播到对它们感兴趣的组件，以便它们可以采取适当的操作。

Kafka 是一种流行的开源流媒体平台，可用于构建事件驱动的架构。 Kafka 具有高度可扩展性和容错性，并提供高性能和低延迟。

在本文中，我们将了解如何使用 Spring Boot 和 Kafka 构建事件驱动架构。我们还将了解如何使用 Spring Cloud Stream 来简化事件驱动微服务的开发。

## 设置卡夫卡

在我们开始开发我们的事件驱动架构之前，我们需要设置一个 Kafka 代理。 Kafka 可从 [Confluent 网站](https://www.confluent.io/download/) 下载。

下载并解压缩 Kafka 后，您可以通过运行以下命令启动代理：

```
bin/kafka-server-start.sh config/server.properties
```

## 创建一个 Spring Boot 项目

我们将使用 Spring Boot 来简化微服务的开发。 Spring Boot 可以轻松创建独立的、生产级的基于 Spring 的应用程序。

我们可以使用 [Spring Initializr](https://start.spring.io/) 来创建一个新的 Spring Boot 项目。我们需要选择以下依赖项：

- 网络
- 云流
- 卡夫卡流

![Spring Initializr](https://i.imgur.com/RgC5koh.png)

生成项目后，我们可以将其导入到我们选择的 IDE 中。

## 开发生产者

我们的事件驱动架构将由生成事件的生产者和处理这些事件的消费者组成。我们将从开发生产者开始。

生产者将是一个简单的 Spring Boot 应用程序，它公开了一个 REST 端点。当调用此端点时，它将生成一个事件并将其发送到 Kafka 主题。

首先，我们需要创建一个新的 Kafka 主题。我们可以使用 Kafka CLI 来做到这一点：

```
bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --topic events --partitions 1 --replication-factor 1
```

接下来，我们将创建一个 Spring Cloud Stream 绑定，它将事件发送到我们的 Kafka 主题。此绑定将在 application.yml 文件中定义：

```yaml
spring:
  cloud:
    stream:
      bindings:
        output:
          destination: events
          content-type: application/json
```

现在我们可以创建我们的 Spring Boot 控制器。该控制器将公开一个可用于生成事件的“/events”端点：

```java
@RestController
public class EventController {

    @Autowired
    private MessageChannel output;

    @PostMapping("/events")
    public void publishEvent(@RequestBody Event event) {
        output.send(MessageBuilder.withPayload(event).build());
    }
}
```

该控制器使用“@RestController”注释以指示它公开 REST 端点。它还注入一个用于向 Kafka 主题发送消息的“MessageChannel”bean。

最后，我们需要定义我们的“事件”类。此类将用于表示生产者生成的事件：

```java
public class Event {

    private String id;
    private String data;

    // Getters and setters
}
```

## 开发消费者

现在我们已经开发了生产者，我们可以继续开发消费者。

消费者将是一个 Spring Cloud Stream 应用程序，它使用 Kafka Streams 来处理发送到 Kafka 主题的事件。

首先，我们将创建一个 Spring Cloud Stream 绑定，它将接收来自 Kafka 主题的事件。此绑定将在 application.yml 文件中定义：

```yaml
spring:
  cloud:
    stream:
      bindings:
        input:
          destination: events
          content-type: application/json
```

接下来，我们将创建一个 Kafka Streams 拓扑来处理事件。此拓扑将在“EventStreamsConfig”类中定义：

```java
@Configuration
public class EventStreamsConfig {

    @Bean
    public Topology buildTopology(StreamsBuilder builder) {
        // ...
    }
}
```

`buildTopology()` 方法接受 `StreamsBuilder` 作为参数。我们可以使用这个构建器来构建我们的拓扑。

在我们的拓扑中，我们将创建一个从 Kafka 主题读取的事件流。然后我们将使用 Kafka Streams 处理器处理这个流。该处理器将从事件中提取数据并将其打印到控制台：

```java
@Configuration
public class EventStreamsConfig {

    @Bean
    public Topology buildTopology(StreamsBuilder builder) {
        Stream<Event> stream = builder.stream("events", Consumed.with(Serdes.String(), new JsonSerde<>(Event.class)));
        stream.process(new ProcessorSupplier<String, Event>() {
            @Override
            public Processor<String, Event> get() {
                return new Processor<String, Event>() {
                    private ProcessorContext context;

                    @Override
                    public void init(ProcessorContext context) {
                        this.context = context;
                    }

                    @Override
                    public void process(String key, Event event) {
                        String data = event.getData();
                        System.out.println(data);
                    }

                    @Override
                    public void close() {
                    }
                };
            }
        });

        return builder.build();
    }
}
```

在此拓扑中，我们使用“JsonSerde”来序列化和反序列化事件。如果我们想使用纯文本事件，我们可以选择使用 StringSerde。

现在我们已经开发了消费者，我们可以启动它并通过向 Kafka 主题发送一些事件来测试它。我们可以使用 Kafka CLI 来产生事件：

```
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic events
```

然后，在生产者中，我们可以输入一些 JSON 事件数据：

```json
{"id":"1","data":"Hello, world!"}
```

如果我们检查消费者的日志，我们应该看到我们输入的事件数据：

```
Hello, world!
```

## 结论

在本文中，我们了解了如何使用 Spring Boot 和 Kafka 构建事件驱动架构。我们还了解了如何使用 Spring Cloud Stream 来简化事件驱动微服务的开发。