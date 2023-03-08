---
title: 065: 메시징을 위해 Spring Boot와 RabbitMQ 통합
description: 
published: true
date: 2023-02-03T19:55:29.964Z
tags: 
editor: markdown
dateCreated: 2023-02-03T19:55:28.245Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [065: Integrating Spring Boot with RabbitMQ for Messaging***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/065-integrating-spring-boot-with-rabbitmq-for-messaging)
{.links-list}


# 065: 메시징을 위해 Spring Boot와 RabbitMQ 통합

이 게시물에서는 메시지를 생성하고 사용하기 위해 Spring Boot를 RabbitMQ와 통합하는 방법을 배웁니다. 또한 RabbitMQ를 사용하여 간단한 메시지 대기열을 설정하는 방법도 살펴보겠습니다.

RabbitMQ는 클라이언트가 연결하고 메시지를 교환할 수 있게 해주는 메시지 브로커입니다. 메시지 대기열을 처리하는 데 널리 사용되는 선택이며 Spring Boot와 잘 통합됩니다.

## RabbitMQ 설정하기

RabbitMQ를 사용하기 전에 설정해야 합니다. Docker를 사용하여 컨테이너에서 RabbitMQ 서버를 실행합니다.

먼저 RabbitMQ Docker 이미지를 가져와야 합니다.

```
$ docker pull rabbitmq:3.6.5-management
```

다음으로 방금 가져온 이미지를 사용하여 Docker 컨테이너를 시작합니다.

```
$ docker run -d --name rabbitmq -p 15672:15672 -p 5672:5672 rabbitmq:3.6.5-management
```

그러면 컨테이너에서 RabbitMQ 서버가 시작되고 포트 15672의 관리 UI와 포트 5672의 메시지 브로커가 노출됩니다.

## 스프링 부트 프로젝트 생성

이제 RabbitMQ가 실행 중이므로 Spring Boot 프로젝트를 생성하여 메시지를 생성하고 사용할 수 있습니다.

Spring Initializr를 사용하여 프로젝트를 생성합니다. 다음 종속성을 선택해야 합니다.

* 웹
* AMQP

다른 옵션은 기본값으로 둘 수 있습니다.

프로젝트가 생성되면 `pom.xml`에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```

## 스프링 부트 설정

이제 프로젝트를 설정했으므로 RabbitMQ 서버에 연결하도록 Spring Boot를 구성해야 합니다. `application.properties`에 다음을 추가하여 이를 수행합니다.

```
spring.rabbitmq.host=localhost
spring.rabbitmq.port=5672
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```

## 생산자 만들기

이제 프로젝트가 설정되고 구성되었으므로 RabbitMQ 서버에 메시지를 보낼 생산자를 만들 수 있습니다.

`String`을 가져와 RabbitMQ `Queue`로 보내는 `sendMessage` 메서드로 `MessageProducer` 클래스를 생성합니다.

```java
@Component
public class MessageProducer {

    @Autowired
    private AmqpTemplate amqpTemplate;

    public void sendMessage(String message) {
        amqpTemplate.convertAndSend("queue", message);
    }

}
```

이 클래스에서는 `AmqpTemplate`을 사용하여 `String` 메시지를 `AMQP` 메시지로 변환하고 `queue`로 보냅니다.

## 소비자 만들기

이제 생산자가 있으므로 대기열에서 메시지를 수신할 소비자가 필요합니다.

`queue`에서 `AMQP` 메시지를 수신하고 이를 `String`으로 변환하는 `receiveMessage` 메소드로 `MessageConsumer` 클래스를 생성합니다.

```java
@Component
public class MessageConsumer {

    @Autowired
    private AmqpTemplate amqpTemplate;

    public String receiveMessage() {
        return (String) amqpTemplate.receiveAndConvert("queue");
    }

}
```

이 클래스에서는 `AmqpTemplate`을 사용하여 `queue`에서 `AMQP` 메시지를 수신하고 이를 `String`으로 변환합니다.

## 생산자와 소비자 테스트

이제 생산자와 소비자가 설정되었으므로 생산자에서 소비자에게 메시지를 보내는 테스트를 작성해 보겠습니다.

생산자에서 소비자에게 메시지를 보내는 `testSendReceiveMessage` 메서드를 사용하여 `MessageProducerConsumerTest` 클래스를 만듭니다.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class MessageProducerConsumerTest {

    @Autowired
    private MessageProducer messageProducer;

    @Autowired
    private MessageConsumer messageConsumer;

    @Test
    public void testSendReceiveMessage() {
        String message = "Hello, world!";
        messageProducer.sendMessage(message);
        String receivedMessage = messageConsumer.receiveMessage();
        assertThat(receivedMessage, is(message));
    }

}
```

이 테스트에서 우리는 생산자로부터 소비자에게 메시지를 보내고 수신된 메시지가 우리가 보낸 메시지와 동일하다고 주장합니다.

## 추가 정보

* RabbitMQ에 대한 자세한 내용은 [RabbitMQ 웹사이트](https://www.rabbitmq.com/)에서 확인하세요.
* Spring Boot에 대한 자세한 내용은 [Spring Boot 웹사이트](https://spring.io/projects/spring-boot)에서 확인하세요.