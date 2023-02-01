---
title: 037: Implementación de chat en tiempo real con Nest.js y WebSockets
description: 
published: true
date: 2023-02-01T20:59:16.264Z
tags: 
editor: markdown
dateCreated: 2023-02-01T20:59:16.264Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [037: Implementing real-time chat with Nest.js and WebSockets***English** document is available*](/en/Knowledge-base/Nest-js/Learning/037-implementing-real-time-chat-with-nest-js-and-websockets)
{.links-list}


# Implementando chat en tiempo real con Nest.js y WebSockets

Los WebSockets son una tecnología popular para la comunicación en tiempo real en la web. Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor. En esta publicación, veremos cómo usar Nest.js y WebSockets para crear una aplicación de chat simple.

## ¿Qué son los WebSockets?

Los WebSockets son un protocolo de comunicación que permite la comunicación full-duplex y en tiempo real entre clientes y servidores. Full-duplex significa que tanto el cliente como el servidor pueden enviar y recibir datos al mismo tiempo. En tiempo real significa que los datos se envían y reciben a medida que suceden, sin ningún retraso.

Los WebSockets son diferentes del modelo tradicional de comunicación de solicitud-respuesta en la web. Con solicitud-respuesta, el cliente envía una solicitud al servidor y luego espera una respuesta. Con WebSockets, la conexión se mantiene abierta y ambos lados pueden enviar datos en cualquier momento.

## Configuración de un proyecto Nest.js

Comenzaremos configurando un nuevo proyecto Nest.js. Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor.

Para configurar un nuevo proyecto Nest.js, podemos usar la CLI de Nest. Primero, necesitamos instalar la CLI de Nest. Podemos hacer esto con npm:

```
npm install -g @nestjs/cli
```

Una vez que se instala Nest CLI, podemos usarlo para crear un nuevo proyecto. Llamaremos a nuestro proyecto `nestjs-websockets-chat`:

```
nest new nestjs-websockets-chat
```

Esto creará un nuevo directorio llamado `nestjs-websockets-chat` con nuestro proyecto Nest.js dentro.

## Instalando las dependencias

Necesitamos dos dependencias para nuestra aplicación de chat:

- `@nestjs/websockets`: este es el módulo Nest.js para trabajar con WebSockets
- `ws`: esta es una biblioteca popular de WebSocket

Podemos instalar estas dependencias con npm:

```
npm install --save @nestjs/websockets ws
```

## Creando el servidor de chat

Ahora que tenemos nuestro proyecto configurado, podemos comenzar a construir el servidor de chat.

Primero, necesitamos crear un nuevo archivo llamado `chat.controller.ts` en el directorio `src/`. Este archivo contendrá el controlador de nuestro servidor de chat.

En `chat.controller.ts`, necesitamos importar los decoradores `Controller` y `WebSocketGateway` desde `@nestjs/websockets`. También necesitamos importar la clase `WsException` desde `@nestjs/websockets`. Usaremos esto para manejar errores en nuestro servidor de chat.

```typescript
import { Controller, WebSocketGateway, WsException } from '@nestjs/websockets';
```

A continuación, usaremos el decorador `@Controller` para definir nuestro controlador. El decorador `@Controller` toma una ruta como argumento. Esta es la ruta en la que se podrá acceder a nuestro controlador. Estableceremos la ruta a `/chat`.

```typescript
@Controller('/chat')
```

Ahora, usaremos el decorador `@WebSocketGateway` para definir nuestra puerta de enlace WebSocket. El decorador `@WebSocketGateway` toma un objeto de opciones como argumento. Estableceremos la opción `port` en `3001`. Este es el puerto en el que se ejecutará nuestro servidor WebSocket.

```typescript
@WebSocketGateway({ port: 3001 })
```

Ahora que hemos definido nuestro controlador y puerta de enlace, podemos comenzar a agregar métodos.

El primer método que agregaremos es `handleConnection`. Este método se llamará cuando un cliente se conecte a nuestro servidor WebSocket. Usaremos el decorador `@WebSocketServer()` para inyectar la instancia del servidor `WebSocket` en este método.

```typescript
@WebSocketServer() server;

@WebSocketGateway()
  handleConnection(client) {
    // ...
  }
```

A continuación, agregaremos un método `handleDisconnect`. Este método se llamará cuando un cliente se desconecte de nuestro servidor WebSocket. Usaremos el decorador `@WebSocketServer()` para inyectar la instancia del servidor `WebSocket` en este método.

```typescript
@WebSocketServer() server;

@WebSocketGateway()
  handleDisconnect(client) {
    // ...
  }
```

Finalmente, agregaremos un método `message`. Este método se llamará cuando un cliente envíe un mensaje a nuestro servidor WebSocket. Usaremos el decorador `@MessageMapping()` para asignar este método al evento `message`. También usaremos el decorador `@WebSocketServer()` para inyectar la instancia del servidor `WebSocket` en este método.

```typescript
@WebSocketServer() server;

@WebSocketGateway()
  @MessageMapping('message')
  message(client, data) {
    // ...
  }
```

Ahora que hemos definido nuestros métodos, podemos comenzar a implementarlos.

En el método `handleConnection`, usaremos la instancia del servidor `WebSocket` para obtener la lista de clientes conectados. Luego, enviaremos un evento `mensaje` a todos los clientes con el mensaje `¡Bienvenido!`.

```typescript
@WebSocketServer() server;

@WebSocketGateway()
  handleConnection(client) {
    const clients = this.server.clients;
    clients.forEach(c => c.send('message', 'Welcome!'));
  }
```

En el método `handleDisconnect`, usaremos la instancia del servidor `WebSocket` para obtener la lista de clientes conectados. Luego, enviaremos un evento `message` a todos los clientes con el mensaje `¡Adiós!`.

```typescript
@WebSocketServer() server;

@WebSocketGateway()
  handleDisconnect(client) {
    const clients = this.server.clients;
    clients.forEach(c => c.send('message', 'Bye!'));
  }
```

En el método `message`, usaremos la instancia del servidor `WebSocket` para obtener la lista de clientes conectados. Luego, enviaremos un evento `message` a todos los clientes con los datos del mensaje.

```typescript
@WebSocketServer() server;

@WebSocketGateway()
  @MessageMapping('message')
  message(client, data) {
    const clients = this.server.clients;
    clients.forEach(c => c.send('message', data));
  }
```

Ahora que hemos implementado nuestros métodos, nuestro archivo `chat.controller.ts` debería verse así:

```typescript
import { Controller, WebSocketGateway, WsException } from '@nestjs/websockets';

@Controller('/chat')
@WebSocketGateway({ port: 3001 })
export class ChatController {

  @WebSocketServer() server;

  @WebSocketGateway()
  handleConnection(client) {
    const clients = this.server.clients;
    clients.forEach(c => c.send('message', 'Welcome!'));
  }

  @WebSocketGateway()
  handleDisconnect(client) {
    const clients = this.server.clients;
    clients.forEach(c => c.send('message', 'Bye!'));
  }

  @WebSocketGateway()
  @MessageMapping('message')
  message(client, data) {
    const clients = this.server.clients;
    clients.forEach(c => c.send('message', data));
  }

}
```

## Creando el cliente de chat

Ahora que tenemos configurado nuestro servidor de chat, podemos comenzar a construir el cliente de chat.

Primero, necesitamos crear un nuevo archivo llamado `chat.service.ts` en el directorio `src/`. Este archivo contendrá el servicio para nuestro cliente de chat.

En `chat.service.ts`, necesitamos importar el decorador `Inyectable` de `@nestjs/common`. Usaremos esto para definir nuestro servicio como un servicio Nest.js.

```typescript
import { Injectable } from '@nestjs/common';
```

A continuación, usaremos el decorador `@Injectable()` para definir nuestro servicio.

```typescript
@Injectable()
export class ChatService {

}
```

Ahora que hemos definido nuestro servicio, podemos comenzar a agregar métodos.

El primer método que agregaremos es `conectar`. Este método se utilizará para conectarse a nuestro servidor WebSocket. Usaremos la clase `WebSocket` de la biblioteca `ws` para esto.

```typescript
import { Injectable } from '@nestjs/common';
import { WebSocket } from 'ws';

@Injectable()
export class ChatService {

  connect() {
    // ...
  }

}
```

A continuación, agregaremos un método `sendMessage`. Este método se utilizará para enviar un mensaje a nuestro servidor WebSocket. Usaremos la clase `WebSocket` de la biblioteca `ws` para esto.

```typescript
import { Injectable } from '@nestjs/common';
import { WebSocket } from 'ws';

@Injectable()
export class ChatService {

  connect() {
    // ...
  }

  sendMessage(message) {
    // ...
  }

}
```

Finalmente, agregaremos un método `disconnect`. Este método se utilizará para desconectarse de nuestro servidor WebSocket. Usaremos la clase `WebSocket` de la biblioteca `ws` para esto.

```typescript
import { Injectable } from '@nestjs/common';
import { WebSocket } from 'ws';

@Injectable()
export class ChatService {

  connect() {
    // ...
  }

  sendMessage(message) {
    // ...
  }

  disconnect() {
    // ...
  }

}
```

Ahora que hemos definido nuestros métodos, podemos comenzar a implementarlos.

En el método `conectar`, crearemos una nueva instancia `WebSocket` y nos conectaremos a nuestro servidor WebSocket. También configuraremos un detector de eventos para el evento `message`. Este evento se emitirá cuando recibamos un mensaje de nuestro servidor WebSocket.

```typescript
import { Injectable } from '@nestjs/common';
import { WebSocket } from 'ws';

@Injectable()
export class ChatService {

  socket;

  connect() {
    this.socket = new WebSocket('ws://localhost:3001');
    this.socket.on('message', (data) => {
      // ...
    });
  }

  // ...

}
```

En el método `sendMessage`, usaremos la instancia `WebSocket` para enviar un mensaje a nuestro servidor WebSocket.

```typescript
import { Injectable } from '@nestjs/common';
import { WebSocket } from 'ws';

@Injectable()
export class ChatService {

  socket;

  connect() {
    // ...
  }

  sendMessage(message) {
    this.socket.send(message);
  }

  // ...

}
```

En el método `disconnect`, usaremos la instancia `WebSocket` para cerrar la conexión a nuestro servidor WebSocket.

```typescript
import { Injectable } from '@nestjs/common';
import { WebSocket } from 'ws';

@Injectable()
export class ChatService {

  socket;

  connect() {
    // ...
  }

  sendMessage(message) {
    // ...
  }

  disconnect() {
    this.socket.close();
  }

}
```

Ahora que hemos implementado nuestros métodos, nuestro archivo `chat.service.ts` debería verse así:

```typescript
import { Injectable } from '@nestjs/common';
import { WebSocket } from 'ws';

@Injectable()
export class ChatService {

  socket;

  connect() {
    this.socket = new WebSocket('ws://localhost:3001');
    this.socket.on('message', (data) => {
      // ...
    });
  }

  sendMessage(message) {
    this.socket.send(message);
  }

  disconnect() {
    this.socket.close();
  }

}
```

## Creando el componente de chat

Ahora que tenemos nuestro servidor de chat y nuestro cliente configurados, podemos comenzar a construir el componente de chat.

Primero, necesitamos crear un nuevo archivo llamado `chat.component.ts` en el directorio `src/`. Este archivo contendrá el componente para nuestro cliente de chat.

En `chat.component.ts`, necesitamos importar el decorador `Component` de `@nestjs/common`. Usaremos esto para definir nuestro componente como un componente Nest.js.

```typescript
import { Component } from '@nestjs/common';
```

A continuación, usaremos el decorador `@Component()` para definir nuestro componente. Estableceremos la opción `selector` en `chat`. Esta es la etiqueta HTML con la que se representará nuestro componente.

```typescript
@Component({
  selector: 'chat',
})
export class ChatComponent {

}
```

Ahora que hemos definido nuestro componente, podemos comenzar a agregar métodos.

El primer método que agregaremos es `conectar`. Este método se utilizará para conectarse a nuestro servidor WebSocket. Usaremos el servicio `ChatService` para esto.

```typescript
import { Component } from '@nestjs/common';
import { ChatService } from './chat.service';

@Component({
  selector: 'chat',
})
export class ChatComponent {

  constructor(
    private chatService: ChatService,
  ) {}

  connect() {
    // ...
  }

}
```

A continuación, agregaremos un método `sendMessage`. Este método se utilizará para enviar un mensaje a nuestro servidor WebSocket. Usaremos el servicio `ChatService` para esto.

```typescript
import { Component } from '@nestjs/common';
import { ChatService } from './chat.service';

@Component({
  selector: 'chat',
})
export class ChatComponent {

  constructor(
    private chatService: ChatService,
  ) {}

  connect() {
    // ...
  }

  sendMessage(message) {
    // ...
  }

}
```

Finalmente, agregaremos un método `disconnect`. Este método se utilizará para desconectarse de nuestro servidor WebSocket. Usaremos el servicio `ChatService` para esto.

```typescript
import { Component } from '@nestjs/common';
import { ChatService } from './chat.service';

@Component({
  selector: 'chat',
})
export class ChatComponent {

  constructor(
    private chatService: ChatService,
  ) {}

  connect() {
    // ...
  }

  sendMessage(message) {
    // ...
  }

  disconnect() {
    // ...
  }

}
```

Ahora que hemos definido nuestros métodos, podemos comenzar a implementarlos.

En el método `connect`, usaremos `ChatService` para conectarnos a nuestro servidor WebSocket.

```mecanografiado
importar {Componente} de '@nestjs/common';
importar { ChatService } desde './chat.service';

@Componente({