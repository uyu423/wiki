---
title: 082: 데이터 스트리밍을 위해 Apache Kafka와 Spring Boot 통합
description: 
published: true
date: 2023-02-02T22:24:15.425Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:24:13.690Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [082: Integrating Spring Boot with Apache Kafka for Streaming Data***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/082-integrating-spring-boot-with-apache-kafka-for-streaming-data)
{.links-list}


# 082: 데이터 스트리밍을 위해 Apache Kafka와 Spring Boot 통합

이 게시물에서는 스트리밍 데이터를 위해 Spring Boot를 Apache Kafka와 통합하는 방법을 살펴보겠습니다. Apache Kafka는 확장 가능하고 처리량이 많고 대기 시간이 짧은 스트리밍 애플리케이션을 구축하는 데 사용할 수 있는 인기 있는 오픈 소스 스트리밍 플랫폼입니다. Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 만드는 데 사용할 수 있는 널리 사용되는 Java 기반 프레임워크입니다.

Spring Boot를 Apache Kafka와 통합하면 다음과 같은 여러 가지 이점을 얻을 수 있습니다.

- 확장 가능하고 효율적인 방식으로 많은 양의 데이터를 처리하는 능력
- 이벤트 기반 애플리케이션을 구축할 수 있는 능력
- 느슨하게 결합된 방식으로 다른 시스템 및 서비스와 통합할 수 있는 기능

## 전제 조건

시작하기 전에 이 게시물을 따라하기 위해 필요한 몇 가지 사항이 있습니다.

- 자바 개발 환경
- 아파치 메이븐
- Apache Kafka 개발 환경

## 스프링 부트 프로젝트 설정

가장 먼저 해야 할 일은 Spring Boot 프로젝트를 설정하는 것입니다. Spring Initializr를 사용하여 이를 수행할 수 있습니다. 이 게시물에서는 다음 설정을 사용합니다.

- 프로젝트: 메이븐 프로젝트
- 언어: 자바
- 스프링 부트: 2.1.0
- 그룹: com.example
- 아티팩트: kafka-streams
- 이름: kafka-streams
- 설명: Kafka Streams 예제
- 패키지 이름: com.example.kafka.streams
- 포장: 항아리
- 자바 버전: 1.8
- 종속성: 웹, Lombok, Apache Kafka Streams

프로젝트가 설정되면 다음과 같은 디렉토리 구조가 있어야 합니다.

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

## Apache Kafka용 Spring Boot 구성

이제 Spring Boot 프로젝트가 설정되었으므로 Apache Kafka와 함께 작동하도록 구성해야 합니다. `application.properties` 파일에 다음 속성을 추가하여 이를 수행할 수 있습니다.

```
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.streams.properties.application.id=streams-demo
spring.kafka.streams.properties.commit.interval.ms=1000
spring.kafka.streams.properties.default.key.serde=org.apache.kafka.common.serialization.Serdes$StringSerde
spring.kafka.streams.properties.default.value.serde=org.apache.kafka.common.serialization.Serdes$StringSerde
```

이러한 각 속성이 수행하는 작업을 살펴보겠습니다.

- `spring.kafka.bootstrap-servers`: 이 속성은 애플리케이션이 연결할 Kafka 브로커를 구성하는 데 사용됩니다.
- `spring.kafka.streams.properties.application.id`: 이 속성은 Kafka Streams 애플리케이션의 고유 식별자를 구성하는 데 사용됩니다.
- `spring.kafka.streams.properties.commit.interval.ms`: 이 속성은 Kafka Streams가 오프셋을 커밋하는 빈도를 구성하는 데 사용됩니다.
- `spring.kafka.streams.properties.default.key.serde`: 이 속성은 Kafka Streams의 기본 키 serde를 구성하는 데 사용됩니다.
- `spring.kafka.streams.properties.default.value.serde`: 이 속성은 Kafka Streams에 대한 기본값 serde를 구성하는 데 사용됩니다.

## Kafka Streams 애플리케이션 생성

이제 프로젝트가 설정 및 구성되었으므로 Kafka Streams 애플리케이션 작성을 시작할 수 있습니다. `KafkaStreamsApplication`이라는 새 클래스를 만드는 것으로 시작하겠습니다. 이 클래스는 `org.springframework.boot.SpringApplication` 클래스를 확장하고 `@SpringBootApplication` 주석으로 주석을 추가합니다.

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

`@SpringBootApplication` 주석은 Spring Boot 애플리케이션을 구성하는 데 사용되는 편의 주석입니다. 다음 주석을 사용하는 것과 동일합니다.

- `@Configuration`: 이 주석은 클래스에 Spring Boot 구성이 포함되어 있음을 나타내는 데 사용됩니다.
- `@EnableAutoConfiguration`: 이 주석은 Spring Boot의 자동 구성 기능을 활성화하는 데 사용됩니다.
- `@ComponentScan`: 이 주석은 Spring 컴포넌트 스캔을 활성화하는 데 사용됩니다.

## Kafka Streams 토폴로지 만들기

이제 `KafkaStreamsApplication` 클래스가 설정되었으므로 Kafka Streams 토폴로지 작성을 시작할 수 있습니다. Kafka Streams 토폴로지는 스트림 처리 노드의 방향성 그래프입니다. 이 토폴로지에는 소스 노드와 싱크 노드라는 두 개의 노드가 있습니다.

소스 노드는 입력 주제에서 데이터를 읽고 싱크 노드는 데이터를 출력 주제에 씁니다. `@EnableKafkaStreams` 주석으로 `KafkaStreamsApplication` 클래스에 주석을 달아 토폴로지를 만들 수 있습니다.

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

각 주석과 메서드가 수행하는 작업을 살펴보겠습니다.

- `@EnableKafkaStreams`: 이 주석은 Spring Boot 애플리케이션에서 Kafka Streams를 활성화하는 데 사용됩니다.
- `@Value("${spring.kafka.bootstrap-servers}")`: 이 주석은 `spring.kafka.bootstrap-servers` 속성을 `bootstrapServers` 필드에 삽입하는 데 사용됩니다.
- `@Value("${spring.kafka.streams.properties.application.id}")`: 이 주석은 `applicationId`에 `spring.kafka.streams.properties.application.id` 속성을 주입하는 데 사용됩니다. 필드.
- `@Value("${spring.kafka.streams.properties.commit.interval.ms}")`: 이 주석은 `spring.kafka.streams.properties.commit.interval.ms` 속성을 `commitIntervalMs` 필드.
- `@Value("${spring.kafka.streams.properties.default.key.serde}")`: 이 주석은 `spring.kafka.streams.properties.default.key.serde` 속성을 `defaultKeySerde` 필드.
- `@Value("${spring.kafka.streams.properties.default.value.serde}")`: 이 주석은 `spring.kafka.streams.properties.default.value.serde` 속성을 `defaultValueSerde` 필드.
- `public static void main(String[] args)`: `KafkaStreamsApplication` 클래스의 기본 메서드입니다. 이 메서드는 Spring Boot 애플리케이션을 시작하는 데 사용됩니다.
- `@Bean`: 이 주석은 메서드가 다른 Spring 관리 빈에 주입할 수 있는 빈을 생성함을 나타내는 데 사용됩니다.
- `StreamsBuilderFactoryBeanCustomizer streamsBuilderFactoryBeanCustomizer()`: 이 메서드는 `StreamsBuilderFactoryBeanCustomizer` 빈을 생성하는 데 사용됩니다. 이 bean은 `StreamsBuilderFactoryBean`을 사용자 정의하는 데 사용됩니다.
- `public void customize(StreamsBuilderFactoryBean streamsBuilderFactoryBean)`: `StreamsBuilderFactoryBeanCustomizer` 인터페이스의 `customize` 메소드입니다. 이 메소드는 `StreamsBuilderFactoryBean`을 사용자 정의하는 데 사용됩니다.
- `streamsBuilderFactoryBean.setBootstrapServers(bootstrapServers);`: 이 줄은 `StreamsBuilderFactoryBean`에 대한 부트스트랩 서버를 설정하는 데 사용됩니다.
- `streamsBuilderFactoryBean.setApplicationId(applicationId);`: 이 행은 `StreamsBuilderFactoryBean`에 대한 애플리케이션 ID를 설정하는 데 사용됩니다.
- `streamsBuilderFactoryBean.setCommitInterval(Long.parseLong(commitIntervalMs));`: 이 줄은 `StreamsBuilderFactoryBean`에 대한 커밋 간격을 설정하는 데 사용됩니다.
- `streamsBuilderFactoryBean.setDefaultKeySerde(Serdes.String());`: 이 줄은 `StreamsBuilderFactoryBean`에 대한 기본 키 serde를 설정하는 데 사용됩니다.
- `streamsBuilderFactoryBean.setDefaultValueSerde(Serdes.String());`: 이 행은 `StreamsBuilderFactoryBean`에 대한 기본값 serde를 설정하는 데 사용됩니다.
- `@Bean`: 이 주석은 메서드가 다른 Spring 관리 빈에 주입할 수 있는 빈을 생성함을 나타내는 데 사용됩니다.
- `KStream<String, String> kStream(StreamsBuilder kStreamBuilder)`: 이 메소드는 `KStream` bean을 생성하는 데 사용됩니다. 이 빈은 스트림 처리 토폴로지를 나타내는 데 사용됩니다.
- `KStream<String, String> stream = kStreamBuilder.stream("input-topic");`: 이 줄은 입력 주제에서 `KStream`을 생성하는 데 사용됩니다.
- `stream.to("output-topic");`: 이 라인은 `KStream`에서 출력 주제로 데이터를 쓰는 데 사용됩니다.
- `return stream;`: 이 줄은 `KStream`을 반환하는 데 사용됩니다.

## 애플리케이션 빌드 및 실행

이제 애플리케이션을 작성했으므로 빌드하고 실행할 수 있습니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
mvn spring-boot:run
```

애플리케이션이 실행되면 입력 및 출력 항목에서 메시지 생성 및 사용을 시작할 수 있습니다.

## 결론

이 게시물에서는 스트리밍 데이터를 위해 Spring Boot를 Apache Kafka와 통합하는 방법을 살펴보았습니다. 또한 Kafka Streams 토폴로지를 만들고 Spring Boot 애플리케이션에서 실행하는 방법도 살펴보았습니다.