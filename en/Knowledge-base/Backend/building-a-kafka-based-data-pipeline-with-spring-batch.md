---
title: Building a Kafka-based data pipeline with Spring Batch
description: 
published: true
date: 2023-01-29T17:08:58.906Z
tags: 
editor: markdown
dateCreated: 2023-01-29T17:08:58.906Z
---


# Introduction

In this post, we'll explore how to build a data pipeline using Kafka and Spring Batch. We'll start by setting up a Kafka broker and creating a Kafka producer to generate some data. Next, we'll create a Spring Batch job to consume the data from Kafka and store it in a database. Finally, we'll create a Spring Batch job to read from the database and write to a file.

# Setting up Kafka

The first step is to set up a Kafka broker. We'll use Docker to run Kafka in a container. First, we'll create a Docker Compose file to define the services we'll need:

```yaml
version: '2'

services:
  zookeeper:
    image: wurstmeister/zookeeper
    ports:
      - "2181:2181"
  kafka:
    image: wurstmeister/kafka
    ports:
      - "9092:9092"
    environment:
      KAFKA_ADVERTISED_HOST_NAME: kafka
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
```

Now we can start up our Kafka broker by running `docker-compose up`.

# Creating a Kafka Producer

Now that our Kafka broker is up and running, we can create a Kafka producer to generate some data. We'll use the Kafka command line tools to do this. First, we'll create a topic:

```
kafka-topics --create --zookeeper zookeeper:2181 --replication-factor 1 --partitions 1 --topic test
```

Next, we'll start a producer and produce some messages:

```
kafka-console-producer --broker-list kafka:9092 --topic test
```

In the console, type some messages and press enter. You should see the messages appear in the producer output.

# Creating a Spring Batch Job to Consume from Kafka

Now that we have a Kafka producer up and running, we can create a Spring Batch job to consume the data. We'll start by creating a Spring Boot application:

```java
@SpringBootApplication
public class KafkaBatchApplication {

    public static void main(String[] args) {
        SpringApplication.run(KafkaBatchApplication.class, args);
    }
}
```

Next, we'll add the `spring-kafka` dependency to our `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.kafka</groupId>
    <artifactId>spring-kafka</artifactId>
</dependency>
```

Now we can create a Spring Batch job to consume from Kafka. We'll start by creating a `KafkaItemReader`:

```java
@Bean
public KafkaItemReader<String> kafkaItemReader() {
    Map<String, Object> configs = new HashMap<>();
    configs.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, "kafka:9092");
    configs.put(ConsumerConfig.GROUP_ID_CONFIG, "test-group");
    configs.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
    configs.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);

    KafkaItemReader<String> reader = new KafkaItemReader<>();
    reader.setKafkaTemplate(kafkaTemplate());
    reader.setTopic("test");
    reader.setConsumerProperties(configs);
    reader.setVerifyMode(VerifyMode.NONE);

    return reader;
}
```

This reader will consume messages from the `test` topic and deserialize them as strings.

Next, we'll create a `KafkaItemWriter`:

```java
@Bean
public KafkaItemWriter<String> kafkaItemWriter() {
    Map<String, Object> configs = new HashMap<>();
    configs.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, "kafka:9092");
    configs.put(ProducerConfig.ACKS_CONFIG, "all");
    configs.put(ProducerConfig.RETRIES_CONFIG, 0);
    configs.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class);
    configs.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class);

    KafkaItemWriter<String> writer = new KafkaItemWriter<>();
    writer.setKafkaTemplate(kafkaTemplate());
    writer.setTopic("test");
    writer.setProducerProperties(configs);

    return writer;
}
```

This writer will write the messages it receives to the `test` topic.

Finally, we'll create a `KafkaTransactionManager`:

```java
@Bean
public KafkaTransactionManager kafkaTransactionManager() {
    KafkaTransactionManager transactionManager = new KafkaTransactionManager();
    transactionManager.setKafkaOperations(kafkaTemplate());
    transactionManager.setTransactionSynchronization(AbstractPlatformTransactionManager.SYNCHRONIZATION_ON_ACTUAL_TRANSACTION);

    return transactionManager;
}
```

This transaction manager will be used to manage the transactions for our Kafka producer.

Now we can create our batch job:

```java
@Bean
public Job kafkaJob() {
    return jobBuilderFactory.get("kafkaJob")
            .start(kafkaStep())
            .build();
}

@Bean
public Step kafkaStep() {
    return stepBuilderFactory.get("kafkaStep")
            .<String, String>chunk(10)
            .reader(kafkaItemReader())
            .writer(kafkaItemWriter())
            .transactionManager(kafkaTransactionManager())
            .build();
}
```

This job will read messages from Kafka, process them, and write them back to Kafka.

# Creating a Spring Batch Job to Read from a Database

Now that we have a job that writes data to a database, we can create a job that reads from the database. We'll start by adding the `spring-boot-starter-data-jpa` dependency to our `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

Next, we'll create a `DataSource`:

```java
@Bean
public DataSource dataSource() {
    return DataSourceBuilder.create()
            .url("jdbc:mysql://localhost/test")
            .username("root")
            .password("password")
            .driverClassName("com.mysql.jdbc.Driver")
            .build();
}
```

This datasource will be used by our batch job to connect to the database.

Now we can create our batch job:

```java
@Bean
public Job databaseJob() {
    return jobBuilderFactory.get("databaseJob")
            .start(databaseStep())
            .build();
}

@Bean
public Step databaseStep() {
    return stepBuilderFactory.get("databaseStep")
            .<String, String>chunk(10)
            .reader(databaseItemReader())
            .writer(databaseItemWriter())
            .build();
}
```

This job will read messages from the database, process them, and write them to a file.

# Conclusion

In this post, we've seen how to build a data pipeline using Kafka and Spring Batch. We've started by setting up a Kafka broker and creating a Kafka producer to generate some data. Next, we've created a Spring Batch job to consume the data from Kafka and store it in a database. Finally, we've created a Spring Batch job to read from the database and write to a file.