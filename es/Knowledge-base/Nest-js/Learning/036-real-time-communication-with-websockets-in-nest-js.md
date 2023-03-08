---
title: 036: Comunicación en tiempo real con WebSockets en Nest.js
description: 
published: true
date: 2023-02-08T11:56:10.473Z
tags: 
editor: markdown
dateCreated: 2023-02-08T11:56:08.843Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [036: Real-time communication with WebSockets in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/036-real-time-communication-with-websockets-in-nest-js)
{.links-list}


# Comunicación en tiempo real con WebSockets en Nest.js

WebSocket es un protocolo de comunicaciones informáticas que proporciona canales de comunicación full-duplex a través de una única conexión TCP. El protocolo WebSocket se estandarizó en 2011, y el W3C está estandarizando la API de WebSocket en Web IDL.

WebSocket está diseñado para implementarse en navegadores web y servidores web, pero puede ser utilizado por cualquier aplicación cliente o servidor. El protocolo WebSocket hace posible una mayor interacción entre un navegador y un sitio web, facilitando el contenido en vivo y la creación de juegos en tiempo real. Esto es posible al proporcionar una forma estandarizada para que el servidor envíe contenido al navegador sin que el cliente lo solicite, y permite que los mensajes se transmitan de un lado a otro mientras se mantiene abierta la conexión. De esta forma, puede tener lugar una conversación continua bidireccional (bidireccional) entre el navegador y el servidor.

## ¿Cómo funciona WebSocket?

WebSocket utiliza una conexión de socket TCP de larga duración (bidireccional) entre el cliente y el servidor. Una vez establecida la conexión, permanece abierta hasta que el cliente o servidor decide cerrarla. Esto es diferente de la típica conexión HTTP, que normalmente se cierra después de cada ciclo de solicitud/respuesta.

La conexión WebSocket se inicia mediante una solicitud HTTP con un encabezado de actualización. El cliente envía una solicitud al servidor, solicitando actualizar la conexión a un WebSocket desde una conexión HTTP normal. Si el servidor acepta actualizar la conexión, responde con una respuesta HTTP con un encabezado de actualización. Una vez que se actualiza la conexión, el cliente y el servidor pueden enviarse datos en ambas direcciones.

Los datos que se intercambian entre el cliente y el servidor se encuentran en forma de mensajes. Cada mensaje tiene un tipo y una carga útil de datos. El tipo de mensaje determina cómo se interpretarán los datos de la carga útil.

Hay cuatro tipos de mensajes:

- **Texto**: la carga útil del mensaje se interpreta como una cadena codificada en UTF-8.
- **Binario**: la carga útil del mensaje se interpreta como datos binarios sin procesar.
- **Cerrar**: La conexión está cerrada.
- **Ping**: El cliente le pregunta al servidor si todavía está allí. El servidor responde con un mensaje Pong.

## ¿Por qué usar WebSocket?

HTTP es un gran protocolo, pero tiene algunas limitaciones. Una de las principales limitaciones es que es un protocolo de solicitud/respuesta. Esto significa que el cliente debe enviar una solicitud al servidor y luego esperar una respuesta. El servidor no puede enviar datos al cliente sin que el cliente lo solicite primero.

Esta limitación se puede solucionar mediante el uso de sondeos. El cliente puede enviar una solicitud al servidor preguntando si hay nuevos datos, y el servidor puede responder con los nuevos datos si los hay. Esto funciona, pero tiene algunos inconvenientes.

- Es ineficiente, ya que el cliente tiene que seguir enviando solicitudes aunque no haya nuevos datos.
- Agrega latencia, ya que el cliente tiene que esperar una respuesta antes de poder enviar otra solicitud.
- No es en tiempo real, ya que hay un retraso entre que el servidor genera nuevos datos y el cliente los recibe.

WebSocket elimina estas limitaciones al proporcionar un canal de comunicaciones de dúplex completo a través de una única conexión TCP. Esto significa que el cliente y el servidor pueden enviarse datos al mismo tiempo, sin tener que esperar una respuesta.

## Primeros pasos con WebSocket en Nest.js

Nest.js es un marco para crear aplicaciones del lado del servidor. Está construido sobre Node.js y usa TypeScript.

Nest.js proporciona una forma de usar WebSocket con el módulo @nestjs/websockets.

Para usar @nestjs/websockets, debe instalarlo desde npm:

```
npm install @nestjs/websockets
```

Una vez que se instala @nestjs/websockets, puede crear un servidor Nest.js como este:

```typescript
import { NestFactory } from '@nestjs/core';
import { WsAdapter } from '@nestjs/platform-ws';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.useWebSocketAdapter(new WsAdapter(app));
  await app.listen(3000);
}
bootstrap();
```

En el ejemplo anterior, importamos el WsAdapter de @nestjs/platform-ws y lo pasamos al método useWebSocketAdapter(). Esto hará que el servidor Nest.js utilice el protocolo WebSocket en lugar de HTTP.

Luego podemos crear un controlador para manejar los mensajes de WebSocket:

```typescript
import {
  Controller,
  OnGatewayConnection,
  OnGatewayDisconnect,
  SubscribeMessage,
  WebSocketGateway,
  WsResponse,
} from '@nestjs/websockets';
import { Observable, of } from 'rxjs';
import { map } from 'rxjs/operators';

@Controller()
@WebSocketGateway()
export class AppController {
  @SubscribeMessage('events')
  findAll(client, data): Observable<WsResponse<number[]>> {
    return of([1, 2, 3]).pipe(map(item => ({ event: 'events', data: item })));
  }

  @SubscribeMessage('identity')
  identity(client, data: number): Observable<number> {
    return of(data);
  }

  @OnGatewayConnection()
  handleConnection(client) {
    console.log('Client connected');
  }

  @OnGatewayDisconnect()
  handleDisconnect(client) {
    console.log('Client disconnected');
  }
}
```

En el ejemplo anterior, hemos creado un controlador con dos métodos. El primer método, findAll(), está suscrito al tema 'eventos'. Esto significa que se llamará cada vez que un cliente envíe un mensaje al tema 'eventos'. El método findAll() devuelve un Observable que emitirá un mensaje al cliente.

El segundo método, identidad(), está suscrito al tema 'identidad'. Esto significa que se llamará cada vez que un cliente envíe un mensaje al tema 'identidad'. El método Identity() devuelve un Observable que emitirá los datos que envió el cliente.

También hemos definido dos métodos, handleConnection() y handleDisconnect(), que se llamarán cuando un cliente se conecte y se desconecte del servidor WebSocket.

## Enviar y recibir mensajes

Una vez que el servidor Nest.js se está ejecutando, podemos enviarle mensajes mediante un cliente WebSocket. Hay muchos clientes WebSocket disponibles, pero para este ejemplo usaremos el paquete ws NPM.

Para instalar el paquete ws, ejecute el siguiente comando:

```
npm install ws
```

Una vez instalado el paquete ws, podemos crear un cliente como este:

```javascript
const WebSocket = require('ws');

const ws = new WebSocket('ws://localhost:3000');

ws.on('open', function open() {
  console.log('connected');
  ws.send(JSON.stringify({ event: 'events', data: 'hello world' }));
});

ws.on('message', function incoming(data) {
  console.log(data);
});
```

En el ejemplo anterior, hemos creado un cliente WebSocket que se conecta al servidor Nest.js. Hemos definido dos controladores de eventos, uno para cuando se abre la conexión y otro para cuando se recibe un mensaje.

En el controlador de eventos abierto, estamos enviando un mensaje al servidor. El mensaje tiene un tipo de 'eventos' y una carga útil de 'hola mundo'.

En el controlador de eventos del mensaje, estamos imprimiendo los datos que se recibieron del servidor.

## Conclusión

En este artículo, hemos visto cómo usar WebSocket para crear aplicaciones en tiempo real con Nest.js. Hemos visto cómo crear un servidor Nest.js y cómo enviar y recibir mensajes con un cliente WebSocket.