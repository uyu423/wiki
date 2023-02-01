---
title: 012: uso de Spring Boot con intermediarios de mensajes (RabbitMQ)
description: 
published: true
date: 2023-02-01T20:07:29.678Z
tags: 
editor: markdown
dateCreated: 2023-02-01T20:07:29.678Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [012: Using Spring Boot with message brokers (RabbitMQ)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/012-using-spring-boot-with-message-brokers-rabbitmq)
{.links-list}
 Debería ser capaz de entender el artículo con sólo leerlo.

# Introducción

Con el lanzamiento de Spring Boot 2.0, se introdujo una nueva característica llamada `spring-boot-starter-amqp`. Esto permite una integración más sencilla de las aplicaciones Spring Boot con intermediarios de mensajes, como RabbitMQ. En este artículo, veremos cómo usar esta nueva función para conectar una aplicación Spring Boot a una instancia de RabbitMQ.

# Configuración de RabbitMQ

Lo primero que debemos hacer es configurar un servidor RabbitMQ. Si aún no tiene RabbitMQ instalado, puede seguir las instrucciones [aquí] (https://www.rabbitmq.com/download.html). Una vez que RabbitMQ esté en funcionamiento, podemos crear una nueva cola ejecutando el siguiente comando:

```
rabbitmqctl create_queue mi cola
```

# Creación de una aplicación Spring Boot

Ahora que tenemos configurado RabbitMQ, podemos crear una aplicación Spring Boot que lo usará. Comenzaremos creando un nuevo proyecto Maven con la dependencia `spring-boot-starter-amqp`:

```xml
<dependencias>
<dependencia>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-iniciador-amqp</artifactId>
</dependencia>
</dependencias>
```

A continuación, debemos configurar la conexión a nuestro servidor RabbitMQ. Podemos hacer esto agregando las siguientes propiedades a nuestro archivo `application.properties`:

```propiedades
primavera.rabbitmq.host=localhost
spring.rabbitmq.port=5672
spring.rabbitmq.username=invitado
spring.rabbitmq.contraseña=invitado
```

# Enviando mensajes

Ahora que nuestra aplicación está configurada y conectada a RabbitMQ, podemos comenzar a enviar mensajes. Haremos esto creando un nuevo bean `MessageProducer` e inyectándolo en nuestro `MessageController`:

```java
@Componente
public class MessageProducer {

@autocableado
RabbitTemplate privado RabbitTemplate;

public void sendMessage(Mensaje de cadena) {
rabbitTemplate.convertAndSend("mi cola", mensaje);
}
}

@RestController
Clase pública MessageController {

@autocableado
privado Productor de mensajes Productor de mensajes;

@PostMapping("/mensajes")
public void sendMessage(@RequestBody String mensaje) {
mensajeProducer.sendMessage(mensaje);
}
}
```

En el código anterior, estamos usando `RabbitTemplate` para enviar un mensaje a nuestra cola `my-queue`. Podemos probar esto enviando una solicitud POST al extremo `/messages` con un cuerpo de mensaje:

```
curl -X POST -H "Tipo de contenido: texto/sin formato" -d "¡Hola, mundo!" http://localhost:8080/mensajes
```

# Recibiendo Mensajes

Ahora que podemos enviar mensajes, configuremos nuestra aplicación para recibirlos. Haremos esto creando un nuevo bean `MessageConsumer` e inyectándolo en nuestro `MessageController`:

```java
@Componente
Consumidor de mensajes de clase pública {

@autocableado
RabbitTemplate privado RabbitTemplate;

cadena pública recibir mensaje () {
return (String) rabbitTemplate.receiveAndConvert("my-queue");
}
}

@RestController
Clase pública MessageController {

@autocableado
privado Productor de mensajes Productor de mensajes;

@autocableado
privado MensajeConsumidor mensajeConsumidor;

@PostMapping("/mensajes")
public void sendMessage(@RequestBody String mensaje) {
mensajeProducer.sendMessage(mensaje);
}

@GetMapping("/mensajes")
cadena pública getMessage() {
devolver mensajeConsumidor.recibirMensaje();
}
}
```

En el código anterior, estamos usando `RabbitTemplate` para recibir un mensaje de nuestra cola `my-queue`. Podemos probar esto enviando una solicitud GET al extremo `/messages`:

```
curl http://localhost:8080/mensajes
```

# Conclusión

En este artículo, hemos visto cómo usar el nuevo `spring-boot-starter-amqp` para integrar fácilmente una aplicación Spring Boot con un intermediario de mensajes, como RabbitMQ. También hemos visto cómo usar `RabbitTemplate` para enviar y recibir mensajes.