---
title: 042: Spring Boot 및 Apache Flink를 사용하여 실시간 분석 애플리케이션 구축
description: 
published: true
date: 2023-02-04T08:32:44.414Z
tags: 
editor: markdown
dateCreated: 2023-02-04T08:32:42.743Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [042: Building a real-time analytics application using Spring Boot and Apache Flink***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/042-building-a-real-time-analytics-application-using-spring-boot-and-apache-flink)
{.links-list}


# 042: Spring Boot 및 Apache Flink를 사용하여 실시간 분석 애플리케이션 구축

이 게시물에서는 Spring Boot 및 Apache Flink를 사용하여 실시간 분석 애플리케이션을 빌드하는 방법을 보여줍니다.

Apache Flink는 강력한 스트리밍 분석 기능을 갖춘 오픈 소스 스트림 처리 프레임워크입니다. 배치 데이터와 스트리밍 데이터를 모두 처리할 수 있으며 변환, 집계 및 기간 설정을 위한 풍부한 연산자 집합이 있습니다.

Spring Boot는 웹 애플리케이션 구축에 널리 사용되는 Java 프레임워크입니다. "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다.

이 두 가지 기술을 함께 사용하면 실시간으로 데이터를 처리할 수 있는 애플리케이션을 구축할 수 있습니다.

## 프로젝트 설정

가장 먼저 해야 할 일은 새 Spring Boot 프로젝트를 만드는 것입니다. Spring Initializr를 사용하여 이를 수행할 수 있습니다.

프로젝트를 만든 후에는 `pom.xml`에 다음 종속성을 추가해야 합니다.

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

`flink-streaming-java_2.11` 종속성은 Java용 Apache Flink 스트리밍 API입니다. `flink-connector-kafka_2.11` 종속성은 Apache Flink용 Kafka 커넥터로, Kafka 주제에서 데이터를 읽고 쓸 수 있습니다.

## 카프카 생산자 만들기

Kafka 주제에서 데이터를 읽으려면 먼저 Kafka 생산자를 만들어야 합니다. Kafka 프로듀서는 Kafka 주제에 데이터를 쓰는 프로그램입니다.

우리의 경우에는 난수를 생성하고 Kafka 주제에 쓰는 간단한 Kafka 생산자를 만들 것입니다.

먼저 새 Java 클래스를 만들고 `@Component`로 주석을 추가해야 합니다. 이 주석은 이것이 다른 구성 요소에 주입될 수 있는 구성 요소임을 Spring에 알려줍니다.

```java
@Component
public class RandomNumberProducer {

}
```

다음으로 `KafkaTemplate`을 생산자에 주입해야 합니다. 'KafkaTemplate'은 Kafka 생산자 API를 둘러싼 Spring 래퍼로, Spring 애플리케이션에서 Kafka로 작업하기가 더 쉬워집니다.

```java
@Autowired
private KafkaTemplate<String, String> kafkaTemplate;
```

이제 난수를 생성하고 Kafka 주제로 보내는 방법을 작성할 수 있습니다. 이 메서드를 `generateAndSendRandomNumber`라고 합니다.

```java
public void generateAndSendRandomNumber() {
    String randomNumber = String.valueOf(ThreadLocalRandom.current().nextInt(0, 100));
    kafkaTemplate.send("random-numbers", randomNumber);
}
```

이 메소드는 0에서 100 사이의 난수를 생성하여 'random-numbers' Kafka 토픽으로 보냅니다.

## Kafka 소비자 만들기

이제 Kafka 생산자가 있으므로 Kafka 소비자를 만들어야 합니다. Kafka 소비자는 Kafka 주제에서 데이터를 읽는 프로그램입니다.

우리의 경우에는 `random-numbers` Kafka 주제에서 데이터를 읽고 콘솔에 인쇄하는 간단한 Kafka 소비자를 만들 것입니다.

먼저 새 Java 클래스를 만들고 `@Component`로 주석을 추가해야 합니다. 이 주석은 이것이 다른 구성 요소에 주입될 수 있는 구성 요소임을 Spring에 알려줍니다.

```java
@Component
public class RandomNumberConsumer {

}
```

다음으로 소비자에게 `FlinkKafkaConsumer011`을 주입해야 합니다. 'FlinkKafkaConsumer011'은 Kafka 주제에서 데이터를 읽을 수 있는 Apache Flink용 Kafka 커넥터입니다.

```java
@Autowired
private FlinkKafkaConsumer011<String> flinkKafkaConsumer;
```

이제 'random-numbers' Kafka 주제에서 데이터를 소비하고 콘솔에 출력하는 방법을 작성할 수 있습니다. 이 메서드를 `consumeAndPrintRandomNumbers`라고 합니다.

```java
public void consumeAndPrintRandomNumbers() {
    DataStream<String> stream = env
            .addSource(flinkKafkaConsumer.setStartFromEarliest()
                    .setTopic("random-numbers")
                    .setConsumerGroup("random-number-consumer"));

    stream.print();
}
```

이 메서드는 `random-numbers` Kafka 주제에서 데이터를 읽고 콘솔에 출력합니다.

## Flink 작업 생성

이제 Kafka 생산자와 Kafka 소비자가 있으므로 이들을 하나로 묶는 Flink 작업을 생성해야 합니다.

Flink 작업은 하나 이상의 소스에서 데이터를 읽고, 하나 이상의 변환을 적용하고, 결과를 하나 이상의 싱크에 쓰는 프로그램입니다.

우리의 경우에는 `random-numbers` Kafka 주제에서 데이터를 읽고 `map` 변환을 적용하여 숫자를 제곱하고 결과를 `random-numbers-squared ` 카프카 주제.

먼저 새 Java 클래스를 만들고 `@Component`로 주석을 추가해야 합니다. 이 주석은 이것이 다른 구성 요소에 주입될 수 있는 구성 요소임을 Spring에 알려줍니다.

```java
@Component
public class RandomNumberSquarer {

}
```

다음으로 `StreamExecutionEnvironment`를 작업에 주입해야 합니다. `StreamExecutionEnvironment`는 모든 Apache Flink 스트림 처리 프로그램의 진입점입니다.

```java
@Autowired
private StreamExecutionEnvironment env;
```

이제 Flink 작업을 생성하고 실행하는 메서드를 작성할 수 있습니다. 이 메서드를 `squareRandomNumbers`라고 합니다.

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

이 메서드는 `random-numbers` Kafka 토픽에서 데이터를 읽고 `map` 변환을 적용하여 숫자를 제곱한 다음 결과를 `random-numbers-squared` Kafka 토픽에 씁니다.

## 함께 모아서

이제 Kafka 생산자, Kafka 소비자 및 Flink 작업이 있으므로 모두 함께 연결해야 합니다.

새로운 Spring Boot 애플리케이션을 생성하고 `@EnableScheduling`으로 주석을 달아 이를 수행할 수 있습니다. 이 주석은 이 애플리케이션에 대한 스케줄링을 활성화하도록 Spring에 지시합니다.

```java
@SpringBootApplication
@EnableScheduling
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

다음으로, 새로운 `@Configuration` 클래스를 생성하고 `@EnableKafka`로 주석을 추가해야 합니다. 이 주석은 이 애플리케이션에 대해 Kafka를 활성화하도록 Spring에 지시합니다.

```java
@Configuration
@EnableKafka
public class KafkaConfiguration {

}
```

이제 `Properties` 유형의 `@Bean`을 만들고 `@Value`로 주석을 달 수 있습니다. 이 빈은 Kafka 생산자와 소비자를 구성하는 데 사용됩니다.

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

마지막으로 `generateAndSendRandomNumber` 및 `squareRandomNumbers` 메소드를 호출하는 `@Scheduled` 메소드를 생성해야 합니다. 이 메서드는 매초마다 호출되며 실시간으로 난수를 생성하고 제곱합니다.

```java
@Scheduled(fixedRate = 1000)
public void schedule() {
    randomNumberProducer.generateAndSendRandomNumber();
    randomNumberSquarer.squareRandomNumbers();
}
```

## 애플리케이션 실행

이제 애플리케이션을 구성했으므로 간단히 `main` 메서드를 실행하여 실행할 수 있습니다.

애플리케이션이 시작되어 실행되면 콘솔에 다음 출력이 표시되어야 합니다.

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

이 출력은 Kafka 생산자가 생성하는 난수를 제곱하는 Flink 작업의 결과를 보여줍니다.

## 결론

이 게시물에서는 Spring Boot 및 Apache Flink를 사용하여 실시간 분석 애플리케이션을 빌드하는 방법을 보여주었습니다. 또한 Kafka 생산자, Kafka 소비자 및 Flink 작업을 함께 연결하여 데이터를 실시간으로 처리하는 방법도 보여 주었습니다.