---
title: 012: 메시지 브로커와 함께 Spring Boot 사용(RabbitMQ)
description: 
published: true
date: 2023-02-01T20:20:37.054Z
tags: 
editor: markdown
dateCreated: 2023-02-01T20:20:37.054Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [012: Using Spring Boot with message brokers (RabbitMQ)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/012-using-spring-boot-with-message-brokers-rabbitmq)
{.links-list}
 게시물은 독립적이어야 합니다.
  
    IT 개발 학습 블로그는 개발자가 기술을 향상시키는 데 사용할 수 있는 플랫폼입니다. 블로그는 기본에서 고급까지 다양한 주제를 다루며 모든 수준의 개발자에게 적합합니다.

# 메시지 브로커(RabbitMQ)와 함께 스프링 부트 사용

이 게시물에서는 메시지 브로커, 특히 RabbitMQ와 함께 Spring Boot를 사용하는 방법을 살펴보겠습니다. 다음 주제를 다룹니다.

* 메시지 브로커란?
* 메시지 브로커를 사용하는 이유는 무엇입니까?
* RabbitMQ에서 Spring Boot를 사용하는 방법은 무엇입니까?

## 메시지 브로커란?

메시지 브로커는 응용 프로그램이 메시지를 전달하여 서로 통신할 수 있도록 하는 소프트웨어입니다. 메시지 브로커는 채팅 응용 프로그램, 게임 응용 프로그램 및 금융 거래 시스템과 같은 다양한 응용 프로그램에서 사용됩니다.

## 메시지 브로커를 사용하는 이유는 무엇입니까?

애플리케이션에서 메시지 브로커를 사용하려는 몇 가지 이유가 있습니다.

* **애플리케이션을 분리하려면**: 메시지 브로커를 사용하여 애플리케이션이 서로 직접적으로 의존하지 않도록 분리할 수 있습니다. 이를 통해 애플리케이션의 탄력성과 확장성을 높일 수 있습니다.

* **성능 향상을 위해**: 메시지 브로커를 사용하면 메시지 브로커로 메시지 전달 작업을 오프로드하여 애플리케이션의 성능을 향상시킬 수 있습니다.

* **신뢰성 제공**: 메시지 브로커를 사용하면 직접 통신 모델을 사용하는 경우 제공할 수 없는 배달 보장과 같은 신뢰성 보장을 제공할 수 있습니다.

## Spring Boot를 RabbitMQ와 함께 사용하는 방법은 무엇입니까?

메시지 브로커를 사용해야 하는 몇 가지 이유를 살펴보았으므로 이제 RabbitMQ와 함께 Spring Boot를 사용하는 방법을 살펴보겠습니다.

RabbitMQ는 사용하기 쉽고 다양한 기능을 갖춘 인기 있는 오픈 소스 메시지 브로커입니다.

Spring Boot에서 RabbitMQ를 사용하려면 `pom.xml` 파일에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```

종속성을 추가한 후에는 `application.properties` 파일에서 RabbitMQ를 구성할 수 있습니다.

```properties
spring.rabbitmq.host=localhost
spring.rabbitmq.port=5672
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```

이제 RabbitMQ를 구성했으므로 애플리케이션에서 이를 사용하는 방법을 살펴보겠습니다.

먼저 메시지를 작성해야 합니다.

```java
public class MyMessage {

    private String text;

    public MyMessage(String text) {
        this.text = text;
    }

    public String getText() {
        return text;
    }

    public void setText(String text) {
        this.text = text;
    }
}
```

다음으로 메시지 생성자를 만들어야 합니다.

```java
@Component
public class MyMessageProducer {

    @Autowired
    private RabbitTemplate rabbitTemplate;

    public void sendMessage(MyMessage message) {
        rabbitTemplate.convertAndSend("my-exchange", "my-routing-key", message);
    }
}
```

마지막으로 메시지 소비자를 만들어야 합니다.

```java
@Component
public class MyMessageConsumer {

    @Autowired
    private RabbitTemplate rabbitTemplate;

    public MyMessage receiveMessage() {
        return (MyMessage) rabbitTemplate.receiveAndConvert("my-queue");
    }
}
```

그리고 그게 다야! 이제 `MyMessageProducer`를 사용하여 메시지를 보내고 `MyMessageConsumer`를 사용하여 메시지를 받을 수 있습니다.

## 추가 정보

* 메시지 브로커에 대해 자세히 알아보려면 이 [기사](https://www.cloudamqp.com/blog/2017-12-29-what-is-message-broker.html)를 확인하세요.

* RabbitMQ에 대해 더 알고 싶다면 [공식 문서](https://www.rabbitmq.com/documentation.html)를 확인하세요.