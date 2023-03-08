---
title: 031: Integrating with other technologies such as Redis, RabbitMQ, and more
description: 
published: true
date: 2023-02-15T10:32:23.597Z
tags: 
editor: markdown
dateCreated: 2023-02-15T10:32:21.424Z
---

- [031: Integración con otras tecnologías como Redis, RabbitMQ y más***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/031-integrating-with-other-technologies-such-as-redis-rabbitmq-and-more)
{.links-list}
- [031：与Redis、RabbitMQ等其他技术集成***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/031-integrating-with-other-technologies-such-as-redis-rabbitmq-and-more)
{.links-list}
- [031: Redis, RabbitMQ 등과 같은 다른 기술과 통합***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/031-integrating-with-other-technologies-such-as-redis-rabbitmq-and-more)
{.links-list}


#031: Integrating with other technologies such as Redis, RabbitMQ, and more

In this post, we'll learn about integrating with other technologies, such as Redis, RabbitMQ, and more.

##What is Redis?

Redis is an open source, in-memory data structure store that can be used as a database, cache, and message broker. It supports data structures such as strings, hashes, lists, sets, and sorted sets with range queries, bitmaps, hyperloglogs, and geospatial indexes with radius queries.

##What is RabbitMQ?

RabbitMQ is an open source message broker that offers a reliable, highly available, and scalable platform for handling messages.

##How to integrate with Redis

Integrating with Redis is simple. You just need to add the following dependency to your project:

```xml
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-redis</artifactId>
    <version>2.0.8.RELEASE</version>
</dependency>
```

And configure the RedisTemplate bean in your application context:

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

##How to integrate with RabbitMQ

Integrating with RabbitMQ is also simple. You just need to add the following dependency to your project:

```xml
<dependency>
    <groupId>org.springframework.amqp</groupId>
    <artifactId>spring-rabbit</artifactId>
    <version>1.7.4.RELEASE</version>
</dependency>
```

And configure the RabbitTemplate bean in your application context:

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

##Additional Information

- For more information about Redis, see the [Redis website](https://redis.io/).
- For more information about RabbitMQ, see the [RabbitMQ website](https://www.rabbitmq.com/).