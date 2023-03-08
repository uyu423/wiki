---
title: Kafka를 사용한 Spring Boot 및 이벤트 기반 아키텍처
description: 
published: true
date: 2023-02-08T02:32:38.737Z
tags: 
editor: markdown
dateCreated: 2023-02-08T02:32:37.164Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot and Event-Driven Architecture with Kafka***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-event-driven-architecture-with-kafka)
{.links-list}


# Kafka를 사용한 스프링 부트 및 이벤트 기반 아키텍처

EDA(Event-Driven Architecture)는 확장 가능한 고성능 애플리케이션을 구축하는 데 널리 사용되는 디자인 패턴입니다. 이벤트 기반 시스템에서 이벤트는 발생 시 사용자 또는 시스템 구성 요소에 의해 생성됩니다. 그런 다음 이러한 이벤트는 관심이 있는 구성 요소로 전파되어 적절한 조치를 취할 수 있습니다.

Kafka는 이벤트 기반 아키텍처를 구축하는 데 사용할 수 있는 인기 있는 오픈 소스 스트리밍 플랫폼입니다. Kafka는 확장성이 뛰어나고 내결함성이 있으며 고성능과 짧은 대기 시간을 제공합니다.

이 기사에서는 Spring Boot와 Kafka를 사용하여 이벤트 기반 아키텍처를 구축하는 방법을 살펴보겠습니다. 또한 Spring Cloud Stream을 사용하여 이벤트 기반 마이크로서비스 개발을 간소화하는 방법도 알아봅니다.

## 카프카 설정

이벤트 기반 아키텍처 개발을 시작하기 전에 Kafka 브로커를 설정해야 합니다. Kafka는 [Confluent 웹사이트](https://www.confluent.io/download/)에서 다운로드할 수 있습니다.

Kafka를 다운로드하고 추출한 후 다음 명령을 실행하여 브로커를 시작할 수 있습니다.

```
bin/kafka-server-start.sh config/server.properties
```

## 스프링 부트 프로젝트 생성

Spring Boot를 사용하여 마이크로 서비스 개발을 단순화할 것입니다. Spring Boot를 사용하면 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다.

[Spring Initializr](https://start.spring.io/)를 사용하여 새로운 Spring Boot 프로젝트를 생성할 수 있습니다. 다음 종속성을 선택해야 합니다.

- 웹
- 클라우드 스트림
- 카프카 스트림

![스프링 이니셜라이저](https://i.imgur.com/RgC5koh.png)

프로젝트를 생성하면 선택한 IDE로 가져올 수 있습니다.

## 생산자 개발

이벤트 기반 아키텍처는 이벤트를 생성하는 생산자와 해당 이벤트를 처리하는 소비자로 구성됩니다. 프로듀서 개발부터 시작하겠습니다.

생산자는 REST 끝점을 노출하는 간단한 Spring Boot 애플리케이션입니다. 이 엔드포인트가 호출되면 이벤트를 생성하여 Kafka 주제로 보냅니다.

먼저 새 Kafka 주제를 만들어야 합니다. Kafka CLI를 사용하여 이 작업을 수행할 수 있습니다.

```
bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --topic events --partitions 1 --replication-factor 1
```

다음으로 이벤트를 Kafka 주제로 보낼 Spring Cloud Stream 바인딩을 생성합니다. 이 바인딩은 `application.yml` 파일에서 정의됩니다.

```yaml
spring:
  cloud:
    stream:
      bindings:
        output:
          destination: events
          content-type: application/json
```

이제 Spring Boot 컨트롤러를 만들 수 있습니다. 이 컨트롤러는 이벤트를 생성하는 데 사용할 수 있는 `/events` 엔드포인트를 노출합니다.

```java
@RestController
public class EventController {

    @Autowired
    private MessageChannel output;

    @PostMapping("/events")
    public void publishEvent(@RequestBody Event event) {
        output.send(MessageBuilder.withPayload(event).build());
    }
}
```

컨트롤러는 REST 엔드포인트를 노출함을 나타내기 위해 `@RestController`로 주석 처리됩니다. 또한 Kafka 주제에 메시지를 보내는 데 사용되는 'MessageChannel' 빈을 주입합니다.

마지막으로 `Event` 클래스를 정의해야 합니다. 이 클래스는 생산자가 생성한 이벤트를 나타내는 데 사용됩니다.

```java
public class Event {

    private String id;
    private String data;

    // Getters and setters
}
```

## 소비자 개발

생산자를 개발했으므로 이제 소비자 개발로 넘어갈 수 있습니다.

소비자는 Kafka 주제로 전송되는 이벤트를 처리하기 위해 Kafka Streams를 사용하는 Spring Cloud Stream 애플리케이션이 됩니다.

먼저 Kafka 주제에서 이벤트를 수신할 Spring Cloud Stream 바인딩을 생성합니다. 이 바인딩은 `application.yml` 파일에서 정의됩니다.

```yaml
spring:
  cloud:
    stream:
      bindings:
        input:
          destination: events
          content-type: application/json
```

다음으로 이벤트를 처리할 Kafka Streams 토폴로지를 만듭니다. 이 토폴로지는 `EventStreamsConfig` 클래스에서 정의됩니다.

```java
@Configuration
public class EventStreamsConfig {

    @Bean
    public Topology buildTopology(StreamsBuilder builder) {
        // ...
    }
}
```

`buildTopology()` 메서드는 `StreamsBuilder`를 매개변수로 받아들입니다. 이 빌더를 사용하여 토폴로지를 구성할 수 있습니다.

토폴로지에서는 Kafka 항목에서 읽은 이벤트 스트림을 만듭니다. 그런 다음 Kafka Streams 프로세서를 사용하여 이 스트림을 처리합니다. 이 프로세서는 이벤트에서 데이터를 추출하여 콘솔에 출력합니다.

```java
@Configuration
public class EventStreamsConfig {

    @Bean
    public Topology buildTopology(StreamsBuilder builder) {
        Stream<Event> stream = builder.stream("events", Consumed.with(Serdes.String(), new JsonSerde<>(Event.class)));
        stream.process(new ProcessorSupplier<String, Event>() {
            @Override
            public Processor<String, Event> get() {
                return new Processor<String, Event>() {
                    private ProcessorContext context;

                    @Override
                    public void init(ProcessorContext context) {
                        this.context = context;
                    }

                    @Override
                    public void process(String key, Event event) {
                        String data = event.getData();
                        System.out.println(data);
                    }

                    @Override
                    public void close() {
                    }
                };
            }
        });

        return builder.build();
    }
}
```

이 토폴로지에서는 `JsonSerde`를 사용하여 이벤트를 직렬화 및 역직렬화합니다. 일반 텍스트 이벤트를 사용하려면 `StringSerde`를 대신 사용할 수 있습니다.

이제 소비자를 개발했으므로 Kafka 주제에 일부 이벤트를 전송하여 소비자를 시작하고 테스트할 수 있습니다. Kafka CLI를 사용하여 이벤트를 생성할 수 있습니다.

```
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic events
```

그런 다음 생산자에서 일부 JSON 이벤트 데이터를 입력할 수 있습니다.

```json
{"id":"1","data":"Hello, world!"}
```

소비자의 로그를 확인하면 입력한 이벤트 데이터가 표시됩니다.

```
Hello, world!
```

## 결론

이 기사에서는 Spring Boot와 Kafka를 사용하여 이벤트 기반 아키텍처를 구축하는 방법을 살펴보았습니다. 또한 Spring Cloud Stream을 사용하여 이벤트 기반 마이크로서비스 개발을 간소화하는 방법도 살펴보았습니다.