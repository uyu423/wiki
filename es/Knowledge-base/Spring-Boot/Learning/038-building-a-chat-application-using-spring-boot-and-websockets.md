---
title: 038: Creación de una aplicación de chat con Spring Boot y WebSockets
description: 
published: true
date: 2023-02-04T06:32:23.482Z
tags: 
editor: markdown
dateCreated: 2023-02-04T06:32:21.670Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [038: Building a chat application using Spring Boot and WebSockets***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/038-building-a-chat-application-using-spring-boot-and-websockets)
{.links-list}


# 038: Construyendo una aplicación de chat usando Spring Boot y WebSockets

Los WebSockets son una poderosa herramienta para crear aplicaciones en tiempo real, como aplicaciones de chat. En esta publicación, le mostraremos cómo crear una aplicación de chat con Spring Boot y WebSockets.

## Configurando tu proyecto

Para comenzar, deberá crear un nuevo proyecto Spring Boot. Puede hacerlo usando [Spring Initializr](https://start.spring.io/). Asegúrese de seleccionar las dependencias Web y WebSocket.

Una vez que haya configurado su proyecto, deberá agregar la siguiente dependencia a su `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-websocket</artifactId>
</dependency>
```

## Configuración de WebSockets

A continuación, deberá configurar WebSockets en su archivo `application.properties`:

```properties
server.port=8080

spring.websocket.server.port=8081
spring.websocket.server.path=/ws
```

## Creando el punto final de WebSocket

Ahora que tiene su proyecto configurado, puede comenzar a construir el punto final de WebSocket. Cree una nueva clase llamada `ChatEndpoint` y anótela con `@ServerEndpoint`. Esta anotación le dirá a Spring que esta clase es un punto final de WebSocket.

```java
@ServerEndpoint("/ws")
public class ChatEndpoint {

}
```

## Enviar y recibir mensajes

El siguiente paso es agregar métodos para enviar y recibir mensajes. La anotación `@OnMessage` se utilizará para marcar un método como controlador de mensajes. Se llamará a este método cada vez que se reciba un mensaje en el extremo de WebSocket.

```java
@OnMessage
public void handleMessage(String message, Session session) {
    // do something with the message
}
```

Para enviar un mensaje, puede usar el método `Session.getBasicRemote().sendText(message)`.

```java
@OnMessage
public void handleMessage(String message, Session session) {
    session.getBasicRemote().sendText("Echo: " + message);
}
```

## Probando la aplicación de chat

Puede probar su aplicación de chat usando la [prueba de eco de WebSocket.org] (https://www.websocket.org/echo.html). Ingrese su punto final de WebSocket (ws://localhost:8081/ws) y comience a enviar mensajes. Deberías ver los mensajes que envías de vuelta a ti.

## Conclusión

En esta publicación, le mostramos cómo crear una aplicación de chat con Spring Boot y WebSockets. Los WebSockets son una poderosa herramienta para crear aplicaciones en tiempo real.