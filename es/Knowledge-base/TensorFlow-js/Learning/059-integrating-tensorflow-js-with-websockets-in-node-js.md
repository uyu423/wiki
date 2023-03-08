---
title: 059: Integrando TensorFlow.js con WebSockets en Node.js
description: 
published: true
date: 2023-02-02T20:44:16.079Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:44:11.381Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [059: Integrating TensorFlow.js with WebSockets in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/059-integrating-tensorflow-js-with-websockets-in-node-js)
{.links-list}


# 059: Integrando TensorFlow.js con WebSockets en Node.js

TensorFlow.js es una poderosa herramienta para entrenar e implementar modelos de aprendizaje automático en el navegador. Sin embargo, los modelos de entrenamiento en el navegador pueden ser lentos e ineficientes debido a los recursos limitados disponibles.

Una forma de acelerar el entrenamiento es usar WebSockets para enviar datos a un servidor para el entrenamiento. De esta forma, el servidor puede usar sus recursos para entrenar el modelo más rápidamente.

En esta publicación, le mostraremos cómo configurar un servidor Node.js y usar WebSockets para enviar datos al servidor para entrenar un modelo TensorFlow.js.

## Requisitos previos

Antes de comenzar, hay algunas cosas que necesitará:

- Un editor de texto. Recomendamos [Visual Studio Code](https://code.visualstudio.com/).
- [Node.js](https://nodejs.org/en/) instalado en su computadora.
- [NPM](https://www.npmjs.com/) (que viene con Node.js) instalado en su computadora.
- [TensorFlow.js](https://js.tensorflow.org/) instalado en su computadora.

## Configuración del servidor Node.js

Primero, necesitaremos configurar un servidor Node.js. Usaremos el marco web [ Express ](https://expressjs.com/) para facilitar las cosas.

Cree un nuevo archivo llamado `server.js` y pegue el siguiente código en él:

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => res.send('Hello World!'));

app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

Este código crea un servidor Express básico que escucha en el puerto 3000.

A continuación, necesitaremos instalar las dependencias para nuestro servidor. En su terminal, navegue hasta el directorio donde se encuentra `server.js` y ejecute el siguiente comando:

```
npm install express --save
```

Esto instalará el marco Express y lo guardará como una dependencia en nuestro archivo `package.json`.

Ahora que nuestro servidor está configurado, podemos iniciarlo ejecutando el siguiente comando en nuestra terminal:

```
node server.js
```

Debería ver el siguiente resultado:

```
Example app listening on port 3000!
```

## Envío de datos al servidor

Ahora que nuestro servidor está en funcionamiento, podemos comenzar a enviarle datos. Usaremos [ WebSockets ](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) para enviar datos desde el navegador al servidor.

Primero, necesitaremos instalar la biblioteca WebSocket [ ws ](https://github.com/websockets/ws). En su terminal, navegue hasta el directorio donde se encuentra `server.js` y ejecute el siguiente comando:

```
npm install ws --save
```

Esto instalará la biblioteca `ws` y la guardará como una dependencia en nuestro archivo `package.json`.

A continuación, necesitaremos modificar nuestro archivo `server.js` para usar la biblioteca `ws`. Reemplace el contenido de `server.js` con el siguiente código:

```javascript
const express = require('express');
const app = express();
const port = 3000;
const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
  ws.on('message', (message) => {
    console.log(`Received message => ${message}`);
  });
  ws.send('Hello!');
});

app.get('/', (req, res) => res.send('Hello World!'));

app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

Este código crea un nuevo servidor WebSocket que escucha en el puerto 8080. Cuando se establece una conexión, el servidor registrará todos los mensajes que reciba.

Ahora que nuestro servidor está configurado para recibir datos, podemos escribir un código para enviarle datos. Cree un nuevo archivo llamado `client.html` y pegue el siguiente código en él:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>WebSocket Client</title>
  </head>
  <body>
    <h1>WebSocket Client</h1>
    <script>
      const ws = new WebSocket('ws://localhost:8080');
      ws.onopen = () => {
        // Send a message when the WebSocket is opened
        ws.send('Hello!');
      };
      ws.onmessage = (event) => {
        // Log the message when a message is received
        console.log(event.data);
      };
    </script>
  </body>
</html>
```

Este código crea una nueva conexión WebSocket a nuestro servidor y envía un mensaje cuando se abre la conexión. También registra los mensajes que recibe.

Abra `client.html` en su navegador y debería ver el siguiente resultado en la consola:

```
Hello!
```

## Envío de datos al servidor para entrenamiento

Ahora que podemos enviar datos a nuestro servidor, podemos usarlos para entrenar un modelo TensorFlow.js. Usaremos el [ Iris Dataset ](https://en.wikipedia.org/wiki/Iris_flower_data_set) para entrenar un modelo de clasificación simple.

Primero, necesitaremos modificar nuestro archivo `server.js` para incluir la biblioteca TensorFlow.js. Reemplace el contenido de `server.js` con el siguiente código:

```javascript
const express = require('express');
const app = express();
const port = 3000;
const WebSocket = require('ws');
const tf = require('@tensorflow/tfjs');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
  ws.on('message', (message) => {
    console.log(`Received message => ${message}`);
  });
  ws.send('Hello!');
});

app.get('/', (req, res) => res.send('Hello World!'));

app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

Este código incluye la biblioteca TensorFlow.js y crea un modelo de clasificación básico.

A continuación, necesitaremos modificar nuestro archivo `client.html` para enviar datos al servidor para entrenamiento. Reemplace el contenido de `client.html` con el siguiente código:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>WebSocket Client</title>
  </head>
  <body>
    <h1>WebSocket Client</h1>
    <script>
      const ws = new WebSocket('ws://localhost:8080');
      ws.onopen = () => {
        // Send data to the server when the WebSocket is opened
        ws.send('1,2,3,4');
      };
      ws.onmessage = (event) => {
        // Log the message when a message is received
        console.log(event.data);
      };
    </script>
  </body>
</html>
```

Este código envía datos al servidor cuando se abre la conexión. También registra los mensajes que recibe.

Abra `client.html` en su navegador y debería ver el siguiente resultado en la consola:

```
Received message => 1,2,3,4
```

## Conclusión

En esta publicación, le mostramos cómo configurar un servidor Node.js y usar WebSockets para enviar datos al servidor para entrenar un modelo TensorFlow.js.

Esta es una forma poderosa de entrenar modelos de aprendizaje automático en el navegador. Al usar los recursos de un servidor, podemos entrenar modelos de manera más rápida y eficiente.