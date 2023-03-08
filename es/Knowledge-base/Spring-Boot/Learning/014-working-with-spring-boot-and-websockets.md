---
title: 014: Trabajar con Spring Boot y WebSockets
description: 
published: true
date: 2023-02-03T09:18:03.826Z
tags: 
editor: markdown
dateCreated: 2023-02-03T09:17:58.710Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [014: Working with Spring Boot and WebSockets***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/014-working-with-spring-boot-and-websockets)
{.links-list}


# 014: Trabajando con Spring Boot y WebSockets

Los WebSockets son una poderosa herramienta para construir aplicaciones en tiempo real. Spring Boot facilita el trabajo con WebSockets. En esta publicación, aprenderemos cómo trabajar con Spring Boot y WebSockets.

## ¿Qué son los WebSockets?

Los WebSockets son un protocolo de comunicación que permite la comunicación full-duplex entre un cliente y un servidor. Esto significa que tanto el cliente como el servidor pueden enviar y recibir datos al mismo tiempo.

Los WebSockets son una excelente manera de crear aplicaciones en tiempo real. Son rápidos, eficientes y le permiten enviar datos al cliente tan pronto como estén disponibles.

## Configuración de Spring Boot

Comencemos configurando una aplicación Spring Boot simple. Usaremos Spring Initializr para crear nuestro proyecto.

Vaya al sitio web de Spring Initializr (https://start.spring.io/).

Elija las siguientes opciones:

- Proyecto: Proyecto Maven
- Idioma: Java
- Versión de arranque de primavera: 2.1.3
- Grupo: com.ejemplo
- Artefacto: websockets-demo

Haga clic en Generar proyecto.

Ahora debería tener un archivo zip que contiene todo lo que necesita para comenzar. Descomprima el archivo y ábralo en su IDE favorito.

## Creación de un punto final de WebSocket

Comencemos por crear un punto de enlace WebSocket simple. Usaremos la anotación @ServerEndpoint para crear nuestro punto final.

Cree una nueva clase Java en el paquete com.example.websockets.demo y asígnele el nombre MyWebSocketEndpoint.java.

Agregue el siguiente código al archivo MyWebSocketEndpoint.java:

```java
@ServerEndpoint("/websocket")
public class MyWebSocketEndpoint {

}
```

La anotación @ServerEndpoint se usa para crear un punto final de WebSocket. El valor de la anotación es la ruta que se utilizará para acceder al punto final.

## Enviar y recibir mensajes

Ahora que tenemos nuestro punto final, agreguemos algo de código para enviar y recibir mensajes.

Agregue el siguiente código al archivo MyWebSocketEndpoint.java:

```java
@ServerEndpoint("/websocket")
public class MyWebSocketEndpoint {

@OnOpen
public void onOpen(Session session) {
    // do something when the connection is opened
}

@OnMessage
public void onMessage(String message, Session session) {
    // do something when a message is received
}

@OnClose
public void onClose(Session session) {
    // do something when the connection is closed
}

@OnError
public void onError(Throwable error) {
    // do something when there is an error
}
}
```

La anotación @OnOpen se usa para especificar un método que se llamará cuando se abra una conexión. La anotación @OnMessage se usa para especificar un método que se llamará cuando se reciba un mensaje. La anotación @OnClose se usa para especificar un método que se llamará cuando se cierre una conexión. La anotación @OnError se usa para especificar un método que se llamará cuando haya un error.

## Configuración del punto final

Ahora que tenemos nuestro punto final, vamos a configurarlo.

Agregue el siguiente código al archivo MyWebSocketEndpoint.java:

```java
@ServerEndpoint("/websocket")
public class MyWebSocketEndpoint {

@OnOpen
public void onOpen(Session session) {
    // do something when the connection is opened
}

@OnMessage
public void onMessage(String message, Session session) {
    // do something when a message is received
}

@OnClose
public void onClose(Session session) {
    // do something when the connection is closed
}

@OnError
public void onError(Throwable error) {
    // do something when there is an error
}
}
```

La anotación @ServerEndpoint se usa para crear un punto final de WebSocket. El valor de la anotación es la ruta que se utilizará para acceder al punto final.

La anotación @OnOpen se usa para especificar un método que se llamará cuando se abra una conexión. La anotación @OnMessage se usa para especificar un método que se llamará cuando se reciba un mensaje. La anotación @OnClose se usa para especificar un método que se llamará cuando se cierre una conexión. La anotación @OnError se usa para especificar un método que se llamará cuando haya un error.

## Probando el punto final

Ahora que tenemos nuestro punto final, vamos a probarlo.

Cree una nueva clase Java en el paquete com.example.websockets.demo y asígnele el nombre MyWebSocketEndpointTest.java.

Agregue el siguiente código al archivo MyWebSocketEndpointTest.java:

```java
@Test
public void testMyWebSocketEndpoint() throws Exception {
    URI uri = new URI("ws://localhost:8080/websocket");
    WebSocketContainer container = ContainerProvider.getWebSocketContainer();
    Session session = container.connectToServer(MyWebSocketEndpoint.class, uri);
    session.getBasicRemote().sendText("Hello world!");
    session.close();
}
```

En el método testMyWebSocketEndpoint(), creamos un URI para nuestro punto final de WebSocket. Luego creamos un WebSocketContainer y nos conectamos a nuestro punto final. Enviamos un mensaje al servidor y luego cerramos la conexión.

Si ejecuta la prueba, debería ver el siguiente resultado:

```
Hello world!
```

## Conclusión

En esta publicación, hemos aprendido a trabajar con Spring Boot y WebSockets. Hemos creado un punto final de WebSocket simple y lo hemos probado.