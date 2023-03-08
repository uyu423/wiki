---
title: Spring Boot y WebSockets para comunicación en tiempo real
description: 
published: true
date: 2023-02-04T10:56:44.390Z
tags: 
editor: markdown
dateCreated: 2023-02-04T10:56:42.584Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot and WebSockets for Real-Time Communication***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-websockets-for-real-time-communication)
{.links-list}


# Spring Boot y WebSockets para comunicación en tiempo real

Los websockets se están volviendo cada vez más populares como un medio para proporcionar comunicación en tiempo real entre los navegadores web y los servidores web. Spring Boot proporciona una manera muy conveniente de desarrollar e implementar aplicaciones web que usan Websockets.

## ¿Qué son los WebSockets?

Los WebSockets son una tecnología relativamente nueva que proporciona canales de comunicación full-duplex a través de una sola conexión TCP. Esto significa que tanto el cliente como el servidor pueden enviar y recibir datos al mismo tiempo.

Los WebSockets son particularmente adecuados para aplicaciones que requieren baja latencia, como aplicaciones de chat y juegos en línea.

## ¿Por qué usar Spring Boot?

Spring Boot es un marco muy popular para desarrollar aplicaciones Java. Hace que sea muy fácil crear e implementar aplicaciones basadas en Spring.

Spring Boot también proporciona una forma muy conveniente de desarrollar e implementar aplicaciones web que usan Websockets.

## Empezando

En esta sección, crearemos una aplicación de chat muy simple que usa WebSockets.

Utilizaremos las siguientes herramientas y tecnologías:

- Bota de primavera
- WebSockets
-Java

### Requisitos previos

Antes de comenzar, debemos asegurarnos de tener instaladas las siguientes herramientas:

-Java8
- Experto

### Creación del proyecto

Vamos a usar Spring Initializr para crear nuestro proyecto. Spring Initializr es una aplicación web que te ayuda a crear proyectos basados en Spring.

Vaya a http://start.spring.io y seleccione las siguientes opciones:

- Generar un Proyecto Maven con Java y Spring Boot 1.4
- Internet
- WebSocket
- Hoja de tomillo

Haga clic en "Generar proyecto" para descargar el proyecto.

### Configuración del proyecto

Una vez que tenga el proyecto, debe importarlo a su IDE favorito. Estoy usando IntelliJ IDEA.

Una vez que se importa el proyecto, debería ver la siguiente estructura del proyecto:

```
├── pom.xml
└── src
    └── main
        ├── java
        │   └── com
        │       └── example
        │           └── websockets
        │               └── Application.java
        └── resources
            ├── application.properties
            └── templates
                └── index.html
```

### Implementación del controlador WebSocket

Comenzaremos implementando el controlador WebSocket. Este es el componente que recibirá mensajes del cliente y enviará mensajes al cliente.

Cree una nueva clase Java llamada `MessageHandler` en el paquete `com.example.websockets`.

Agrega el siguiente código a la clase `MessageHandler`:

```java
@Component
public class MessageHandler {

    private final SimpMessagingTemplate messagingTemplate;

    @Autowired
    public MessageHandler(SimpMessagingTemplate messagingTemplate) {
        this.messagingTemplate = messagingTemplate;
    }

    @MessageMapping("/send/message")
    public void onReceiveMessage(String message) {
        System.out.println("Received message: " + message);
        messagingTemplate.convertAndSend("/topic/messages", message);
    }
}
```

Echemos un vistazo a lo que está pasando en la clase `MessageHandler`.

Primero, anotamos la clase con `@Component`. Esto le dice a Spring que este es un componente que se puede inyectar en otros componentes.

A continuación, creamos un campo `SimpMessagingTemplate` y lo anotamos con `@Autowired`. Esto le dice a Spring que inyecte una instancia de `SimpMessagingTemplate` en este campo.

`SimpMessagingTemplate` es un componente proporcionado por Spring para enviar mensajes a clientes a través de WebSockets.

A continuación, creamos un constructor que toma `SimpMessagingTemplate` como parámetro. Se llama a este constructor cuando Spring inyecta una instancia de `SimpMessagingTemplate` en el campo `messagingTemplate`.

Finalmente, tenemos un método anotado `@MessageMapping` llamado `onReceiveMessage`. Este método se llama cuando se envía un mensaje al extremo `/send/message`.

La anotación `@MessageMapping` le dice a Spring que se debe llamar a este método cuando se recibe un mensaje en el extremo `/send/message`.

El método `onReceiveMessage` toma un parámetro `String`. Este es el mensaje que se envió desde el cliente.

Dentro del método `onReceiveMessage`, imprimimos el mensaje en la consola y luego usamos `messagingTemplate` para enviar el mensaje al extremo `/topic/messages`.

El punto final `/topic/messages` es un tema al que están suscritos todos los clientes. Cuando se envía un mensaje a este extremo, todos los clientes que están suscritos al tema recibirán el mensaje.

### Implementando la configuración de WebSocket

A continuación, debemos implementar la configuración de WebSocket. Este es el componente que configurará la conexión WebSocket.

Cree una nueva clase Java llamada `WebSocketConfig` en el paquete `com.example.websockets`.

Agrega el siguiente código a la clase `WebSocketConfig`:

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {

    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {
        registry.enableSimpleBroker("/topic");
        registry.setApplicationDestinationPrefixes("/app");
    }

    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        registry.addEndpoint("/websocket").withSockJS();
    }
}
```

Echemos un vistazo a lo que está pasando en la clase `WebSocketConfig`.

Primero, anotamos la clase con `@Configuration` y `@EnableWebSocketMessageBroker`. La anotación `@Configuration` le dice a Spring que esta es una clase de configuración. La anotación `@EnableWebSocketMessageBroker` habilita el intermediario de mensajes WebSocket.

A continuación, implementamos la interfaz `WebSocketMessageBrokerConfigurer`. Esta interfaz proporciona métodos para configurar el intermediario de mensajes WebSocket.

Anulamos el método `configureMessageBroker`. Este método se utiliza para configurar el intermediario de mensajes.

En el método `configureMessageBroker`, habilitamos el intermediario simple y establecemos el prefijo de destino de la aplicación.

El intermediario simple es un intermediario de mensajes que admite mensajes de publicación/suscripción. Es muy simple de usar y es lo que usaremos en este ejemplo.

El prefijo de destino de la aplicación se utiliza para prefijar el destino de todos los mensajes que se envían desde el cliente.

Finalmente, anulamos el método `registerStompEndpoints`. Este método se utiliza para registrar puntos finales STOMP. STOMP es un protocolo de mensajería simple orientado a texto.

En el método `registerStompEndpoints`, agregamos un punto final que se asigna a la URL `/websocket`. También configuramos el punto final para usar SockJS.

SockJS es una biblioteca de JavaScript del lado del cliente que proporciona una manera conveniente de usar STOMP sobre WebSockets.

### Implementación del controlador web

A continuación, necesitamos implementar el controlador web. Este es el componente que manejará las solicitudes web.

Cree una nueva clase Java llamada `WebController` en el paquete `com.example.websockets`.

Agrega el siguiente código a la clase `WebController`:

```java
@Controller
public class WebController {

    @GetMapping("/")
    public String index() {
        return "index";
    }
}
```

Echemos un vistazo a lo que está pasando en la clase `WebController`.

Primero, anotamos la clase con `@Controller`. Esto le dice a Spring que este es un controlador web.

A continuación, tenemos un método anotado `@GetMapping` llamado `index`. Este método se llama cuando se realiza una solicitud GET a la URL `/`.

Dentro del método `index`, devolvemos la plantilla `index`. La plantilla `index` se encuentra en el directorio `resources/templates`.

### Implementación de la plantilla de índice

A continuación, debemos implementar la plantilla `index`.

Abra el archivo `resources/templates/index.html` y agregue el siguiente código:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>WebSocket Chat</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/sockjs-client/1.1.2/sockjs.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/stomp.js/2.3.3/stomp.min.js"></script>
</head>
<body>

<h1>WebSocket Chat</h1>

<form id="message-form">
    <label for="message-input">Message:</label>
    <input type="text" id="message-input" placeholder="Enter a message">
    <button type="submit">Send</button>
</form>

<ul id="messages">
    <!-- Messages will be inserted here -->
</ul>

<script>
    var stompClient = null;

    function connect() {
        var socket = new SockJS('/websocket');
        stompClient = Stomp.over(socket);

        stompClient.connect({}, function (frame) {
            console.log('Connected: ' + frame);
            stompClient.subscribe('/topic/messages', function (message) {
                showMessage(JSON.parse(message.body).message);
            });
        });
    }

    function disconnect() {
        if (stompClient !== null) {
            stompClient.disconnect();
        }
        console.log("Disconnected");
    }

    function sendMessage() {
        var message = document.getElementById('message-input').value;
        stompClient.send("/app/send/message", {}, JSON.stringify({'message': message}));
    }

    function showMessage(message) {
        var messages = document.getElementById('messages');
        var li = document.createElement('li');
        li.appendChild(document.createTextNode(message));
        messages.appendChild(li);
    }

    connect();
</script>

</body>
</html>
```

Echemos un vistazo a lo que está pasando en la plantilla `index`.

Primero, incluimos las bibliotecas de JavaScript `sockjs` y `stomp`. El cliente utiliza estas bibliotecas para conectarse al servidor WebSocket.

A continuación, tenemos un elemento `<form>` con un `id` de `message-form`. Este elemento `<form>` se utiliza para enviar mensajes al servidor.

Dentro del elemento `<form>`, tenemos un elemento `<label>` y un elemento `<input>`. El elemento `<input>` se usa para ingresar el mensaje que se enviará al servidor.

Finalmente, tenemos un elemento `<ul>` con un `id` de `messages`. Este elemento `<ul>` se utiliza para mostrar los mensajes que se reciben del servidor.

Debajo del elemento `<ul>`, tenemos un elemento `<script>` de JavaScript. Este elemento `<script>` contiene el código para conectarse al servidor WebSocket y enviar y recibir mensajes.

Primero, creamos una variable `stompClient`. Esta variable se utiliza para almacenar el cliente STOMP.

A continuación, tenemos una función `conectar`. Esta función se utiliza para conectarse al servidor WebSocket.

Dentro de la función `connect`, creamos una nueva instancia `SockJS` y pasamos la URL `/websocket` al constructor. Esta URL es el punto final que configuramos en la clase `WebSocketConfig`.

Luego creamos una nueva instancia `stompClient` y pasamos la instancia `SockJS` al constructor.

A continuación, llamamos al método `connect` en la instancia `stompClient`. Este método toma dos argumentos. El primer argumento es un objeto vacío y el segundo argumento es una función de devolución de llamada.

La función de devolución de llamada se llama cuando se establece la conexión.

Dentro de la función de devolución de llamada, nos suscribimos al tema `/topic/messages`. Este es el tema en el que la clase `MessageHandler` está publicando mensajes.

Cuando se recibe un mensaje sobre este tema, se llama a la función de devolución de llamada con el mensaje como argumento.

En la función de devolución de llamada, llamamos a la función `showMessage` y pasamos el mensaje a la función.

La función `showMessage` toma un mensaje como argumento y agrega el mensaje a `messages` `<ul>`.

Finalmente, tenemos una función `desconectar`. Esta función se utiliza para desconectarse del servidor WebSocket.

Dentro de la función `disconnect`, comprobamos si la variable `stompClient` no es `null`. Si no es `null`, llamamos al método `disconnect` en la instancia `stompClient`.

También tenemos una función `sendMessage`. Esta función se utiliza para enviar un mensaje al servidor.

Dentro de la función `sendMessage`, obtenemos el mensaje del elemento `<input>` de `message-input` y lo almacenamos en una variable llamada `message`.

Luego llamamos al método `send` en la instancia `stompClient` y pasamos el destino, los encabezados y el cuerpo al método.

El destino es el punto final al que queremos enviar el mensaje. En este caso, queremos enviar el mensaje al extremo `/app/send/message`. Este es el punto final que configuramos en la clase `MessageHandler`.

Los encabezados y el cuerpo son opcionales. No necesitamos establecer los encabezados en este ejemplo, por lo que solo pasamos un objeto vacío.

El cuerpo es el mensaje que queremos enviar al servidor. Usamos la función `JSON.stringify` para convertir el mensaje en una cadena JSON.

Finalmente, tenemos una función `showMessage`. Esta función se utiliza para mostrar un mensaje en `messages` `<ul>`.

Dentro de la función `showMessage`, obtenemos los `mensajes` `<ul>` y los almacenamos en una variable llamada `messages`.

Luego creamos un nuevo elemento `<li>` y lo almacenamos en una variable llamada `li`.

Luego creamos un nuevo `TextNode` con el mensaje como texto y lo agregamos al elemento `<li>`.

Finalmente, agregamos el elemento `<li>` a los `mensajes` `<ul>`.

Al final de la plantilla `index`, llamamos a la función `connect`. Esto conectará al cliente con el servidor WebSocket.

### Prueba de la aplicación

Ahora que hemos implementado la aplicación, vamos a probarla.

Inicie la aplicación ejecutando la clase `Application`.

Una vez que se inicia la aplicación, abra un navegador web y vaya a http://localhost:8080.

Deberías ver la siguiente página:

![Página de chat de WebSocket](https://i.imgur.com/uGjTtqP.png)

Introduzca un mensaje en el campo `Mensaje` y haga clic en el botón `Enviar`.

Debería ver aparecer el mensaje en la lista `Mensajes`.

![Página de chat de WebSocket con mensaje](https://i.imgur.com/DVnWql6.png)

## Conclusión

En este artículo, hemos visto cómo usar Spring Boot y WebSockets para crear una aplicación de chat en tiempo real.

También hemos visto cómo usar `SimpMessagingTemplate` para enviar mensajes a clientes a través de WebSockets.

## Referencias

- [Documentación de referencia de Spring Boot](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
- [WebSocket](https://en.wikipedia.org/wiki/WebSocket)
- [Spring Boot y WebSockets](https://spring.io/guides/gs/messaging-stomp-websocket/)
- [Uso de WebSockets para crear una aplicación de chat