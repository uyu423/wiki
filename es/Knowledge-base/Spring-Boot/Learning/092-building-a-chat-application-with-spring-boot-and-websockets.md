---
title: 092: Creación de una aplicación de chat con Spring Boot y WebSockets
description: 
published: true
date: 2023-02-05T22:32:31.811Z
tags: 
editor: markdown
dateCreated: 2023-02-05T22:32:30.224Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [092: Building a Chat Application with Spring Boot and WebSockets***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/092-building-a-chat-application-with-spring-boot-and-websockets)
{.links-list}


# 092: Creación de una aplicación de chat con Spring Boot y WebSockets

En esta publicación, veremos cómo crear una aplicación de chat con Spring Boot y WebSockets.

Los WebSockets son una conexión bidireccional, dúplex completa y persistente entre un navegador web y un servidor. Permiten la comunicación en tiempo real entre los dos.

Spring Boot es un marco basado en Java que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

## Configuración del proyecto

Usaremos Spring Initializr para configurar nuestro proyecto. Vaya a https://start.spring.io/ y seleccione lo siguiente:

* Internet
* WebSocket
* Hoja de tomillo

Nombre el proyecto "aplicación de chat" y haga clic en "Generar proyecto".

## Dependencias

Spring Boot configurará automáticamente las dependencias necesarias para nuestro proyecto.

## WebSockets

WebSockets son manejados por un controlador. En nuestro proyecto, crearemos un controlador llamado `ChatController.java`.

```java
@Controller
public class ChatController {

    @MessageMapping("/chat")
    @SendTo("/topic/messages")
    public String sendMessage(String message) {
        return message;
    }
}
```

La anotación `@MessageMapping` asigna una URL específica al método del controlador. La anotación `@SendTo` especifica la URL del extremo del servidor WebSocket. Luego, el mensaje se transmite a todos los clientes conectados a ese punto final.

En nuestro archivo HTML, agregaremos un formulario con un campo de entrada y un botón de envío. El formulario enviará POST al extremo `/chat`.

```html
<form action="/chat" th:action="@{/chat}" th:object="${message}" method="post">
    <input type="text" th:field="*{text}"/>
    <input type="submit" value="Send"/>
</form>
```

El campo de entrada está vinculado a la propiedad `texto` del objeto `mensaje`. Cuando se envía el formulario, el objeto `message` se pasa al método `sendMessage` del `ChatController` y la propiedad `text` se usa como el mensaje que se transmitirá.

## Mensajes de difusión

Podemos usar `SimpMessagingTemplate` para transmitir mensajes a un destino específico.

```java
@Autowired
private SimpMessagingTemplate template;

@MessageMapping("/chat")
@SendTo("/topic/messages")
public String sendMessage(String message) {
    this.template.convertAndSend("/topic/messages", message);
    return message;
}
```

El método `convertAndSend` convierte el mensaje a JSON y lo envía al destino especificado.

## Recibir mensajes

Podemos usar la anotación `@SubscribeMapping` para asignar una URL específica a un método. El método se invocará cuando un cliente se suscriba a la URL.

```java
@Controller
public class ChatController {

    @Autowired
    private SimpMessagingTemplate template;

    @MessageMapping("/chat")
    @SendTo("/topic/messages")
    public String sendMessage(String message) {
        this.template.convertAndSend("/topic/messages", message);
        return message;
    }

    @SubscribeMapping("/topic/messages")
    public List<String> subscribe() {
        List<String> messages = new ArrayList<>();
        messages.add("Hello");
        messages.add("Welcome");
        return messages;
    }
}
```

El método `subscribe` devuelve una lista de mensajes que se enviarán al cliente cuando se suscriba al destino `/tema/mensajes`.

## Prueba de la aplicación

Podemos probar nuestra aplicación ejecutándola y yendo a http://localhost:8080/. Deberíamos ver el formulario y la lista de mensajes.

También podemos abrir las herramientas de desarrollo del navegador e ir a la pestaña Red. Deberíamos ver que se establece la conexión WebSocket.

## Conclusión

En esta publicación, hemos visto cómo crear una aplicación de chat con Spring Boot y WebSockets.