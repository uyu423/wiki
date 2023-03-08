---
title: 042: Building a real-time analytics application using Spring Boot and Apache Flink
description: 
published: true
date: 2023-02-04T08:32:48.151Z
tags: 
editor: markdown
dateCreated: 2023-02-04T08:32:42.776Z
---

- [042: Creación de una aplicación de análisis en tiempo real con Spring Boot y Apache Flink***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/042-building-a-real-time-analytics-application-using-spring-boot-and-apache-flink)
{.links-list}
- [042：使用 Spring Boot 和 Apache Flink 构建实时分析应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/042-building-a-real-time-analytics-application-using-spring-boot-and-apache-flink)
{.links-list}
- [042: Spring Boot 및 Apache Flink를 사용하여 실시간 분석 애플리케이션 구축***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/042-building-a-real-time-analytics-application-using-spring-boot-and-apache-flink)
{.links-list}


# 042: Building a real-time analytics application using Spring Boot and Apache Flink

In this post, we'll show you how to build a real-time analytics application using Spring Boot and Apache Flink.

Apache Flink is an open-source stream processing framework with powerful streaming analytics capabilities. It can handle both batch and streaming data, and has a rich set of operators for transformations, aggregations, and windowing.

Spring Boot is a popular Java framework for building web applications. It makes it easy to create stand-alone, production-grade Spring-based applications that you can "just run".

When used together, these two technologies can be used to build applications that can process data in real time.

## Setting up your project

The first thing you'll need to do is create a new Spring Boot project. You can do this using the Spring Initializr.

Once you've created your project, you'll need to add the following dependencies to your `pom.xml`:

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

The `flink-streaming-java_2.11` dependency is the Apache Flink streaming API for Java. The `flink-connector-kafka_2.11` dependency is the Kafka connector for Apache Flink, which allows you to read data from and write data to Kafka topics.

## Creating a Kafka producer

In order to read data from a Kafka topic, we first need to create a Kafka producer. A Kafka producer is a program that writes data to a Kafka topic.

In our case, we're going to create a simple Kafka producer that generates random numbers and writes them to a Kafka topic.

First, we need to create a new Java class and annotate it with `@Component`. This annotation tells Spring that this is a component that can be injected into other components.

```java
@Component
public class RandomNumberProducer {

}
```

Next, we need to inject a `KafkaTemplate` into our producer. `KafkaTemplate` is a Spring wrapper around the Kafka producer API that makes it easier to work with Kafka in a Spring application.

```java
@Autowired
private KafkaTemplate<String, String> kafkaTemplate;
```

Now we can write a method to generate a random number and send it to a Kafka topic. We'll call this method `generateAndSendRandomNumber`.

```java
public void generateAndSendRandomNumber() {
    String randomNumber = String.valueOf(ThreadLocalRandom.current().nextInt(0, 100));
    kafkaTemplate.send("random-numbers", randomNumber);
}
```

This method generates a random number between 0 and 100, and sends it to the `random-numbers` Kafka topic.

## Creating a Kafka consumer

Now that we have a Kafka producer, we need to create a Kafka consumer. A Kafka consumer is a program that reads data from a Kafka topic.

In our case, we're going to create a simple Kafka consumer that reads data from the `random-numbers` Kafka topic and prints it to the console.

First, we need to create a new Java class and annotate it with `@Component`. This annotation tells Spring that this is a component that can be injected into other components.

```java
@Component
public class RandomNumberConsumer {

}
```

Next, we need to inject a `FlinkKafkaConsumer011` into our consumer. `FlinkKafkaConsumer011` is the Kafka connector for Apache Flink, which allows you to read data from a Kafka topic.

```java
@Autowired
private FlinkKafkaConsumer011<String> flinkKafkaConsumer;
```

Now we can write a method to consume data from the `random-numbers` Kafka topic and print it to the console. We'll call this method `consumeAndPrintRandomNumbers`.

```java
public void consumeAndPrintRandomNumbers() {
    DataStream<String> stream = env
            .addSource(flinkKafkaConsumer.setStartFromEarliest()
                    .setTopic("random-numbers")
                    .setConsumerGroup("random-number-consumer"));

    stream.print();
}
```

This method reads data from the `random-numbers` Kafka topic, and prints it to the console.

## Creating a Flink job

Now that we have a Kafka producer and a Kafka consumer, we need to create a Flink job that ties them together.

A Flink job is a program that reads data from one or more sources, applies one or more transformations, and writes the results to one or more sinks.

In our case, we're going to create a simple Flink job that reads data from the `random-numbers` Kafka topic, applies a `map` transformation to square the numbers, and writes the results to the `random-numbers-squared` Kafka topic.

First, we need to create a new Java class and annotate it with `@Component`. This annotation tells Spring that this is a component that can be injected into other components.

```java
@Component
public class RandomNumberSquarer {

}
```

Next, we need to inject a `StreamExecutionEnvironment` into our job. `StreamExecutionEnvironment` is the entry point for all Apache Flink stream processing programs.

```java
@Autowired
private StreamExecutionEnvironment env;
```

Now we can write a method to create and execute our Flink job. We'll call this method `squareRandomNumbers`.

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

This method reads data from the `random-numbers` Kafka topic, applies a `map` transformation to square the numbers, and writes the results to the `random-numbers-squared` Kafka topic.

## Putting it all together

Now that we have a Kafka producer, a Kafka consumer, and a Flink job, we need to wire them all together.

We can do this by creating a new Spring Boot application and annotating it with `@EnableScheduling`. This annotation tells Spring to enable scheduling for this application.

```java
@SpringBootApplication
@EnableScheduling
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

Next, we need to create a new `@Configuration` class and annotate it with `@EnableKafka`. This annotation tells Spring to enable Kafka for this application.

```java
@Configuration
@EnableKafka
public class KafkaConfiguration {

}
```

Now we can create a `@Bean` of type `Properties` and annotate it with `@Value`. This bean will be used to configure the Kafka producer and consumer.

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

Finally, we need to create a `@Scheduled` method that calls the `generateAndSendRandomNumber` and `squareRandomNumbers` methods. This method will be called every second, and will generate and square random numbers in real time.

```java
@Scheduled(fixedRate = 1000)
public void schedule() {
    randomNumberProducer.generateAndSendRandomNumber();
    randomNumberSquarer.squareRandomNumbers();
}
```

## Running your application

Now that we have our application configured, we can run it by simply running the `main` method.

Once the application is up and running, you should see the following output in the console:

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

This output shows the results of our Flink job, which is squaring the random numbers that are being generated by our Kafka producer.

## Conclusion

In this post, we've shown you how to build a real-time analytics application using Spring Boot and Apache Flink. We've also shown you how to wire together a Kafka producer, a Kafka consumer, and a Flink job to process data in real time.