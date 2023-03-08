---
title: 031: Redis, RabbitMQ 등과 같은 다른 기술과 통합
description: 
published: true
date: 2023-02-15T10:32:29.179Z
tags: 
editor: markdown
dateCreated: 2023-02-15T10:32:21.416Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [031: Integrating with other technologies such as Redis, RabbitMQ, and more***English** document is available*](/en/Knowledge-base/Nest-js/Learning/031-integrating-with-other-technologies-such-as-redis-rabbitmq-and-more)
{.links-list}


# 031: Redis, RabbitMQ 등과 같은 다른 기술과의 통합

이 게시물에서는 Redis, RabbitMQ 등과 같은 다른 기술과의 통합에 대해 알아봅니다.

## 레디스란?

Redis는 데이터베이스, 캐시 및 메시지 브로커로 사용할 수 있는 오픈 소스 메모리 내 데이터 구조 저장소입니다. 문자열, 해시, 목록, 세트, 범위 쿼리가 있는 정렬된 세트, 비트맵, 하이퍼로그, 반지름 쿼리가 있는 지리 공간 인덱스와 같은 데이터 구조를 지원합니다.

## RabbitMQ란?

RabbitMQ는 메시지 처리를 위한 안정적이고 가용성이 높으며 확장 가능한 플랫폼을 제공하는 오픈 소스 메시지 브로커입니다.

## Redis와 통합하는 방법

Redis와의 통합은 간단합니다. 프로젝트에 다음 종속성을 추가하기만 하면 됩니다.

```xml
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-redis</artifactId>
    <version>2.0.8.RELEASE</version>
</dependency>
```

그리고 애플리케이션 컨텍스트에서 RedisTemplate 빈을 구성합니다.

```java
@Configuration
public class RedisConfig {

    @Bean
    public RedisTemplate<String, Object> redisTemplate(
            RedisConnectionFactory redisConnectionFactory) {
        RedisTemplate<String, Object> template = new RedisTemplate<>();
        template.setConnectionFactory(redisConnectionFactory);
        return template;
    }
}
```

## RabbitMQ와 통합하는 방법

RabbitMQ와의 통합도 간단합니다. 프로젝트에 다음 종속성을 추가하기만 하면 됩니다.

```xml
<dependency>
    <groupId>org.springframework.amqp</groupId>
    <artifactId>spring-rabbit</artifactId>
    <version>1.7.4.RELEASE</version>
</dependency>
```

그리고 애플리케이션 컨텍스트에서 RabbitTemplate 빈을 구성합니다.

```java
@Configuration
public class RabbitMQConfig {

    @Bean
    public RabbitTemplate rabbitTemplate(ConnectionFactory connectionFactory) {
        RabbitTemplate template = new RabbitTemplate(connectionFactory);
        template.setMessageConverter(new Jackson2JsonMessageConverter());
        return template;
    }
}
```

## 추가 정보

- Redis에 대한 자세한 내용은 [Redis 홈페이지](https://redis.io/)를 참조하세요.
- RabbitMQ에 대한 자세한 내용은 [RabbitMQ 웹사이트](https://www.rabbitmq.com/)를 참조하세요.