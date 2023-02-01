---
title: 012: uso de Spring Boot con intermediarios de mensajes (RabbitMQ)
description: 
published: true
date: 2023-02-01T20:12:28.402Z
tags: 
editor: markdown
dateCreated: 2023-02-01T20:12:28.402Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [012: Using Spring Boot with message brokers (RabbitMQ)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/012-using-spring-boot-with-message-brokers-rabbitmq)
{.links-list}

  
# Introducción

Los desarrolladores a menudo tienen la tarea de crear aplicaciones que necesitan interactuar entre sí o con servicios externos. Los intermediarios de mensajes son una forma común de facilitar esta comunicación y Spring Boot brinda un buen soporte para trabajar con ellos.

En este artículo, exploraremos cómo usar Spring Boot con un intermediario de mensajes. Nos centraremos en RabbitMQ, pero los mismos principios se aplicarán a otros intermediarios de mensajes.

# Configuración de un agente de mensajes

Antes de que podamos comenzar a usar un intermediario de mensajes, debemos configurar uno. A los efectos de este artículo, utilizaremos RabbitMQ, que es un popular agente de mensajes de código abierto.

Hay algunas formas diferentes de instalar RabbitMQ. La forma más fácil es usar un paquete preconstruido, que puede descargar desde el sitio web de RabbitMQ.

Una vez que RabbitMQ esté instalado, puede iniciarlo ejecutando el siguiente comando:

```
rabbitmq-server
```

RabbitMQ ahora se ejecutará en su máquina local en el puerto predeterminado (5672).

# Creación de una aplicación Spring Boot

Ahora que tenemos RabbitMQ en funcionamiento, podemos crear una aplicación Spring Boot que lo usará.

Comenzaremos creando un nuevo proyecto Spring Boot en nuestro IDE de elección. Para los propósitos de este artículo, usaremos Spring Initializr para generar nuestro proyecto.

Una vez generado el proyecto, necesitaremos agregar las siguientes dependencias:

- spring-boot-arrancador-amqp
- spring-boot-arrancador-web

La primera dependencia, spring-boot-starter-amqp, nos dará las clases y los objetos necesarios relacionados con AMQP que necesitaremos para trabajar con RabbitMQ. La segunda dependencia, spring-boot-starter-web, nos permitirá crear una aplicación web.

# Configuración del agente de mensajes

Ahora que tenemos nuestro proyecto configurado, podemos comenzar a configurar nuestro intermediario de mensajes.

RabbitMQ utiliza un concepto llamado intercambios para enrutar mensajes a las colas correctas. Hay algunos tipos diferentes de intercambios, pero usaremos el tipo de intercambio directo para este artículo.

Para crear un intercambio directo, necesitaremos agregar lo siguiente a nuestro archivo application.properties:

```
spring.rabbitmq.exchange=my-exchange
```

Esto creará un intercambio llamado my-exchange.

A continuación, necesitamos crear una cola. Podemos hacer esto agregando lo siguiente a nuestro archivo application.properties:

```
spring.rabbitmq.queue=my-queue
```

Esto creará una cola llamada my-queue.

Ahora que tenemos un intercambio y una cola, necesitamos unirlos. Podemos hacer esto agregando lo siguiente a nuestro archivo application.properties:

```
spring.rabbitmq.binding.my-exchange.queue=my-queue
```

Esto vinculará el intercambio my-exchange a la cola my-queue.

# Envío y recepción de mensajes

Ahora que nuestro intermediario de mensajes está configurado, podemos comenzar a enviar y recibir mensajes.

Comenzaremos creando un controlador simple que enviará un mensaje a nuestro intermediario de mensajes:

```java
@RestController
public class MessageController {

@Autowired
private AmqpTemplate amqpTemplate;

@GetMapping("/send-message")
public String sendMessage() {

amqpTemplate.convertAndSend("my-exchange", "my-queue", "Hello, World!");
return "Message sent!";
}
}
```

En el código anterior, hemos inyectado una instancia de AmqpTemplate en nuestro controlador. Esta plantilla se utilizará para enviar mensajes a nuestro intermediario de mensajes.

También hemos creado un punto final GET que enviará un mensaje a nuestro intermediario de mensajes. El mensaje se enrutará a la cola my-queue a través del intercambio my-exchange.

Ahora que tenemos una forma de enviar mensajes, necesitamos una forma de recibirlos. Podemos hacer esto creando un detector de mensajes simple:

```java
@Component
public class MessageListener {

@RabbitListener(queues = "my-queue")
public void handleMessage(String message) {

System.out.println("Received message: " + message);
}
}
```

En el código anterior, hemos anotado nuestro oyente con @RabbitListener. Esta anotación le dice a Spring que escuche los mensajes en la cola my-queue.

Cuando se recibe un mensaje, se invocará el método handleMessage(). Este método simplemente imprimirá el mensaje en la consola.

# Conclusión

En este artículo, exploramos cómo usar Spring Boot con un intermediario de mensajes. Nos hemos centrado en RabbitMQ, pero los mismos principios se aplicarán a otros intermediarios de mensajes.

También hemos visto cómo enviar y recibir mensajes usando Spring Boot.

Finalmente, hemos visto cómo unir un intercambio y una cola.