---
title: 026: Working with Spring Boot and Apache Kafka
description: 
published: true
date: 2023-02-03T18:32:26.962Z
tags: 
editor: markdown
dateCreated: 2023-02-03T18:32:22.000Z
---

- [026: Trabajar con Spring Boot y Apache Kafka***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/026-working-with-spring-boot-and-apache-kafka)
{.links-list}
- [026：使用 Spring Boot 和 Apache Kafka***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/026-working-with-spring-boot-and-apache-kafka)
{.links-list}
- [026: Spring Boot와 Apache Kafka로 작업하기***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/026-working-with-spring-boot-and-apache-kafka)
{.links-list}


# Working with Spring Boot and Apache Kafka

In this post, we'll take a look at how to work with Spring Boot and Apache Kafka. We'll cover the following topics:

- What is Apache Kafka?
- What is Spring Boot?
- How to use Spring Boot with Apache Kafka
- Additional Information
- Warnings
- Dangers

## What is Apache Kafka?

Apache Kafka is a distributed streaming platform. It is used for building real-time data pipelines and streaming apps. It is horizontally scalable, fault-tolerant, and fast.

Kafka is written in Scala and Java. It has a publish-subscribe messaging model. It is a high-performance system.

## What is Spring Boot?

Spring Boot is a Java-based framework used to create microservices. It is used to simplify the bootstrapping and development of a new Spring application.

Spring Boot is opinionated. It provides a set of default configurations. It makes it easy to create stand-alone, production-grade Spring-based applications.

## How to use Spring Boot with Apache Kafka

In order to use Spring Boot with Apache Kafka, we need to add the following dependency to our project:

```xml
<dependency>
    <groupId>org.springframework.kafka</groupId>
    <artifactId>spring-kafka</artifactId>
</dependency>
```

We also need to add the following dependency if we want to use Apache Kafka with Avro:

```xml
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-avro-serializer</artifactId>
</dependency>
```

Now that we have the dependencies in place, let's take a look at how to use Spring Boot with Apache Kafka.

### Configuration

First, we need to configure the Apache Kafka broker. We can do this by setting the following properties in our application.properties file:

```properties
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.producer.retries=0
spring.kafka.producer.batch-size=16384
spring.kafka.producer.buffer-memory=33554432
spring.kafka.consumer.group-id=test
spring.kafka.consumer.auto-offset-reset=earliest
spring.kafka.consumer.enable-auto-commit=false
```

In the above configuration, we are setting the following properties:

- The Apache Kafka broker address
- The number of retries for the producer
- The producer batch size
- The producer buffer memory
- The consumer group id
- The consumer auto offset reset
- The consumer auto commit

### Producer

Now let's take a look at how to create a producer. We can do this by creating a Producer class:

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

In the above producer, we are using the KafkaTemplate to send messages to the Kafka broker.

### Consumer

Now let's take a look at how to create a consumer. We can do this by creating a Consumer class:

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

In the above consumer, we are using the @KafkaListener annotation to listen for messages on the "test" topic.

## Additional Information

- Spring Boot: https://spring.io/projects/spring-boot
- Apache Kafka: https://kafka.apache.org/

## Warnings

- Make sure to add the Apache Kafka broker address to the application.properties file.
- Make sure to add the spring-kafka dependency to the project.

## Dangers

- Do not commit offset manually in the consumer.