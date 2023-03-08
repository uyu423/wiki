---
title: 060: Uso de TensorFlow.js con WebRTC en Node.js
description: 
published: true
date: 2023-02-02T21:05:32.406Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:05:30.664Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [060: Using TensorFlow.js with WebRTC in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/060-using-tensorflow-js-with-webrtc-in-node-js)
{.links-list}


# Uso de TensorFlow.js con WebRTC en Node.js

En esta publicación, le mostraremos cómo usar TensorFlow.js con WebRTC en Node.js. Veremos cómo configurar su entorno de desarrollo, cómo usar TensorFlow.js con WebRTC y cómo implementar su aplicación.

## Configuración de su entorno de desarrollo

Antes de comenzar, debemos configurar nuestro entorno de desarrollo. Tendremos que instalar Node.js y la biblioteca TensorFlow.js Node.js.

### Instalación de Node.js

Primero, necesitamos instalar Node.js. Puede descargar el instalador de Node.js desde el [sitio web de Node.js] (https://nodejs.org/en/). Ejecute el instalador y siga las indicaciones para instalar Node.js.

Una vez que Node.js está instalado, puede verificar que funciona abriendo una terminal y ejecutando el siguiente comando:

```
node -v
```

Debería ver el número de versión de Node.js impreso en el terminal.

### Instalación de la biblioteca TensorFlow.js Node.js

Ahora que tenemos Node.js instalado, podemos instalar la biblioteca TensorFlow.js Node.js. Podemos hacer esto con el administrador de paquetes de Node.js, npm.

Primero, necesitamos crear un archivo package.json. Este archivo contendrá información sobre nuestro proyecto, incluidas las dependencias que queremos instalar. Podemos crear un archivo package.json con el siguiente comando:

```
npm init
```

Esto le pedirá alguna información sobre su proyecto. Puede aceptar los valores predeterminados presionando enter.

A continuación, debemos instalar la biblioteca TensorFlow.js Node.js. Esto lo podemos hacer con el siguiente comando:

```
npm install @tensorflow/tfjs-node
```

Esto instalará la biblioteca TensorFlow.js Node.js y cualquier otra dependencia que necesite.

## Uso de TensorFlow.js con WebRTC

Ahora que tenemos configurado nuestro entorno de desarrollo, podemos comenzar a usar TensorFlow.js con WebRTC.

WebRTC es una tecnología que permite la comunicación en tiempo real entre navegadores. TensorFlow.js es una biblioteca de JavaScript para el aprendizaje automático. Juntas, estas dos tecnologías se pueden usar para crear aplicaciones que pueden realizar aprendizaje automático en tiempo real.

### Empezando

Para comenzar, necesitamos crear un archivo HTML. Podemos hacer esto con un editor de texto como [VS Code](https://code.visualstudio.com/).

En este archivo, debemos incluir la biblioteca TensorFlow.js. Podemos hacer esto agregando la siguiente etiqueta de script al encabezado de nuestro archivo HTML:

```html
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.3/dist/tf.min.js"></script>
```

También necesitamos incluir el adaptador WebRTC. Esta es una biblioteca de JavaScript que proporciona compatibilidad entre las implementaciones de WebRTC de diferentes navegadores. Podemos incluir el adaptador WebRTC con la siguiente etiqueta de script:

```html
<script src="https://webrtc.github.io/adapter/adapter-latest.js"></script>
```

También debemos incluir la biblioteca TensorFlow.js Node.js. Podemos hacer esto con una etiqueta de script:

```html
<script src="./node_modules/@tensorflow/tfjs-node/dist/tfjs-node.js"></script>
```

### Crear una conexión WebRTC

Ahora que tenemos las bibliotecas TensorFlow.js y WebRTC incluidas, podemos comenzar a usarlas.

Primero, necesitamos crear una conexión WebRTC. Esto lo podemos hacer con el siguiente código:

```javascript
// Get the user's media stream
navigator.mediaDevices.getUserMedia({ video: true, audio: true })
  .then(function (mediaStream) {
    // Create a WebRTC connection
    const peerConnection = new RTCPeerConnection();

    // Add the media stream to the connection
    peerConnection.addStream(mediaStream);

    // Create an offer
    peerConnection.createOffer()
      .then(function (offer) {
        // Set the offer as the local description
        peerConnection.setLocalDescription(offer);

        // Send the offer to the remote peer
        // ...
      });
  });
```

En este código, primero obtenemos el flujo de medios del usuario. Esto nos dará acceso a la cámara web y al micrófono del usuario. Luego creamos una conexión WebRTC. Esta conexión se utilizará para conectar el navegador del usuario al par remoto.

A continuación, agregamos el flujo de medios del usuario a la conexión. Esto permitirá que el compañero remoto vea y escuche al usuario.

Luego, creamos una oferta. Esta es una descripción del flujo de medios del usuario y las capacidades del navegador del usuario. Establecemos esta oferta como la descripción local. Esto será utilizado por el par remoto para conectarse con el usuario.

Finalmente, enviamos la oferta al par remoto. El interlocutor remoto utilizará esta oferta para conectarse con el usuario.

### Recibir una oferta

Ahora que hemos visto cómo crear una oferta, echemos un vistazo a cómo recibir una oferta.

Cuando el par remoto nos envía una oferta, debemos configurarla como la descripción remota. Esto lo podemos hacer con el siguiente código:

```javascript
// Get the user's media stream
navigator.mediaDevices.getUserMedia({ video: true, audio: true })
  .then(function (mediaStream) {
    // Create a WebRTC connection
    const peerConnection = new RTCPeerConnection();

    // Add the media stream to the connection
    peerConnection.addStream(mediaStream);

    // When we receive an offer
    peerConnection.on('offer', function (offer) {
      // Set the offer as the remote description
      peerConnection.setRemoteDescription(offer);

      // Create an answer
      peerConnection.createAnswer()
        .then(function (answer) {
          // Set the answer as the local description
          peerConnection.setLocalDescription(answer);

          // Send the answer to the remote peer
          // ...
        });
    });
  });
```

En este código, primero obtenemos el flujo de medios del usuario. Esto nos dará acceso a la cámara web y al micrófono del usuario. Luego creamos una conexión WebRTC. Esta conexión se utilizará para conectar el navegador del usuario al par remoto.

A continuación, agregamos el flujo de medios del usuario a la conexión. Esto permitirá que el compañero remoto vea y escuche al usuario.

Luego, configuramos un detector de eventos para cuando recibamos una oferta. Cuando recibimos una oferta, la configuramos como descripción remota.

Finalmente, creamos una respuesta. Esta es una descripción del flujo de medios del usuario y las capacidades del navegador del usuario. Establecemos esta respuesta como la descripción local. Esto será utilizado por el par remoto para conectarse con el usuario.

### Enviando una respuesta

Ahora que hemos visto cómo crear una respuesta, echemos un vistazo a cómo enviar una respuesta.

Cuando el par remoto nos envía una respuesta, debemos configurarlo como la descripción remota. Esto lo podemos hacer con el siguiente código:

```javascript
// Get the user's media stream
navigator.mediaDevices.getUserMedia({ video: true, audio: true })
  .then(function (mediaStream) {
    // Create a WebRTC connection
    const peerConnection = new RTCPeerConnection();

    // Add the media stream to the connection
    peerConnection.addStream(mediaStream);

    // When we receive an answer
    peerConnection.on('answer', function (answer) {
      // Set the answer as the remote description
      peerConnection.setRemoteDescription(answer);
    });

    // Create an offer
    peerConnection.createOffer()
      .then(function (offer) {
        // Set the offer as the local description
        peerConnection.setLocalDescription(offer);

        // Send the offer to the remote peer
        // ...
      });
  });
```

En este código, primero obtenemos el flujo de medios del usuario. Esto nos dará acceso a la cámara web y al micrófono del usuario. Luego creamos una conexión WebRTC. Esta conexión se utilizará para conectar el navegador del usuario al par remoto.

A continuación, agregamos el flujo de medios del usuario a la conexión. Esto permitirá que el compañero remoto vea y escuche al usuario.

Luego, configuramos un detector de eventos para cuando recibamos una respuesta. Cuando recibimos una respuesta, la configuramos como la descripción remota.

Finalmente, creamos una oferta. Esta es una descripción del flujo de medios del usuario y las capacidades del navegador del usuario. Establecemos esta oferta como la descripción local. Esto será utilizado por el par remoto para conectarse con el usuario.

## Desplegando su aplicación

Ahora que hemos visto cómo usar TensorFlow.js con WebRTC, echemos un vistazo a cómo implementar nuestra aplicación.

Necesitaremos usar un servidor web para servir nuestro archivo HTML. Podemos hacer esto con el [módulo HTTP de Node.js](https://nodejs.org/api/http.html).

Primero, necesitamos crear un archivo llamado `server.js`. En este archivo, necesitaremos el módulo `http` y crearemos un servidor HTTP. Esto lo podemos hacer con el siguiente código:

```javascript
const http = require('http');

const server = http.createServer(function (request, response) {
  // Serve the HTML file
  // ...
});

server.listen(8080);
```

En este código, requerimos el módulo `http`. Este módulo nos dará acceso al servidor y cliente HTTP. Luego creamos un servidor HTTP. Este servidor se utilizará para servir nuestro archivo HTML.

A continuación, debemos decirle al servidor qué archivo servir. Podemos hacer esto agregando el siguiente código a la devolución de llamada `createServer`:

```javascript
const fs = require('fs');

const index = fs.readFileSync('./index.html');

response.writeHead(200, { 'Content-Type': 'text/html' });
response.end(index);
```

En este código, requerimos el módulo `fs`. Este módulo nos dará acceso al sistema de archivos. Luego leemos el contenido de nuestro archivo HTML en una variable.

Finalmente, escribimos el contenido del archivo HTML en la respuesta. También configuramos el encabezado `Content-Type` en `text/html`. Esto le dirá al navegador que el archivo es un archivo HTML.

## Conclusión

En esta publicación, le mostramos cómo usar TensorFlow.js con WebRTC en Node.js. Hemos repasado cómo configurar su entorno de desarrollo, cómo usar TensorFlow.js con WebRTC y cómo implementar su aplicación.