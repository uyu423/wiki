---
title: 031: Integración con otras tecnologías como Redis, RabbitMQ y más
description: 
published: true
date: 2023-02-15T10:32:29.179Z
tags: 
editor: markdown
dateCreated: 2023-02-15T10:32:21.421Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [031: Integrating with other technologies such as Redis, RabbitMQ, and more***English** document is available*](/en/Knowledge-base/Nest-js/Learning/031-integrating-with-other-technologies-such-as-redis-rabbitmq-and-more)
{.links-list}


# 031: Integración con otras tecnologías como Redis, RabbitMQ y más

En esta publicación, aprenderemos sobre la integración con otras tecnologías, como Redis, RabbitMQ y más.

## ¿Qué es Redis?

Redis es un almacén de estructura de datos en memoria de código abierto que se puede utilizar como base de datos, caché y agente de mensajes. Admite estructuras de datos como cadenas, hashes, listas, conjuntos y conjuntos ordenados con consultas de rango, mapas de bits, hiperloglogs e índices geoespaciales con consultas de radio.

## ¿Qué es RabbitMQ?

RabbitMQ es un agente de mensajes de código abierto que ofrece una plataforma confiable, escalable y de alta disponibilidad para el manejo de mensajes.

## Cómo integrarse con Redis

La integración con Redis es simple. Solo necesita agregar la siguiente dependencia a su proyecto:

```xml
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-redis</artifactId>
    <version>2.0.8.RELEASE</version>
</dependency>
```

Y configure el bean RedisTemplate en el contexto de su aplicación:

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

## Cómo integrarse con RabbitMQ

La integración con RabbitMQ también es simple. Solo necesita agregar la siguiente dependencia a su proyecto:

```xml
<dependency>
    <groupId>org.springframework.amqp</groupId>
    <artifactId>spring-rabbit</artifactId>
    <version>1.7.4.RELEASE</version>
</dependency>
```

Y configure el bean RabbitTemplate en el contexto de su aplicación:

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

## Información adicional

- Para obtener más información sobre Redis, consulte el [sitio web de Redis] (https://redis.io/).
- Para obtener más información sobre RabbitMQ, consulte el [sitio web de RabbitMQ] (https://www.rabbitmq.com/).