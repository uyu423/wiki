---
title: 065: Integración de Spring Boot con RabbitMQ para mensajería
description: 
published: true
date: 2023-02-03T19:55:30.014Z
tags: 
editor: markdown
dateCreated: 2023-02-03T19:55:28.242Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [065: Integrating Spring Boot with RabbitMQ for Messaging***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/065-integrating-spring-boot-with-rabbitmq-for-messaging)
{.links-list}


# 065: Integrando Spring Boot con RabbitMQ para Mensajería

En esta publicación, aprenderemos cómo integrar Spring Boot con RabbitMQ para producir y consumir mensajes. También exploraremos cómo configurar una cola de mensajes simple usando RabbitMQ.

RabbitMQ es un intermediario de mensajes que permite a los clientes conectarse e intercambiar mensajes. Es una opción popular para manejar colas de mensajes y tiene una buena integración con Spring Boot.

## Configuración de RabbitMQ

Antes de que podamos comenzar a usar RabbitMQ, debemos configurarlo. Usaremos Docker para ejecutar un servidor RabbitMQ en un contenedor.

Primero, necesitamos extraer la imagen de RabbitMQ Docker:

```
$ docker pull rabbitmq:3.6.5-management
```

A continuación, iniciaremos un contenedor Docker usando la imagen que acabamos de extraer:

```
$ docker run -d --name rabbitmq -p 15672:15672 -p 5672:5672 rabbitmq:3.6.5-management
```

Esto iniciará un servidor RabbitMQ en un contenedor y expondrá la interfaz de usuario de administración en el puerto 15672 y el intermediario de mensajes en el puerto 5672.

## Creación de un proyecto Spring Boot

Ahora que tenemos RabbitMQ en funcionamiento, podemos crear un proyecto Spring Boot para producir y consumir mensajes.

Usaremos Spring Initializr para crear nuestro proyecto. Tendremos que seleccionar las siguientes dependencias:

* Internet
* AMQP

Podemos dejar las otras opciones en sus valores predeterminados.

Una vez que se genera el proyecto, necesitaremos agregar la siguiente dependencia a nuestro `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```

## Configuración de Spring Boot

Ahora que tenemos nuestro proyecto configurado, necesitamos configurar Spring Boot para conectarnos a nuestro servidor RabbitMQ. Haremos esto agregando lo siguiente a nuestras `application.properties`:

```
spring.rabbitmq.host=localhost
spring.rabbitmq.port=5672
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```

## Creación de un productor

Ahora que nuestro proyecto está instalado y configurado, podemos crear un productor para enviar mensajes a nuestro servidor RabbitMQ.

Crearemos una clase `MessageProducer` con un método `sendMessage` que toma una `String` y la envía a una `Queue` de RabbitMQ.

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

En esta clase, estamos usando `AmqpTemplate` para convertir nuestro mensaje `String` en un mensaje `AMQP` y enviarlo a la `cola`.

## Creando un Consumidor

Ahora que tenemos un productor, necesitamos un consumidor para recibir los mensajes de la cola.

Crearemos una clase `MessageConsumer` con un método `receiveMessage` que recibe un mensaje `AMQP` de la `cola` y lo convierte en una `String`.

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

En esta clase, usamos `AmqpTemplate` para recibir un mensaje `AMQP` de la `cola` y convertirlo en `String`.

## Poniendo a prueba a nuestro productor y consumidor

Ahora que tenemos nuestro productor y consumidor configurados, escribamos una prueba para enviar un mensaje de nuestro productor a nuestro consumidor.

Crearemos una clase `MessageProducerConsumerTest` con un método `testSendReceiveMessage` que envía un mensaje de nuestro productor a nuestro consumidor.

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

En esta prueba, enviamos un mensaje de nuestro productor a nuestro consumidor y afirmamos que el mensaje recibido es el mismo que enviamos.

## Información adicional

* Para obtener más información sobre RabbitMQ, consulte el [sitio web de RabbitMQ] (https://www.rabbitmq.com/).
* Para obtener más información sobre Spring Boot, consulte el [sitio web de Spring Boot] (https://spring.io/projects/spring-boot).