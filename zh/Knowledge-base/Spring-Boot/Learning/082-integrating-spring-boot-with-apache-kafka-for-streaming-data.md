---
title: 082：将 Spring Boot 与 Apache Kafka 集成用于流数据
description: 
published: true
date: 2023-02-02T22:24:15.395Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:24:13.689Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [082: Integrating Spring Boot with Apache Kafka for Streaming Data***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/082-integrating-spring-boot-with-apache-kafka-for-streaming-data)
{.links-list}


# 082：将 Spring Boot 与 Apache Kafka 集成用于流数据

在本文中，我们将了解如何将 Spring Boot 与 Apache Kafka 集成以处理流数据。 Apache Kafka 是一种流行的开源流媒体平台，可用于构建可扩展、高吞吐量和低延迟的流媒体应用程序。 Spring Boot 是一种流行的基于 Java 的框架，可用于创建独立的、生产级的基于 Spring 的应用程序。

将 Spring Boot 与 Apache Kafka 集成可以提供多种好处，包括：

- 以可扩展和高效的方式处理大量数据的能力
- 构建事件驱动应用程序的能力
- 以松散耦合的方式与其他系统和服务集成的能力

## 先决条件

在我们开始之前，您需要做一些事情才能跟上这篇文章：

- Java开发环境
- 阿帕奇行家
- 一个 Apache Kafka 开发环境

## 设置 Spring Boot 项目

我们需要做的第一件事是设置一个 Spring Boot 项目。我们可以使用 Spring Initializr 来做到这一点。对于这篇文章，我们将使用以下设置：

- 项目：Maven 项目
- 语言：Java
- 春季启动：2.1.0
- 组：com.example
- 神器：kafka-streams
- 名称：kafka-streams
- 描述：一个 Kafka Streams 例子
- 包名：com.example.kafka.streams
- 包装：罐
- Java 版本：1.8
- 依赖项：Web、Lombok、Apache Kafka Streams

一旦你设置了项目，你应该有一个看起来像这样的目录结构：

```
kafka-streams
├── pom.xml
└── src
    └── main
        ├── java
        │   └── com
        │       └── example
        │           └── kafka
        │               └── streams
        │                   └── KafkaStreamsApplication.java
        └── resources
            └── application.properties
```

## 为 Apache Kafka 配置 Spring Boot

现在我们已经设置了一个 Spring Boot 项目，我们需要配置它以使用 Apache Kafka。我们可以通过将以下属性添加到 application.properties 文件来实现：

```
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.streams.properties.application.id=streams-demo
spring.kafka.streams.properties.commit.interval.ms=1000
spring.kafka.streams.properties.default.key.serde=org.apache.kafka.common.serialization.Serdes$StringSerde
spring.kafka.streams.properties.default.value.serde=org.apache.kafka.common.serialization.Serdes$StringSerde
```

让我们来看看这些属性中的每一个的作用：

- `spring.kafka.bootstrap-servers`：此属性用于配置应用程序将连接到的 Kafka 代理。
- `spring.kafka.streams.properties.application.id`：此属性用于配置 Kafka Streams 应用程序的唯一标识符。
- `spring.kafka.streams.properties.commit.interval.ms`：此属性用于配置 Kafka Streams 提交偏移量的频率。
- `spring.kafka.streams.properties.default.key.serde`：此属性用于配置 Kafka Streams 的默认密钥 serde。
- `spring.kafka.streams.properties.default.value.serde`：此属性用于配置 Kafka Streams 的默认值 serde。

## 创建 Kafka 流应用程序

现在我们的项目已经设置和配置好了，我们可以开始编写我们的 Kafka Streams 应用程序了。我们将从创建一个名为“KafkaStreamsApplication”的新类开始。此类将扩展 org.springframework.boot.SpringApplication 类并使用 @SpringBootApplication 注释进行注释：

```java
package com.example.kafka.streams;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class KafkaStreamsApplication {

    public static void main(String[] args) {
        SpringApplication.run(KafkaStreamsApplication.class, args);
    }

}
```

@SpringBootApplication 注释是一个方便的注释，用于配置 Spring Boot 应用程序。相当于使用下面的注解：

- `@Configuration`：该注解用于表示一个类包含Spring Boot配置。
- `@EnableAutoConfiguration`：该注解用于启用 Spring Boot 的自动配置功能。
- `@ComponentScan`：此注解用于启用 Spring 组件扫描。

## 创建 Kafka 流拓扑

现在我们已经设置了“KafkaStreamsApplication”类，我们可以开始编写我们的 Kafka Streams 拓扑。 Kafka Streams 拓扑是流处理节点的有向图。在我们的拓扑中，我们将有两个节点：一个源节点和一个汇节点。

源节点将从输入主题读取数据，汇节点将数据写入输出主题。我们可以通过使用 `@EnableKafkaStreams` 注释注释 `KafkaStreamsApplication` 类来创建我们的拓扑：

```java
package com.example.kafka.streams;

import org.apache.kafka.common.serialization.Serdes;
import org.apache.kafka.streams.StreamsBuilder;
import org.apache.kafka.streams.kstream.KStream;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.kafka.annotation.EnableKafkaStreams;
import org.springframework.kafka.annotation.StreamsBuilderFactoryBean;
import org.springframework.kafka.config.StreamsBuilderFactoryBeanCustomizer;

@SpringBootApplication
@EnableKafkaStreams
public class KafkaStreamsApplication {

    @Value("${spring.kafka.bootstrap-servers}")
    private String bootstrapServers;

    @Value("${spring.kafka.streams.properties.application.id}")
    private String applicationId;

    @Value("${spring.kafka.streams.properties.commit.interval.ms}")
    private String commitIntervalMs;

    @Value("${spring.kafka.streams.properties.default.key.serde}")
    private String defaultKeySerde;

    @Value("${spring.kafka.streams.properties.default.value.serde}")
    private String defaultValueSerde;

    public static void main(String[] args) {
        SpringApplication.run(KafkaStreamsApplication.class, args);
    }

    @Bean
    public StreamsBuilderFactoryBeanCustomizer streamsBuilderFactoryBeanCustomizer() {
        return new StreamsBuilderFactoryBeanCustomizer() {
            @Override
            public void customize(StreamsBuilderFactoryBean streamsBuilderFactoryBean) {
                streamsBuilderFactoryBean.setBootstrapServers(bootstrapServers);
                streamsBuilderFactoryBean.setApplicationId(applicationId);
                streamsBuilderFactoryBean.setCommitInterval(Long.parseLong(commitIntervalMs));
                streamsBuilderFactoryBean.setDefaultKeySerde(Serdes.String());
                streamsBuilderFactoryBean.setDefaultValueSerde(Serdes.String());
            }
        };
    }

    @Bean
    public KStream<String, String> kStream(StreamsBuilder kStreamBuilder) {
        KStream<String, String> stream = kStreamBuilder.stream("input-topic");
        stream.to("output-topic");
        return stream;
    }

}
```

让我们看一下这些注解和方法各自的作用：

- `@EnableKafkaStreams`：此注释用于在 Spring Boot 应用程序中启用 Kafka Streams。
- `@Value("${spring.kafka.bootstrap-servers}")`：此注释用于将 `spring.kafka.bootstrap-servers` 属性注入 `bootstrapServers` 字段。
- `@Value("${spring.kafka.streams.properties.application.id}")`：此注释用于将 `spring.kafka.streams.properties.application.id` 属性注入 `applicationId`场地。
- `@Value("${spring.kafka.streams.properties.commit.interval.ms}")`：此注释用于将 `spring.kafka.streams.properties.commit.interval.ms` 属性注入到`commitIntervalMs` 字段。
- `@Value("${spring.kafka.streams.properties.default.key.serde}")`：此注释用于将 `spring.kafka.streams.properties.default.key.serde` 属性注入到`defaultKeySerde` 字段。
- `@Value("${spring.kafka.streams.properties.default.value.serde}")`：此注释用于将 `spring.kafka.streams.properties.default.value.serde` 属性注入到`defaultValueSerde` 字段。
- `public static void main(String[] args)`：这是`KafkaStreamsApplication`类的主要方法。此方法用于启动 Spring Boot 应用程序。
- `@Bean`：此注释用于指示方法生成的 bean 可以注入到其他 Spring 管理的 bean 中。
- `StreamsBuilderFactoryBeanCustomizer streamsBuilderFactoryBeanCustomizer()`：此方法用于创建 `StreamsBuilderFactoryBeanCustomizer` bean。此 bean 用于自定义 StreamsBuilderFactoryBean。
- `public void customize(StreamsBuilderFactoryBean streamsBuilderFactoryBean)`：这是 `StreamsBuilderFactoryBeanCustomizer` 接口的 `customize` 方法。此方法用于自定义 StreamsBuilderFactoryBean。
- `streamsBuilderFactoryBean.setBootstrapServers(bootstrapServers);`：此行用于为 `StreamsBuilderFactoryBean` 设置引导服务器。
- `streamsBuilderFactoryBean.setApplicationId(applicationId);`：此行用于设置 `StreamsBuilderFactoryBean` 的应用程序 ID。
- `streamsBuilderFactoryBean.setCommitInterval(Long.parseLong(commitIntervalMs));`：此行用于设置 `StreamsBuilderFactoryBean` 的提交间隔。
- `streamsBuilderFactoryBean.setDefaultKeySerde(Serdes.String());`：此行用于设置 `StreamsBuilderFactoryBean` 的默认密钥 serde。
- `streamsBuilderFactoryBean.setDefaultValueSerde(Serdes.String());`：此行用于设置 `StreamsBuilderFactoryBean` 的默认值 serde。
- `@Bean`：此注释用于指示方法生成的 bean 可以注入到其他 Spring 管理的 bean 中。
- `KStream<String, String> kStream(StreamsBuilder kStreamBuilder)`：此方法用于创建 `KStream` bean。该 bean 用于表示流处理拓扑。
- `KStream<String, String> stream = kStreamBuilder.stream("input-topic");`：这一行用于从输入主题创建一个 `KStream`。
- `stream.to("output-topic");`：这一行用于将来自 `KStream` 的数据写入输出主题。
- `return stream;`：此行用于返回 `KStream`。

## 构建和运行应用程序

现在我们已经编写了应用程序，我们可以构建并运行它。我们可以通过运行以下命令来完成此操作：

```
mvn spring-boot:run
```

一旦应用程序启动并运行，我们就可以开始生成和使用来自输入和输出主题的消息。

## 结论

在本文中，我们了解了如何将 Spring Boot 与 Apache Kafka 集成以处理流数据。我们还了解了如何创建 Kafka Streams 拓扑并在 Spring Boot 应用程序中运行它。