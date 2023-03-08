---
title: 082: Integrating Spring Boot with Apache Kafka for Streaming Data
description: 
published: true
date: 2023-02-02T22:24:18.470Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:24:13.703Z
---

- [082: Integración de Spring Boot con Apache Kafka para transmisión de datos***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/082-integrating-spring-boot-with-apache-kafka-for-streaming-data)
{.links-list}
- [082：将 Spring Boot 与 Apache Kafka 集成用于流数据***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/082-integrating-spring-boot-with-apache-kafka-for-streaming-data)
{.links-list}
- [082: 데이터 스트리밍을 위해 Apache Kafka와 Spring Boot 통합***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/082-integrating-spring-boot-with-apache-kafka-for-streaming-data)
{.links-list}


# 082: Integrating Spring Boot with Apache Kafka for Streaming Data

In this post, we'll take a look at how to integrate Spring Boot with Apache Kafka for streaming data. Apache Kafka is a popular open source streaming platform that can be used to build scalable, high-throughput, and low-latency streaming applications. Spring Boot is a popular Java-based framework that can be used to create stand-alone, production-grade Spring-based applications.

Integrating Spring Boot with Apache Kafka can provide several benefits, including:

- The ability to process large amounts of data in a scalable and efficient manner
- The ability to build event-driven applications
- The ability to integrate with other systems and services in a loosely coupled manner

## Prerequisites

Before we get started, there are a few things that you'll need in order to follow along with this post:

- A Java development environment
- Apache Maven
- An Apache Kafka development environment

## Setting up a Spring Boot Project

The first thing we need to do is to set up a Spring Boot project. We can do this using the Spring Initializr. For this post, we'll be using the following settings:

- Project: Maven Project
- Language: Java
- Spring Boot: 2.1.0
- Group: com.example
- Artifact: kafka-streams
- Name: kafka-streams
- Description: A Kafka Streams example
- Package Name: com.example.kafka.streams
- Packaging: Jar
- Java Version: 1.8
- Dependencies: Web, Lombok, Apache Kafka Streams

Once you have the project set up, you should have a directory structure that looks something like this:

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

## Configuring Spring Boot for Apache Kafka

Now that we have a Spring Boot project set up, we need to configure it to work with Apache Kafka. We can do this by adding the following properties to the `application.properties` file:

```
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.streams.properties.application.id=streams-demo
spring.kafka.streams.properties.commit.interval.ms=1000
spring.kafka.streams.properties.default.key.serde=org.apache.kafka.common.serialization.Serdes$StringSerde
spring.kafka.streams.properties.default.value.serde=org.apache.kafka.common.serialization.Serdes$StringSerde
```

Let's take a look at what each of these properties does:

- `spring.kafka.bootstrap-servers`: This property is used to configure the Kafka brokers that the application will connect to.
- `spring.kafka.streams.properties.application.id`: This property is used to configure the unique identifier for the Kafka Streams application.
- `spring.kafka.streams.properties.commit.interval.ms`: This property is used to configure the frequency with which Kafka Streams will commit offsets.
- `spring.kafka.streams.properties.default.key.serde`: This property is used to configure the default key serde for Kafka Streams.
- `spring.kafka.streams.properties.default.value.serde`: This property is used to configure the default value serde for Kafka Streams.

## Creating a Kafka Streams Application

Now that our project is set up and configured, we can start writing our Kafka Streams application. We'll start by creating a new class called `KafkaStreamsApplication`. This class will extend the `org.springframework.boot.SpringApplication` class and annotated with the `@SpringBootApplication` annotation:

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

The `@SpringBootApplication` annotation is a convenience annotation that is used to configure a Spring Boot application. It is equivalent to using the following annotations:

- `@Configuration`: This annotation is used to indicate that a class contains Spring Boot configuration.
- `@EnableAutoConfiguration`: This annotation is used to enable Spring Boot's auto-configuration feature.
- `@ComponentScan`: This annotation is used to enable Spring component scanning.

## Creating a Kafka Streams Topology

Now that we have our `KafkaStreamsApplication` class set up, we can start writing our Kafka Streams topology. A Kafka Streams topology is a directed graph of stream processing nodes. In our topology, we'll have two nodes: a source node and a sink node.

The source node will read data from an input topic and the sink node will write the data to an output topic. We can create our topology by annotating the `KafkaStreamsApplication` class with the `@EnableKafkaStreams` annotation:

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

Let's take a look at what each of these annotations and methods do:

- `@EnableKafkaStreams`: This annotation is used to enable Kafka Streams in a Spring Boot application.
- `@Value("${spring.kafka.bootstrap-servers}")`: This annotation is used to inject the `spring.kafka.bootstrap-servers` property into the `bootstrapServers` field.
- `@Value("${spring.kafka.streams.properties.application.id}")`: This annotation is used to inject the `spring.kafka.streams.properties.application.id` property into the `applicationId` field.
- `@Value("${spring.kafka.streams.properties.commit.interval.ms}")`: This annotation is used to inject the `spring.kafka.streams.properties.commit.interval.ms` property into the `commitIntervalMs` field.
- `@Value("${spring.kafka.streams.properties.default.key.serde}")`: This annotation is used to inject the `spring.kafka.streams.properties.default.key.serde` property into the `defaultKeySerde` field.
- `@Value("${spring.kafka.streams.properties.default.value.serde}")`: This annotation is used to inject the `spring.kafka.streams.properties.default.value.serde` property into the `defaultValueSerde` field.
- `public static void main(String[] args)`: This is the main method of the `KafkaStreamsApplication` class. This method is used to start the Spring Boot application.
- `@Bean`: This annotation is used to indicate that a method produces a bean that can be injected into other Spring-managed beans.
- `StreamsBuilderFactoryBeanCustomizer streamsBuilderFactoryBeanCustomizer()`: This method is used to create a `StreamsBuilderFactoryBeanCustomizer` bean. This bean is used to customize the `StreamsBuilderFactoryBean`.
- `public void customize(StreamsBuilderFactoryBean streamsBuilderFactoryBean)`: This is the `customize` method of the `StreamsBuilderFactoryBeanCustomizer` interface. This method is used to customize the `StreamsBuilderFactoryBean`.
- `streamsBuilderFactoryBean.setBootstrapServers(bootstrapServers);`: This line is used to set the bootstrap servers for the `StreamsBuilderFactoryBean`.
- `streamsBuilderFactoryBean.setApplicationId(applicationId);`: This line is used to set the application id for the `StreamsBuilderFactoryBean`.
- `streamsBuilderFactoryBean.setCommitInterval(Long.parseLong(commitIntervalMs));`: This line is used to set the commit interval for the `StreamsBuilderFactoryBean`.
- `streamsBuilderFactoryBean.setDefaultKeySerde(Serdes.String());`: This line is used to set the default key serde for the `StreamsBuilderFactoryBean`.
- `streamsBuilderFactoryBean.setDefaultValueSerde(Serdes.String());`: This line is used to set the default value serde for the `StreamsBuilderFactoryBean`.
- `@Bean`: This annotation is used to indicate that a method produces a bean that can be injected into other Spring-managed beans.
- `KStream<String, String> kStream(StreamsBuilder kStreamBuilder)`: This method is used to create a `KStream` bean. This bean is used to represent the stream processing topology.
- `KStream<String, String> stream = kStreamBuilder.stream("input-topic");`: This line is used to create a `KStream` from the input topic.
- `stream.to("output-topic");`: This line is used to write the data from the `KStream` to the output topic.
- `return stream;`: This line is used to return the `KStream`.

## Building and Running the Application

Now that we have our application written, we can build and run it. We can do this by running the following command:

```
mvn spring-boot:run
```

Once the application is up and running, we can start producing and consuming messages from the input and output topics.

## Conclusion

In this post, we've taken a look at how to integrate Spring Boot with Apache Kafka for streaming data. We've also seen how to create a Kafka Streams topology and run it in a Spring Boot application.