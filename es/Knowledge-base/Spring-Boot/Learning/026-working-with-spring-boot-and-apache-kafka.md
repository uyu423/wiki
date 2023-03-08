---
title: 026: Trabajar con Spring Boot y Apache Kafka
description: 
published: true
date: 2023-02-03T18:32:23.657Z
tags: 
editor: markdown
dateCreated: 2023-02-03T18:32:21.998Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [026: Working with Spring Boot and Apache Kafka***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/026-working-with-spring-boot-and-apache-kafka)
{.links-list}


# Trabajar con Spring Boot y Apache Kafka

En esta publicación, veremos cómo trabajar con Spring Boot y Apache Kafka. Cubriremos los siguientes temas:

- ¿Qué es Apache Kafka?
- ¿Qué es Spring Boot?
- Cómo usar Spring Boot con Apache Kafka
- Información adicional
- Advertencias
- Peligros

## ¿Qué es Apache Kafka?

Apache Kafka es una plataforma de transmisión distribuida. Se utiliza para crear canalizaciones de datos en tiempo real y aplicaciones de transmisión. Es escalable horizontalmente, tolerante a fallas y rápido.

Kafka está escrito en Scala y Java. Tiene un modelo de mensajería de publicación-suscripción. Es un sistema de alto rendimiento.

## ¿Qué es Spring Boot?

Spring Boot es un marco basado en Java que se utiliza para crear microservicios. Se utiliza para simplificar el arranque y el desarrollo de una nueva aplicación Spring.

Spring Boot es obstinado. Proporciona un conjunto de configuraciones predeterminadas. Facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

## Cómo usar Spring Boot con Apache Kafka

Para usar Spring Boot con Apache Kafka, debemos agregar la siguiente dependencia a nuestro proyecto:

```xml
<dependency>
    <groupId>org.springframework.kafka</groupId>
    <artifactId>spring-kafka</artifactId>
</dependency>
```

También necesitamos agregar la siguiente dependencia si queremos usar Apache Kafka con Avro:

```xml
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-avro-serializer</artifactId>
</dependency>
```

Ahora que tenemos las dependencias en su lugar, echemos un vistazo a cómo usar Spring Boot con Apache Kafka.

### Configuración

Primero, necesitamos configurar el agente Apache Kafka. Podemos hacer esto configurando las siguientes propiedades en nuestro archivo application.properties:

```properties
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.producer.retries=0
spring.kafka.producer.batch-size=16384
spring.kafka.producer.buffer-memory=33554432
spring.kafka.consumer.group-id=test
spring.kafka.consumer.auto-offset-reset=earliest
spring.kafka.consumer.enable-auto-commit=false
```

En la configuración anterior, estamos configurando las siguientes propiedades:

- La dirección del bróker de Apache Kafka
- El número de reintentos para el productor.
- El tamaño del lote del productor.
- La memoria intermedia del productor
- La identificación del grupo de consumidores
- El restablecimiento de compensación automática del consumidor
- El compromiso automático del consumidor

### Productor

Ahora echemos un vistazo a cómo crear un productor. Podemos hacer esto creando una clase Producer:

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

En el productor anterior, usamos KafkaTemplate para enviar mensajes al corredor de Kafka.

### Consumidor

Ahora echemos un vistazo a cómo crear un consumidor. Podemos hacer esto creando una clase de consumidor:

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

En el consumidor anterior, usamos la anotación @KafkaListener para escuchar mensajes sobre el tema de "prueba".

## Información adicional

- Arranque de primavera: https://spring.io/projects/spring-boot
-Apache Kafka: https://kafka.apache.org/

## Advertencias

- Asegúrese de agregar la dirección del intermediario de Apache Kafka al archivo application.properties.
- Asegúrese de agregar la dependencia spring-kafka al proyecto.

## Peligros

- No cometer compensaciones manualmente en el consumidor.