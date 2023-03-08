---
title: 053: Uso de TensorFlow.js con Express.js en Node.js
description: 
published: true
date: 2023-02-02T19:17:22.762Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:17:21.182Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [053: Using TensorFlow.js with Express.js in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/053-using-tensorflow-js-with-express-js-in-node-js)
{.links-list}


# Uso de TensorFlow.js con Express.js en Node.js

TensorFlow.js es una poderosa herramienta para el aprendizaje automático en JavaScript. Se puede usar en Node.js con el marco web Express.js para crear aplicaciones potentes. En esta publicación, le mostraremos cómo comenzar con TensorFlow.js y Express.js.

## Instalando dependencias

Primero, necesitamos instalar las dependencias para nuestro proyecto. Necesitaremos Express.js y TensorFlow.js. Podemos instalarlos con el siguiente comando:

```
npm install express @tensorflow/tfjs
```

## Hola Mundo

Ahora que tenemos nuestras dependencias instaladas, creemos una aplicación simple de "Hola mundo". Crearemos un archivo llamado `index.js` en el directorio raíz de nuestro proyecto y agregaremos el siguiente código:

```javascript
const express = require('express');
const tf = require('@tensorflow/tfjs');

const app = express();

app.get('/', (req, res) => {
  res.send('Hello, world!');
});

app.listen(3000, () => {
  console.log('Example app listening on port 3000!');
});
```

Este código crea un servidor Express.js que escucha en el puerto 3000 y responde "¡Hola, mundo!" cuando se accede a la URL raíz.

## Uso de TensorFlow.js

Ahora que tenemos nuestro servidor Express.js simple en funcionamiento, agreguemos algo de código TensorFlow.js. Comenzaremos agregando una ruta que responda con una cadena generada por un modelo TensorFlow.js.

Primero, necesitamos crear el modelo. Haremos esto en un archivo llamado `model.js`. Crearemos un modelo simple que toma una cadena de entrada y genera una cadena de salida. La cadena de entrada se introducirá en el modelo como un vector codificado one-hot. El modelo generará la cadena de salida utilizando una arquitectura de secuencia a secuencia.

```javascript
const tf = require('@tensorflow/tfjs');

// Create the model
const model = tf.sequential();

// Add an LSTM layer
model.add(tf.layers.lstm({
  units: 8,
  inputShape: [8],
  returnSequences: true
}));

// Add a second LSTM layer
model.add(tf.layers.lstm({
  units: 8,
  returnSequences: true
}));

// Add a dense layer
model.add(tf.layers.dense({
  units: 8,
  activation: 'softmax'
}));

// Compile the model
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'rmsprop'
});

// Export the model
module.exports = model;
```

Este código crea un modelo simple basado en LSTM. El modelo toma una cadena de entrada de 8 caracteres y genera una cadena de 8 caracteres.

Ahora que tenemos nuestro modelo, podemos agregar una ruta que lo use. Agregaremos la siguiente ruta a nuestro archivo `index.js`:

```javascript
app.get('/generate', (req, res) => {
  // Load the model
  const model = require('./model');

  // Generate a string
  const string = model.predict(tf.oneHot('Hello, world!'.split(''), 8));

  // Send the string to the client
  res.send(string);
});
```

Esta ruta carga el modelo que creamos en `model.js` y lo usa para generar una cadena. A continuación, la cadena generada se envía al cliente.

## Conclusión

En esta publicación, le mostramos cómo comenzar con TensorFlow.js y Express.js. Hemos creado una aplicación simple "Hola mundo" y una ruta que usa un modelo TensorFlow.js para generar una cadena.

## Recursos

- [TensorFlow.js](https://js.tensorflow.org/)
- [Express.js](https://expressjs.com/)
- [Node.js](https://nodejs.org/)