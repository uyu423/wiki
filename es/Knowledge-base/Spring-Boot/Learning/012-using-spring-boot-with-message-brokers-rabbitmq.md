---
title: 012: uso de Spring Boot con intermediarios de mensajes (RabbitMQ)
description: 
published: true
date: 2023-02-01T20:26:40.247Z
tags: 
editor: markdown
dateCreated: 2023-02-01T20:26:38.532Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [012: Using Spring Boot with message brokers (RabbitMQ)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/012-using-spring-boot-with-message-brokers-rabbitmq)
{.links-list}


# 012: Uso de Spring Boot con intermediarios de mensajes (RabbitMQ)

En esta publicación, veremos cómo usar Spring Boot con intermediarios de mensajes, específicamente RabbitMQ. Cubriremos qué son los intermediarios de mensajes, cómo usarlos con Spring Boot y algunas mejores prácticas.

## ¿Qué es un intermediario de mensajes?

Un intermediario de mensajes es una pieza de software que ayuda a administrar la comunicación entre diferentes aplicaciones. Lo hace actuando como intermediario entre las aplicaciones. Las aplicaciones pueden enviar mensajes al intermediario, que luego reenvía los mensajes a las aplicaciones correspondientes.

## ¿Por qué usar un intermediario de mensajes?

Hay algunas razones por las que es posible que desee utilizar un intermediario de mensajes.

### 1. aplicaciones de desacoplamiento

Una de las principales razones para utilizar un intermediario de mensajes es desacoplar aplicaciones. Por desacoplamiento, queremos decir que las aplicaciones no dependen directamente unas de otras. Esto tiene algunos beneficios.

En primer lugar, significa que las aplicaciones se pueden desarrollar de forma independiente. Esto puede ser una gran ventaja si tiene un gran equipo trabajando en diferentes partes del sistema.

En segundo lugar, hace que las aplicaciones sean más resistentes. Si una aplicación deja de funcionar, las demás aún pueden seguir funcionando.

### 2. escalabilidad

Otra razón para usar un intermediario de mensajes es la escalabilidad. Si tiene mucho tráfico, puede agregar más intermediarios para manejar la carga. Esto es mucho más fácil que intentar escalar una sola aplicación.

## Cómo usar un intermediario de mensajes con Spring Boot

Ahora que hemos visto algunas de las razones para usar un intermediario de mensajes, veamos cómo usar uno con Spring Boot.

Spring Boot tiene un buen soporte para intermediarios de mensajes. Podemos usar la dependencia `spring-boot-starter-amqp` para agregar soporte para RabbitMQ.

Para usar RabbitMQ, debemos agregar lo siguiente a nuestro archivo `application.properties`:

```properties
spring.rabbitmq.host=localhost
spring.rabbitmq.port=5672
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```

Reemplace `localhost` con el nombre de host de su servidor RabbitMQ. El puerto predeterminado es `5672`. El nombre de usuario y la contraseña son los predeterminados para RabbitMQ.

Una vez que hemos agregado las propiedades, podemos inyectar un `RabbitTemplate` en nuestro código. Esta es la clase que usaremos para enviar y recibir mensajes.

Aquí hay un ejemplo simple de cómo usar la plantilla para enviar un mensaje:

```java
@Autowired
private RabbitTemplate rabbitTemplate;

public void sendMessage(String message) {
    rabbitTemplate.convertAndSend("exchange", "routingKey", message);
}
```

El método `convertAndSend` toma un intercambio, una clave de enrutamiento y un mensaje. El intercambio es el nombre del intercambio a utilizar. La clave de enrutamiento se utiliza para enrutar el mensaje a la cola correcta. El mensaje puede ser cualquier objeto que se pueda convertir en una matriz de bytes.

También podemos recibir mensajes usando el método `receiveAndConvert`:

```java
@Autowired
private RabbitTemplate rabbitTemplate;

public String receiveMessage() {
    return (String)rabbitTemplate.receiveAndConvert("queue");
}
```

Este método toma un nombre de cola y devuelve un objeto. Necesitamos convertir el objeto al tipo correcto.

## Mejores prácticas

Ahora que hemos visto cómo usar un intermediario de mensajes con Spring Boot, veamos algunas de las mejores prácticas.

### 1. usar convertidores de mensajes

Spring Boot viene con varios convertidores de mensajes. Estos convertidores se pueden utilizar para convertir entre diferentes formatos de mensajes. Por ejemplo, podemos usar `StringMessageConverter` para convertir entre cadenas y matrices de bytes.

Es una buena idea usar un convertidor de mensajes al enviar y recibir mensajes. De esta manera, no tenemos que preocuparnos por convertir el mensaje al formato correcto.

### 2. usar detectores de mensajes

Otra práctica recomendada es usar detectores de mensajes. Un detector de mensajes es una clase que implementa la interfaz `MessageListener`. Esta interfaz tiene un único método `onMessage`:

```java
public interface MessageListener {
    void onMessage(Message message);
}
```

Este método se llama cuando se recibe un mensaje. El mensaje se pasa como un parámetro.

Los detectores de mensajes son una buena manera de manejar los mensajes a medida que se reciben. No tenemos que preocuparnos por buscar mensajes o convertir el mensaje al formato correcto.

### 3. usa una cola de mensajes

Al usar un intermediario de mensajes, es una buena idea usar una cola de mensajes. Una cola de mensajes es una estructura de datos que almacena mensajes. Los mensajes se almacenan en el orden en que se reciben.

Se puede usar una cola de mensajes para almacenar mensajes que deben procesarse. Por ejemplo, podemos agregar mensajes a una cola a medida que se reciben. Entonces podemos procesar los mensajes en la cola uno a la vez.

Las colas de mensajes se pueden utilizar para mejorar el rendimiento. Si estamos procesando muchos mensajes, podemos procesarlos en paralelo. De esta manera, no tenemos que esperar a que se procese un mensaje antes de comenzar a procesar el siguiente mensaje.

## Información adicional

- [Guía de referencia de Spring Boot] (https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
- [Documentación de RabbitMQ](https://www.rabbitmq.com/documentation.html)

## Advertencias

- Asegúrese de utilizar el convertidor de mensajes correcto al enviar y recibir mensajes. De lo contrario, puede obtener resultados inesperados.
- Asegúrese de utilizar el detector de mensajes correcto al recibir mensajes. De lo contrario, puede perder mensajes u obtener resultados inesperados.

## Peligros

- Si no está utilizando una cola de mensajes, es posible que sus mensajes se procesen desordenadamente.
- Si no está utilizando un convertidor de mensajes, es posible que sus mensajes no se conviertan al formato correcto.