---
title: Integrating Kafka with Spring Boot for Real-time Processing
description: 
published: true
date: 2023-01-31T20:17:25.435Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:17:24.083Z
---

- [실시간 처리를 위해 Kafka와 Spring Boot 통합***Korean** version of this document is available*](/ko/Knowledge-base/Backend/integrating-kafka-with-spring-boot-for-real-time-processing)
{.links-list}
- [リアルタイム処理のために Kafka と Spring Boot を統合する***Japanese** version of this document is available*](/ja/Knowledge-base/Backend/integrating-kafka-with-spring-boot-for-real-time-processing)
{.links-list}
- [将 Kafka 与 Spring Boot 集成以进行实时处理***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Backend/integrating-kafka-with-spring-boot-for-real-time-processing)
{.links-list}



# Introduction

In this article, we'll see how to integrate Kafka with Spring Boot to process real-time data. We'll be using a simple example to demonstrate this.

Kafka is a distributed streaming platform that can be used to publish and subscribe to streams of data. It is scalable and fault-tolerant, making it ideal for processing real-time data. Spring Boot is a popular Java framework that can be used to create microservices.

# Setting up Kafka

To run the example code, you will need to have Kafka installed. You can find instructions on how to do this here:

https://kafka.apache.org/quickstart

Once you have Kafka up and running, you can create a topic with the following command:

```
kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
```

# Spring Boot example

Now that we have Kafka set up, let's create a Spring Boot application that will publish and subscribe to messages on the "test" topic.

We'll start by creating a simple Spring Boot application with the following dependencies:

```
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.kafka</groupId>
        <artifactId>spring-kafka</artifactId>
    </dependency>
</dependencies>
```

Next, we'll create a configuration file that will contain the settings for our Kafka broker and topic:

```
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.topic.test=test
```

Now we can create a simple Kafka producer and consumer.

First, let's create a producer that will send messages to the "test" topic:

```java
@Component
public class KafkaProducer {

    private static final Logger logger = LoggerFactory.getLogger(KafkaProducer.class);

    @Autowired
    private KafkaTemplate<String, String> kafkaTemplate;

    public void send(String message) {
        logger.info("sending message='{}' to topic='{}'", message, "test");
        kafkaTemplate.send("test", message);
    }
}
```

Next, let's create a consumer that will receive messages from the "test" topic:

```java
@Component
public class KafkaConsumer {

    private static final Logger logger = LoggerFactory.getLogger(KafkaConsumer.class);

    @KafkaListener(topics = "test")
    public void receive(String message) {
        logger.info("received message='{}'", message);
    }
}
```

Now we can create a simple Spring Boot application that will use the producer and consumer we just created:

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

If we run the application and send a message to the "test" topic, we should see the message being received by the consumer:

![Screenshot of Kafka Consumer](kafka-consumer.png)

# Conclusion

In this article, we saw how to integrate Kafka with Spring Boot to process real-time data. We created a simple producer and consumer that demonstrated how to send and receive messages from a Kafka topic.