---
title: 037: Implementación de chat en tiempo real con Nest.js y WebSockets
description: 
published: true
date: 2023-02-02T05:47:42.315Z
tags: 
editor: markdown
dateCreated: 2023-02-02T05:47:40.627Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [037: Implementing real-time chat with Nest.js and WebSockets***English** document is available*](/en/Knowledge-base/Nest-js/Learning/037-implementing-real-time-chat-with-nest-js-and-websockets)
{.links-list}


# 037: Implementando chat en tiempo real con Nest.js y WebSockets

En esta publicación, le mostraremos cómo agregar fácilmente capacidades de chat en tiempo real a una aplicación web Nest.js utilizando el protocolo WebSocket.

## ¿Qué es WebSocket?

WebSocket es un protocolo de comunicación que permite la comunicación bidireccional de dúplex completo entre un navegador web y un servidor web. En otras palabras, permite la comunicación bidireccional entre un cliente y un servidor en tiempo real.

## ¿Por qué usar WebSocket?

WebSocket es una excelente opción para crear aplicaciones en tiempo real, como aplicaciones de chat, porque proporciona una conexión persistente entre un cliente y un servidor. Esto significa que una vez que se establece una conexión, tanto el cliente como el servidor pueden enviar y recibir datos en cualquier momento.

## ¿Cómo funciona WebSocket?

El protocolo WebSocket utiliza un apretón de manos para establecer una conexión entre un cliente y un servidor. Una vez establecida la conexión, el cliente y el servidor pueden enviar y recibir datos en tiempo real.

## ¿Qué es Nest.js?

Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor. Utiliza JavaScript moderno, está construido con TypeScript (lo que le da un tipeo fuerte) y combina elementos de Programación Orientada a Objetos, Programación Funcional y Programación Reactiva.

## ¿Por qué usar Nest.js?

Nest.js es una excelente opción para crear aplicaciones del lado del servidor, ya que se basa en Node.js, que es una plataforma conocida por su escalabilidad. Además, Nest.js usa TypeScript, lo que le da una tipificación fuerte y una base de código más estructurada. Finalmente, Nest.js combina elementos de Programación Orientada a Objetos, Programación Funcional y Programación Reactiva, lo que lo convierte en un marco muy poderoso.

## ¿Cómo funciona Nest.js?

Nest.js se basa en Node.js, que es una plataforma conocida por su escalabilidad. Además, Nest.js usa TypeScript, lo que le da una tipificación fuerte y una base de código más estructurada. Finalmente, Nest.js combina elementos de Programación Orientada a Objetos, Programación Funcional y Programación Reactiva, lo que lo convierte en un marco muy poderoso.

## Cómo agregar chat en tiempo real a una aplicación web Nest.js usando WebSocket

En esta sección, le mostraremos cómo agregar funciones de chat en tiempo real a una aplicación web Nest.js mediante el protocolo WebSocket.

### Paso 1: Crear un proyecto Nest.js

Primero, deberá crear un proyecto Nest.js. Si no tiene Nest.js instalado, puede instalarlo usando el siguiente comando:

```
npm install -g @nestjs/cli
```

Una vez que se instala Nest.js, puede crear un nuevo proyecto de Nest.js con el siguiente comando:

```
nest new project-name
```

### Paso 2: Instale el módulo WebSocket

A continuación, deberá instalar el módulo WebSocket. El módulo WebSocket es un módulo de Node.js que le permite trabajar con el protocolo WebSocket.

Puede instalar el módulo WebSocket usando el siguiente comando:

```
npm install --save @nestjs/websockets
```

### Paso 3: habilite el módulo WebSocket

Una vez que el módulo WebSocket esté instalado, deberá habilitarlo en su aplicación Nest.js. Puede hacerlo agregando la siguiente línea de código al archivo src/app.module.ts:

```typescript
@Module({
  imports: [
    // ...
    WebsocketsModule.forRoot(),
  ],
  // ...
})
export class AppModule {}
```

### Paso 4: Cree una puerta de enlace WebSocket

A continuación, deberá crear una puerta de enlace WebSocket. Una puerta de enlace WebSocket es un servicio de Nest.js que gestiona las conexiones WebSocket entrantes.

Puede crear una puerta de enlace WebSocket con el siguiente comando:

```
nest generate gateway websocket
```

Esto generará un nuevo archivo, src/websocket/websocket.gateway.ts.

### Paso 5: Manejar las conexiones WebSocket entrantes

Una vez que haya creado la puerta de enlace WebSocket, deberá manejar las conexiones WebSocket entrantes. Puede hacerlo agregando el siguiente código al archivo src/websocket/websocket.gateway.ts:

```typescript
@WebSocketGateway()
export class WebsocketGateway {

  @WebSocketServer()
  server;

  @WebSocketConnect()
  connect(@ConnectedSocket() socket) {
    // ...
  }

  @WebSocketDisconnect()
  disconnect(@ConnectedSocket() socket) {
    // ...
  }

}
```

El decorador @WebSocketGateway() se usa para crear una puerta de enlace WebSocket. El decorador @WebSocketServer() se usa para inyectar el servidor WebSocket en la puerta de enlace WebSocket. El decorador @WebSocketConnect() se usa para manejar las conexiones WebSocket entrantes. El decorador @WebSocketDisconnect() se usa para controlar las desconexiones de WebSocket.

### Paso 6: Crea un servicio de chat

A continuación, deberá crear un servicio de chat. El servicio de chat será el encargado de enviar y recibir mensajes.

Puede crear un servicio de chat con el siguiente comando:

```
nest generate service chat
```

Esto generará un nuevo archivo, src/chat/chat.service.ts.

### Paso 7: implementar el servicio de chat

Una vez que haya creado el servicio de chat, deberá implementarlo. Puede hacerlo agregando el siguiente código al archivo src/chat/chat.service.ts:

```typescript
@Injectable()
export class ChatService {

  constructor(
    private readonly websocketGateway: WebsocketGateway,
  ) {}

  sendMessage(message: string) {
    // ...
  }

  getMessages() {
    // ...
  }

}
```

La clase ChatService tiene dos métodos: sendMessage() y getMessages(). El método sendMessage() se usa para enviar mensajes al servicio de chat. El método getMessages() se usa para recibir mensajes del servicio de chat.

### Paso 8: crea un controlador de chat

A continuación, deberá crear un controlador de chat. El controlador de chat será responsable de manejar las solicitudes HTTP.

Puede crear un controlador de chat con el siguiente comando:

```
nest generate controller chat
```

Esto generará un nuevo archivo, src/chat/chat.controller.ts.

### Paso 9: implementar el controlador de chat

Una vez que haya creado el controlador de chat, deberá implementarlo. Puede hacerlo agregando el siguiente código al archivo src/chat/chat.controller.ts:

```typescript
@Controller('chat')
export class ChatController {

  constructor(
    private readonly chatService: ChatService,
  ) {}

  @Get()
  getMessages() {
    // ...
  }

  @Post()
  sendMessage(@Body() message: string) {
    // ...
  }

}
```

La clase ChatController tiene dos métodos: getMessages() y sendMessage(). El método getMessages() se usa para manejar solicitudes GET. El método sendMessage() se usa para manejar las solicitudes POST.

### Paso 10: Conecte el servicio de chat a la puerta de enlace WebSocket

En este paso, deberá conectar el servicio de chat a la puerta de enlace WebSocket. Puede hacerlo agregando el siguiente código al archivo src/chat/chat.service.ts:

```typescript
@Injectable()
export class ChatService {

  constructor(
    private readonly websocketGateway: WebsocketGateway,
  ) {}

  sendMessage(message: string) {
    this.websocketGateway.server.emit('message', message);
  }

  getMessages() {
    // ...
  }

}
```

El método sendMessage() usa el método emit() para enviar mensajes al servidor WebSocket.

### Paso 11: Conecte el controlador de chat al servicio de chat

En este paso, deberá conectar el controlador de chat al servicio de chat. Puede hacerlo agregando el siguiente código al archivo src/chat/chat.controller.ts:

```typescript
@Controller('chat')
export class ChatController {

  constructor(
    private readonly chatService: ChatService,
  ) {}

  @Get()
  getMessages() {
    return this.chatService.getMessages();
  }

  @Post()
  sendMessage(@Body() message: string) {
    this.chatService.sendMessage(message);
  }

}
```

El método getMessages() usa el método getMessages() para obtener mensajes del servicio de chat. El método sendMessage() utiliza el método sendMessage() para enviar mensajes al servicio de chat.

### Paso 12: Pruebe la aplicación de chat

Para probar la aplicación de chat, puede utilizar una herramienta como Postman.

Primero, deberá iniciar la aplicación Nest.js. Puede hacer esto ejecutando el siguiente comando:

```
npm start
```

A continuación, deberá enviar una solicitud POST al extremo de /chat. Puede hacerlo utilizando la siguiente URL:

```
http://localhost:3000/chat
```

En el cuerpo de la solicitud, deberá incluir un mensaje. Por ejemplo, podría utilizar el siguiente mensaje:

```
Hello, world!
```

Una vez que haya enviado la solicitud, debería ver aparecer el mensaje en la consola.

## Conclusión

En esta publicación, le mostramos cómo agregar fácilmente capacidades de chat en tiempo real a una aplicación web Nest.js utilizando el protocolo WebSocket.