---
title: 012: 메시지 브로커와 함께 Spring Boot 사용(RabbitMQ)
description: 
published: true
date: 2023-02-01T20:26:40.209Z
tags: 
editor: markdown
dateCreated: 2023-02-01T20:26:38.530Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [012: Using Spring Boot with message brokers (RabbitMQ)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/012-using-spring-boot-with-message-brokers-rabbitmq)
{.links-list}


# 012: 메시지 브로커와 함께 Spring Boot 사용(RabbitMQ)

이 게시물에서는 메시지 브로커, 특히 RabbitMQ와 함께 Spring Boot를 사용하는 방법을 살펴보겠습니다. 메시지 브로커가 무엇인지, Spring Boot와 함께 사용하는 방법 및 몇 가지 모범 사례를 다룰 것입니다.

## 메시지 브로커란?

메시지 브로커는 서로 다른 응용 프로그램 간의 통신을 관리하는 데 도움이 되는 소프트웨어입니다. 응용 프로그램 간의 중개자 역할을 하여 이를 수행합니다. 애플리케이션은 브로커에 메시지를 보낼 수 있으며 브로커는 메시지를 적절한 애플리케이션으로 전달합니다.

## 메시지 브로커를 사용하는 이유는 무엇입니까?

메시지 브로커를 사용하려는 몇 가지 이유가 있습니다.

### 1. 애플리케이션 분리

메시지 브로커를 사용하는 주된 이유 중 하나는 애플리케이션을 분리하는 것입니다. 분리란 응용 프로그램이 서로 직접적으로 종속되지 않음을 의미합니다. 여기에는 몇 가지 이점이 있습니다.

첫째, 애플리케이션을 독립적으로 개발할 수 있음을 의미합니다. 이것은 시스템의 다른 부분에서 작업하는 대규모 팀이 있는 경우 큰 이점이 될 수 있습니다.

둘째, 애플리케이션의 탄력성을 높입니다. 한 응용 프로그램이 다운되더라도 다른 응용 프로그램은 계속 작동할 수 있습니다.

### 2. 확장성

메시지 브로커를 사용하는 또 다른 이유는 확장성입니다. 트래픽이 많은 경우 로드를 처리할 브로커를 더 추가할 수 있습니다. 이것은 단일 애플리케이션을 확장하려고 시도하는 것보다 훨씬 쉽습니다.

## Spring Boot에서 메시지 브로커를 사용하는 방법

이제 메시지 브로커를 사용하는 몇 가지 이유를 살펴보았으므로 Spring Boot에서 메시지 브로커를 사용하는 방법을 살펴보겠습니다.

Spring Boot는 메시지 브로커를 잘 지원합니다. RabbitMQ에 대한 지원을 추가하기 위해 `spring-boot-starter-amqp` 종속성을 사용할 수 있습니다.

RabbitMQ를 사용하려면 `application.properties` 파일에 다음을 추가해야 합니다.

```properties
spring.rabbitmq.host=localhost
spring.rabbitmq.port=5672
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```

`localhost`를 RabbitMQ 서버의 호스트 이름으로 바꿉니다. 기본 포트는 '5672'입니다. 사용자 이름과 암호는 RabbitMQ의 기본값입니다.

속성을 추가하고 나면 `RabbitTemplate`을 코드에 삽입할 수 있습니다. 메시지를 보내고 받는 데 사용할 클래스입니다.

다음은 템플릿을 사용하여 메시지를 보내는 방법에 대한 간단한 예입니다.

```java
@Autowired
private RabbitTemplate rabbitTemplate;

public void sendMessage(String message) {
    rabbitTemplate.convertAndSend("exchange", "routingKey", message);
}
```

`convertAndSend` 메서드는 교환, 라우팅 키 및 메시지를 사용합니다. 교환은 사용할 교환의 이름입니다. 라우팅 키는 메시지를 올바른 대기열로 라우팅하는 데 사용됩니다. 메시지는 바이트 배열로 변환할 수 있는 모든 개체가 될 수 있습니다.

`receiveAndConvert` 메서드를 사용하여 메시지를 받을 수도 있습니다.

```java
@Autowired
private RabbitTemplate rabbitTemplate;

public String receiveMessage() {
    return (String)rabbitTemplate.receiveAndConvert("queue");
}
```

이 메서드는 큐 이름을 사용하고 개체를 반환합니다. 객체를 올바른 유형으로 캐스팅해야 합니다.

## 모범 사례

이제 Spring Boot에서 메시지 브로커를 사용하는 방법을 살펴보았으므로 몇 가지 모범 사례를 살펴보겠습니다.

### 1. 메시지 변환기 사용

Spring Boot는 다양한 메시지 변환기와 함께 제공됩니다. 이러한 변환기를 사용하여 서로 다른 메시지 형식 간에 변환할 수 있습니다. 예를 들어 `StringMessageConverter`를 사용하여 문자열과 바이트 배열 사이를 변환할 수 있습니다.

메시지를 보내고 받을 때 메시지 변환기를 사용하는 것이 좋습니다. 이렇게 하면 메시지를 올바른 형식으로 변환하는 것에 대해 걱정할 필요가 없습니다.

### 2. 메시지 리스너 사용

또 다른 모범 사례는 메시지 수신기를 사용하는 것입니다. 메시지 리스너는 `MessageListener` 인터페이스를 구현하는 클래스입니다. 이 인터페이스에는 단일 `onMessage` 메서드가 있습니다.

```java
public interface MessageListener {
    void onMessage(Message message);
}
```

이 메서드는 메시지를 수신할 때 호출됩니다. 메시지는 매개변수로 전달됩니다.

메시지 리스너는 수신된 메시지를 처리하는 좋은 방법입니다. 메시지를 폴링하거나 메시지를 올바른 형식으로 변환하는 것에 대해 걱정할 필요가 없습니다.

### 3. 메시지 대기열 사용

메시지 브로커를 사용할 때 메시지 큐를 사용하는 것이 좋습니다. 메시지 큐는 메시지를 저장하는 데이터 구조입니다. 메시지는 받은 순서대로 저장됩니다.

메시지 큐는 처리해야 하는 메시지를 저장하는 데 사용할 수 있습니다. 예를 들어 메시지를 받으면 대기열에 메시지를 추가할 수 있습니다. 그런 다음 대기열의 메시지를 한 번에 하나씩 처리할 수 있습니다.

메시지 대기열을 사용하여 성능을 향상시킬 수 있습니다. 많은 메시지를 처리하는 경우 병렬로 처리할 수 있습니다. 이렇게 하면 다음 메시지 처리를 시작하기 전에 하나의 메시지가 처리될 때까지 기다릴 필요가 없습니다.

## 추가 정보

- [스프링 부트 참조 가이드](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
- [RabbitMQ 문서](https://www.rabbitmq.com/documentation.html)

## 경고

- 메시지를 보내고 받을 때 올바른 메시지 변환기를 사용하십시오. 그렇지 않으면 예기치 않은 결과가 발생할 수 있습니다.
- 메시지를 수신할 때 올바른 메시지 리스너를 사용했는지 확인하십시오. 그렇지 않으면 메시지를 놓치거나 예기치 않은 결과를 얻을 수 있습니다.

## 위험

- 메시지 대기열을 사용하지 않는 경우 메시지가 순서 없이 처리될 수 있습니다.
- 메시지 변환기를 사용하지 않는 경우 메시지가 올바른 형식으로 변환되지 않을 수 있습니다.