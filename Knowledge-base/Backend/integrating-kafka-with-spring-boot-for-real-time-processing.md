---
title: 실시간 처리를 위해 Kafka와 Spring Boot 통합
description: 
published: true
date: 2023-01-31T20:17:26.875Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:17:24.083Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Integrating Kafka with Spring Boot for Real-time Processing***English** version of this document is available*](/en/Knowledge-base/Backend/integrating-kafka-with-spring-boot-for-real-time-processing)
{.links-list}



# 소개

이 기사에서는 Kafka를 Spring Boot와 통합하여 실시간 데이터를 처리하는 방법을 살펴봅니다. 우리는 이것을 증명하기 위해 간단한 예를 사용할 것입니다.

Kafka는 데이터 스트림을 게시하고 구독하는 데 사용할 수 있는 분산 스트리밍 플랫폼입니다. 확장 가능하고 내결함성이 있어 실시간 데이터 처리에 이상적입니다. Spring Boot는 마이크로 서비스를 만드는 데 사용할 수 있는 인기 있는 Java 프레임워크입니다.

# 카프카 설정

예제 코드를 실행하려면 Kafka가 설치되어 있어야 합니다. 여기에서 이를 수행하는 방법에 대한 지침을 찾을 수 있습니다.

https://kafka.apache.org/quickstart

Kafka를 시작하고 실행하면 다음 명령을 사용하여 주제를 생성할 수 있습니다.

```
kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
```

# 스프링 부트 예제

이제 Kafka가 설정되었으므로 "테스트" 주제에 대한 메시지를 게시하고 구독할 Spring Boot 애플리케이션을 만들어 보겠습니다.

다음 종속성을 사용하여 간단한 Spring Boot 애플리케이션을 생성하는 것으로 시작하겠습니다.

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

다음으로 Kafka 브로커 및 주제에 대한 설정을 포함하는 구성 파일을 생성합니다.

```
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.topic.test=test
```

이제 간단한 Kafka 생산자 및 소비자를 만들 수 있습니다.

먼저 "테스트" 항목에 메시지를 보낼 생산자를 생성해 보겠습니다.

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

다음으로 "테스트" 주제에서 메시지를 수신할 소비자를 생성해 보겠습니다.

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

이제 방금 만든 생산자와 소비자를 사용할 간단한 Spring Boot 애플리케이션을 만들 수 있습니다.

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

응용 프로그램을 실행하고 "테스트" 항목에 메시지를 보내면 소비자가 메시지를 받는 것을 볼 수 있습니다.

![Kafka Consumer 스크린샷](kafka-consumer.png)

# 결론

이 기사에서는 Kafka를 Spring Boot와 통합하여 실시간 데이터를 처리하는 방법을 살펴보았습니다. Kafka 주제에서 메시지를 보내고 받는 방법을 보여주는 간단한 생산자와 소비자를 만들었습니다.