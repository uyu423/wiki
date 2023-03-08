---
title: 063: Análisis de sentimiento en tiempo real con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T21:43:47.192Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:43:45.470Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [063: Real-Time Sentiment Analysis with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/063-real-time-sentiment-analysis-with-tensorflow-js-and-node-js)
{.links-list}


# Análisis de sentimiento en tiempo real con TensorFlow.js y Node.js

En esta publicación, veremos cómo crear una aplicación de análisis de sentimientos en tiempo real utilizando TensorFlow.js y Node.js.

## ¿Qué es el análisis de sentimiento?

El análisis de sentimiento es el proceso de extraer información basada en opiniones del texto. Esto puede ser útil para una variedad de aplicaciones, como comprender los comentarios de los clientes o medir la reacción del público a un evento noticioso.

## Construyendo la aplicación

Usaremos las siguientes herramientas para construir nuestra aplicación:

- [TensorFlow.js](https://js.tensorflow.org/)
- [Node.js](https://nodejs.org/en/)
- [Socket.io](https://socket.io/)

### Configuración del entorno

Primero, necesitamos configurar nuestro entorno de desarrollo. Usaremos [Node.js](https://nodejs.org/en/) para este proyecto, así que asegúrese de tenerlo instalado.

Una vez que se instala Node.js, podemos crear un nuevo directorio de proyecto e inicializarlo con [npm](https://www.npmjs.com/):

```
mkdir sentiment-analysis
cd sentiment-analysis
npm init -y
```

Esto creará un nuevo directorio llamado `sentiment-analysis` y lo inicializará con un archivo `package.json`.

A continuación, necesitamos instalar las dependencias para nuestro proyecto. Usaremos [TensorFlow.js](https://js.tensorflow.org/) y [Socket.io](https://socket.io/):

```
npm install @tensorflow/tfjs socket.io
```

Esto instalará los paquetes `@tensorflow/tfjs` y `socket.io` en nuestro proyecto.

### Creando el modelo

Ahora que tenemos nuestro entorno configurado, podemos comenzar a construir el modelo de análisis de sentimiento. Usaremos un [modelo preentrenado](https://tfhub.dev/google/tfjs-models/tfjs-sentiment/2) de TensorFlow Hub.

Para usar este modelo, primero debemos cargarlo en TensorFlow.js:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
const model = await tf.loadModel('https://tfhub.dev/google/tfjs-models/tfjs-sentiment/2/default/1');
```

A continuación, necesitamos crear una función que tome una cadena de texto y devuelva una puntuación entre 0 y 1, donde 0 es negativo y 1 es positivo. Podemos hacer esto alimentando el texto en el modelo y tomando el argmax de la salida:

```javascript
function getSentiment(text) {
  // Convert the text to a tensor.
  const input = tf.tensor1d([text]);

  // Get the model's predictions.
  const predictions = model.predict(input);

  // Get the highest scoring prediction.
  const argMax = predictions.argMax(-1);

  // We only need the highest scoring prediction's index.
  const index = argMax.dataSync()[0];

  // Get the predicted label.
  const label = (index === 0) ? 'negative' : 'positive';

  // Get the predicted probability.
  const probability = predictions.dataSync()[index];

  return { label, probability };
}
```

Ahora que tenemos nuestro modelo configurado, podemos pasar a crear el servidor.

### Creando el servidor

Usaremos [Node.js](https://nodejs.org/) y [Socket.io](https://socket.io/) para crear el servidor para nuestra aplicación.

Primero, necesitamos requerir las dependencias:

```javascript
const tf = require('@tensorflow/tfjs');
const io = require('socket.io')();
```

A continuación, necesitamos crear una función que maneje el texto entrante desde un socket:

```javascript
function handleText(socket, text) {
  // Get the sentiment of the text.
  const { label, probability } = getSentiment(text);

  // Emit the results to the socket.
  socket.emit('results', { label, probability });
}
```

Finalmente, necesitamos iniciar el servidor y escuchar las conexiones entrantes:

```javascript
// Start the server.
io.listen(3000);

// Listen for incoming connections.
io.on('connection', (socket) => {
  // Listen for text from the socket.
  socket.on('text', (text) => handleText(socket, text));
});
```

Ahora que tenemos nuestro servidor configurado, podemos pasar a crear el cliente.

### Creando el Cliente

Usaremos [Socket.io](https://socket.io/) para crear el cliente para nuestra aplicación.

Primero, necesitamos cargar la biblioteca del cliente Socket.io:

```html
<script src="/socket.io/socket.io.js"></script>
```

A continuación, necesitamos crear un socket y conectarlo al servidor:

```javascript
// Connect to the server.
const socket = io.connect('http://localhost:3000');
```

Ahora que tenemos nuestro socket configurado, podemos comenzar a enviar texto al servidor. Haremos esto escuchando la entrada del usuario y emitiéndola al socket:

```javascript
// Listen for user input.
document.querySelector('#text-input').addEventListener('input', (event) => {
  // Get the input text.
  const text = event.target.value;

  // Emit the text to the socket.
  socket.emit('text', text);
});
```

Finalmente, necesitamos escuchar los resultados del servidor y mostrárselos al usuario:

```javascript
// Listen for results from the server.
socket.on('results', (results) => {
  // Get the results element.
  const element = document.querySelector('#results');

  // Clear the element.
  element.innerHTML = '';

  // Create a new paragraph for each result.
  results.forEach((result) => {
    const { label, probability } = result;
    const paragraph = document.createElement('p');
    paragraph.innerHTML = `${label}: ${probability}`;
    element.appendChild(paragraph);
  });
});
```

Ahora que tenemos nuestro cliente configurado, podemos probar la aplicación.

## Prueba de la aplicación

Para probar la aplicación, abra `index.html` en un navegador. Luego, ingrese algo de texto en la entrada de texto y presione enter. Debería ver los resultados aparecer en el elemento de resultados.

## Conclusión

En esta publicación, hemos visto cómo crear una aplicación de análisis de sentimientos en tiempo real utilizando TensorFlow.js y Node.js. También vimos cómo usar un modelo previamente entrenado de TensorFlow Hub.

Si está interesado en obtener más información sobre el análisis de sentimientos, aquí hay algunos recursos para leer más:

- [Análisis de sentimiento con TensorFlow.js](https://medium.com/tensorflow/sentiment-analysis-with-tensorflow-js-bccd4d9d4a30)
- [Análisis de sentimiento en tiempo real con TensorFlow.js](https://www.tensorflow.org/js/tutorials/sentiment/index)