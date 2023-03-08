---
title: 026: Spring Boot와 Apache Kafka로 작업하기
description: 
published: true
date: 2023-02-03T18:32:23.620Z
tags: 
editor: markdown
dateCreated: 2023-02-03T18:32:21.993Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [026: Working with Spring Boot and Apache Kafka***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/026-working-with-spring-boot-and-apache-kafka)
{.links-list}


# Spring Boot와 Apache Kafka로 작업하기

이 게시물에서는 Spring Boot와 Apache Kafka를 사용하여 작업하는 방법을 살펴보겠습니다. 다음 주제를 다룹니다.

- 아파치 카프카란?
- 스프링부트란?
- Apache Kafka에서 Spring Boot를 사용하는 방법
- 추가 정보
- 경고
- 위험

## 아파치 카프카란?

Apache Kafka는 분산 스트리밍 플랫폼입니다. 실시간 데이터 파이프라인 및 스트리밍 앱을 구축하는 데 사용됩니다. 수평 확장이 가능하고 내결함성이 있으며 빠릅니다.

Kafka는 Scala와 Java로 작성되었습니다. 게시-구독 메시징 모델이 있습니다. 고성능 시스템입니다.

## 스프링부트란?

Spring Boot는 마이크로 서비스를 생성하는 데 사용되는 Java 기반 프레임워크입니다. 새 Spring 애플리케이션의 부트스트래핑 및 개발을 단순화하는 데 사용됩니다.

Spring Boot는 독단적입니다. 기본 구성 세트를 제공합니다. 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다.

## Apache Kafka에서 Spring Boot를 사용하는 방법

Apache Kafka에서 Spring Boot를 사용하려면 프로젝트에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.kafka</groupId>
    <artifactId>spring-kafka</artifactId>
</dependency>
```

또한 Avro와 함께 Apache Kafka를 사용하려면 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-avro-serializer</artifactId>
</dependency>
```

이제 종속성이 준비되었으므로 Apache Kafka에서 Spring Boot를 사용하는 방법을 살펴보겠습니다.

### 구성

먼저 Apache Kafka 브로커를 구성해야 합니다. application.properties 파일에서 다음 속성을 설정하여 이를 수행할 수 있습니다.

```properties
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.producer.retries=0
spring.kafka.producer.batch-size=16384
spring.kafka.producer.buffer-memory=33554432
spring.kafka.consumer.group-id=test
spring.kafka.consumer.auto-offset-reset=earliest
spring.kafka.consumer.enable-auto-commit=false
```

위의 구성에서 다음 속성을 설정합니다.

- Apache Kafka 브로커 주소
- 생산자의 재시도 횟수
- 생산자 배치 크기
- 생산자 버퍼 메모리
- 소비자 그룹 ID
- 소비자 자동 오프셋 재설정
- 소비자 자동 커밋

### 프로듀서

이제 생산자를 만드는 방법을 살펴보겠습니다. Producer 클래스를 생성하여 이를 수행할 수 있습니다.

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

위의 생산자에서 KafkaTemplate을 사용하여 Kafka 브로커에 메시지를 보냅니다.

### 소비자

이제 소비자를 만드는 방법을 살펴보겠습니다. Consumer 클래스를 생성하여 이를 수행할 수 있습니다.

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

위의 소비자에서 @KafkaListener 주석을 사용하여 "테스트" 주제에 대한 메시지를 수신합니다.

## 추가 정보

- 스프링 부트: https://spring.io/projects/spring-boot
- 아파치 카프카: https://kafka.apache.org/

## 경고

- application.properties 파일에 Apache Kafka 브로커 주소를 추가해야 합니다.
- 프로젝트에 spring-kafka 종속성을 추가해야 합니다.

## 위험

- 소비자에서 오프셋을 수동으로 커밋하지 마십시오.