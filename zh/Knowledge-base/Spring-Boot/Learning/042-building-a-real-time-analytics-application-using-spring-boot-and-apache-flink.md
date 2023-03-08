---
title: 042：使用 Spring Boot 和 Apache Flink 构建实时分析应用程序
description: 
published: true
date: 2023-02-04T08:32:44.391Z
tags: 
editor: markdown
dateCreated: 2023-02-04T08:32:42.746Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [042: Building a real-time analytics application using Spring Boot and Apache Flink***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/042-building-a-real-time-analytics-application-using-spring-boot-and-apache-flink)
{.links-list}


# 042：使用 Spring Boot 和 Apache Flink 构建实时分析应用程序

在本文中，我们将向您展示如何使用 Spring Boot 和 Apache Flink 构建实时分析应用程序。

Apache Flink 是一个开源流处理框架，具有强大的流分析功能。它可以处理批处理和流数据，并有一组丰富的转换、聚合和窗口操作符。

Spring Boot 是一种用于构建 Web 应用程序的流行 Java 框架。它使您可以轻松创建独立的、生产级的基于 Spring 的应用程序，您可以“直接运行”。

当一起使用时，这两种技术可用于构建可以实时处理数据的应用程序。

## 设置你的项目

您需要做的第一件事是创建一个新的 Spring Boot 项目。您可以使用 Spring Initializr 执行此操作。

创建项目后，您需要将以下依赖项添加到 `pom.xml`：

```xml
<dependencies>
    <dependency>
        <groupId>org.apache.flink</groupId>
        <artifactId>flink-streaming-java_2.11</artifactId>
        <version>1.8.0</version>
    </dependency>
    <dependency>
        <groupId>org.apache.flink</groupId>
        <artifactId>flink-connector-kafka_2.11</artifactId>
        <version>1.8.0</version>
    </dependency>
</dependencies>
```

`flink-streaming-java_2.11` 依赖项是 Apache Flink streaming API for Java。 `flink-connector-kafka_2.11` 依赖项是 Apache Flink 的 Kafka 连接器，它允许您从 Kafka 主题读取数据和写入数据。

## 创建 Kafka 生产者

为了从 Kafka 主题中读取数据，我们首先需要创建一个 Kafka 生产者。 Kafka 生产者是一个将数据写入 Kafka 主题的程序。

在我们的例子中，我们将创建一个简单的 Kafka 生产者，它生成随机数并将它们写入 Kafka 主题。

首先，我们需要创建一个新的 Java 类并用 @Component 注释它。这个注解告诉 Spring 这是一个可以注入到其他组件中的组件。

```java
@Component
public class RandomNumberProducer {

}
```

接下来，我们需要将一个 `KafkaTemplate` 注入到我们的生产者中。 `KafkaTemplate` 是围绕 Kafka 生产者 API 的 Spring 包装器，它使在 Spring 应用程序中使用 Kafka 变得更加容易。

```java
@Autowired
private KafkaTemplate<String, String> kafkaTemplate;
```

现在我们可以编写一个方法来生成随机数并将其发送到 Kafka 主题。我们将此方法称为“generateAndSendRandomNumber”。

```java
public void generateAndSendRandomNumber() {
    String randomNumber = String.valueOf(ThreadLocalRandom.current().nextInt(0, 100));
    kafkaTemplate.send("random-numbers", randomNumber);
}
```

此方法生成一个介于 0 和 100 之间的随机数，并将其发送到 `random-numbers` Kafka 主题。

## 创建一个 Kafka 消费者

现在我们有了一个 Kafka 生产者，我们需要创建一个 Kafka 消费者。 Kafka 消费者是一个从 Kafka 主题读取数据的程序。

在我们的例子中，我们将创建一个简单的 Kafka 消费者，它从 `random-numbers` Kafka 主题中读取数据并将其打印到控制台。

首先，我们需要创建一个新的 Java 类并用 @Component 注释它。这个注解告诉 Spring 这是一个可以注入到其他组件中的组件。

```java
@Component
public class RandomNumberConsumer {

}
```

接下来，我们需要将“FlinkKafkaConsumer011”注入我们的消费者。 `FlinkKafkaConsumer011` 是 Apache Flink 的 Kafka 连接器，它允许您从 Kafka 主题读取数据。

```java
@Autowired
private FlinkKafkaConsumer011<String> flinkKafkaConsumer;
```

现在我们可以编写一个方法来使用 `random-numbers` Kafka 主题中的数据并将其打印到控制台。我们将此方法称为“consumeAndPrintRandomNumbers”。

```java
public void consumeAndPrintRandomNumbers() {
    DataStream<String> stream = env
            .addSource(flinkKafkaConsumer.setStartFromEarliest()
                    .setTopic("random-numbers")
                    .setConsumerGroup("random-number-consumer"));

    stream.print();
}
```

此方法从 `random-numbers` Kafka 主题读取数据，并将其打印到控制台。

## 创建 Flink 作业

现在我们有了一个 Kafka 生产者和一个 Kafka 消费者，我们需要创建一个 Flink 作业将它们联系在一起。

Flink 作业是一种从一个或多个源读取数据、应用一个或多个转换并将结果写入一个或多个接收器的程序。

在我们的例子中，我们将创建一个简单的 Flink 作业，它从“随机数”Kafka 主题读取数据，应用“映射”转换对数字进行平方，并将结果写入“随机数平方” `卡夫卡主题。

首先，我们需要创建一个新的 Java 类并用 @Component 注释它。这个注解告诉 Spring 这是一个可以注入到其他组件中的组件。

```java
@Component
public class RandomNumberSquarer {

}
```

接下来，我们需要将一个“StreamExecutionEnvironment”注入到我们的工作中。 `StreamExecutionEnvironment` 是所有 Apache Flink 流处理程序的入口点。

```java
@Autowired
private StreamExecutionEnvironment env;
```

现在我们可以编写一个方法来创建和执行我们的 Flink 作业。我们将此方法称为“squareRandomNumbers”。

```java
public void squareRandomNumbers() {
    DataStream<String> stream = env
            .addSource(flinkKafkaConsumer.setStartFromEarliest()
                    .setTopic("random-numbers")
                    .setConsumerGroup("random-number-consumer"));

    stream
            .map(new MapFunction<String, String>() {
                @Override
                public String map(String value) {
                    int number = Integer.parseInt(value);
                    int square = number * number;
                    return String.valueOf(square);
                }
            })
            .addSink(new FlinkKafkaProducer011<>("random-numbers-squared", new SimpleStringSchema(), props));
}
```

此方法从 `random-numbers` Kafka 主题读取数据，应用 `map` 转换对数字进行平方，并将结果写入 `random-numbers-squared` Kafka 主题。

## 把它们放在一起

现在我们有了一个 Kafka 生产者、一个 Kafka 消费者和一个 Flink 作业，我们需要将它们连接在一起。

我们可以通过创建一个新的 Spring Boot 应用程序并使用 @EnableScheduling 对其进行注释来完成此操作。这个注释告诉 Spring 为这个应用程序启用调度。

```java
@SpringBootApplication
@EnableScheduling
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

接下来，我们需要创建一个新的 `@Configuration` 类并用 `@EnableKafka` 注释它。这个注释告诉 Spring 为这个应用程序启用 Kafka。

```java
@Configuration
@EnableKafka
public class KafkaConfiguration {

}
```

现在我们可以创建一个类型为 `Properties` 的 `@Bean` 并用 `@Value` 注释它。该 bean 将用于配置 Kafka 生产者和消费者。

```java
@Bean
@Value("${kafka.bootstrap.servers}")
public Properties props() {
    Properties props = new Properties();
    props.setProperty("bootstrap.servers", bootstrapServers);
    props.setProperty("group.id", "random-number-consumer");
    props.setProperty("enable.auto.commit", "true");
    props.setProperty("auto.commit.interval.ms", "1000");
    props.setProperty("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
    props.setProperty("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
    return props;
}
```

最后，我们需要创建一个调用 generateAndSendRandomNumber 和 squareRandomNumbers 方法的 @Scheduled 方法。该方法每秒调用一次，实时生成随机数并进行平方。

```java
@Scheduled(fixedRate = 1000)
public void schedule() {
    randomNumberProducer.generateAndSendRandomNumber();
    randomNumberSquarer.squareRandomNumbers();
}
```

## 运行你的应用程序

现在我们已经配置了我们的应用程序，我们可以通过简单地运行 `main` 方法来运行它。

应用程序启动并运行后，您应该会在控制台中看到以下输出：

```
1
4
9
16
25
36
49
64
81
100
```

此输出显示了我们的 Flink 作业的结果，该作业正在对我们的 Kafka 生产者生成的随机数进行平方。

## 结论

在本文中，我们向您展示了如何使用 Spring Boot 和 Apache Flink 构建实时分析应用程序。我们还向您展示了如何将 Kafka 生产者、Kafka 消费者和 Flink 作业连接在一起以实时处理数据。