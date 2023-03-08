---
title: Trabajar con Node.js y WebSockets para comunicación en tiempo real
description: 
published: true
date: 2023-02-17T01:55:39.089Z
tags: 
editor: markdown
dateCreated: 2023-02-17T01:55:30.795Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Working with Node.js and WebSockets for Real-Time Communication***English** document is available*](/en/Knowledge-base/Nodejs/working-with-node-js-and-websockets-for-real-time-communication)
{.links-list}


      Blog de aprendizaje sobre desarrollo de TI

# Trabajar con Node.js y WebSockets para comunicación en tiempo real

Node.js es un entorno de tiempo de ejecución de Javascript que le permite ejecutar código Javascript fuera del navegador. Es versátil y se puede utilizar para desarrollar aplicaciones del lado del servidor, herramientas de línea de comandos e incluso aplicaciones de escritorio.

WebSockets es una tecnología web que permite la comunicación bidireccional de dúplex completo entre un cliente y un servidor. Está diseñado para la comunicación en tiempo real y se usa a menudo en aplicaciones como aplicaciones de chat, aplicaciones de edición colaborativa y aplicaciones de juegos.

En este artículo, exploraremos cómo usar Node.js y WebSockets para la comunicación en tiempo real. Discutiremos cómo configurar un servidor Node.js que pueda manejar solicitudes de WebSocket y también crearemos una aplicación de chat simple que usa WebSockets para la comunicación en tiempo real.

## Configuración de un servidor Node.js

Usaremos el paquete npm [ws](https://www.npmjs.com/package/ws) para trabajar con WebSockets en Node.js.

Primero, necesitamos instalar el paquete `ws`:

```
npm install ws
```

A continuación, debemos crear un archivo llamado `server.js` y agregar el siguiente código:

```javascript
const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
  ws.on('message', (message) => {
    console.log(`Received message => ${message}`);
  });

  ws.send('Hello!');
});
```

En el código anterior, usamos el paquete `ws` para crear un servidor WebSocket en el puerto 8080. También manejamos el evento `conexión`, que se activa cuando un cliente se conecta al servidor. Cuando se establece una conexión, estamos configurando un controlador de eventos para el evento "mensaje", que se activa cuando se recibe un mensaje del cliente. Finalmente, estamos enviando un mensaje al cliente cuando se establece la conexión.

Para ejecutar el servidor, podemos usar el siguiente comando:

```
node server.js
```

## Crear una aplicación de chat

Ahora que tenemos un servidor Node.js que puede manejar solicitudes de WebSocket, construyamos una aplicación de chat simple que use WebSockets para la comunicación en tiempo real.

Primero, necesitamos crear un archivo llamado `client.html` y agregar el siguiente código:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>WebSocket Chat</title>
</head>
<body>
  <h1>WebSocket Chat</h1>
  <form id="form">
    <label for="message">Message:</label>
    <input type="text" id="message" />
    <input type="submit" value="Send" />
  </form>
  <ul id="messages"></ul>
  <script>
    const form = document.getElementById('form');
    const messages = document.getElementById('messages');
    const message = document.getElementById('message');

    const ws = new WebSocket('ws://localhost:8080');

    ws.onopen = () => {
      console.log('Connected');
    };

    ws.onmessage = (event) => {
      const li = document.createElement('li');
      li.innerText = event.data;
      messages.appendChild(li);
    };

    ws.onerror = (error) => {
      console.log(error);
    };

    ws.onclose = () => {
      console.log('Disconnected');
    };

    form.addEventListener('submit', (event) => {
      event.preventDefault();

      ws.send(message.value);
      message.value = '';
    });
  </script>
</body>
</html>
```

En el código anterior, usamos HTML y Javascript para crear una aplicación de chat simple. Usamos la API `WebSocket` para establecer una conexión con el servidor y usamos el evento `message` para recibir mensajes del servidor y mostrarlos en el navegador. También estamos usando el método `send` para enviar mensajes al servidor.

## Conclusión

En este artículo, exploramos cómo usar Node.js y WebSockets para la comunicación en tiempo real. Hemos configurado un servidor Node.js que puede manejar solicitudes de WebSocket y también hemos creado una aplicación de chat simple que usa WebSockets para la comunicación en tiempo real.