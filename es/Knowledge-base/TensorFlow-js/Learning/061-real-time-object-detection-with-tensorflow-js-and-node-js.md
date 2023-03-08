---
title: 061: Detección de objetos en tiempo real con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T21:17:45.222Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:17:43.579Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [061: Real-Time Object Detection with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/061-real-time-object-detection-with-tensorflow-js-and-node-js)
{.links-list}


# 061: Detección de objetos en tiempo real con TensorFlow.js y Node.js

En esta publicación, aprenderemos a usar TensorFlow.js y Node.js para realizar la detección de objetos en tiempo real.

## ¿Qué es TensorFlow.js?

TensorFlow.js es una biblioteca de código abierto para el aprendizaje automático en JavaScript. Le permite entrenar y ejecutar modelos de aprendizaje automático en el navegador o en un entorno Node.js.

## ¿Qué es Node.js?

Node.js es un entorno de tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript fuera del navegador.

## ¿Cómo podemos usar TensorFlow.js y Node.js para realizar la detección de objetos en tiempo real?

Podemos usar TensorFlow.js y Node.js para realizar la detección de objetos en tiempo real al:

1. Entrenamiento de un modelo de aprendizaje automático para detectar objetos en imágenes.
2. Implementación del modelo en un servidor Node.js.
3. Usar el servidor para procesar imágenes entrantes y detectar objetos en tiempo real.

## 1. Entrenamiento de un modelo de aprendizaje automático para detectar objetos en imágenes

Comenzaremos entrenando un modelo de aprendizaje automático para detectar objetos en imágenes. Para ello, utilizaremos el modelo MobileNet. MobileNet es un modelo preentrenado que ha sido entrenado en un gran conjunto de datos de imágenes.

Podemos utilizar MobileNet para realizar la detección de objetos mediante:

1. Cargando el modelo de MobileNet.
2. Pasar una imagen al modelo.
3. Obtener las predicciones del modelo.

Veamos cómo podemos hacer esto en código:

```javascript
// Load the MobileNet model.
const model = await mobilenet.load();

// Classify the image.
const predictions = await model.classify(image);

// Get the model's predictions.
console.log(predictions);
```

## 2. Implementación del modelo en un servidor Node.js

Una vez que hayamos entrenado nuestro modelo, podemos implementarlo en un servidor Node.js. Esto nos permitirá procesar las imágenes entrantes y detectar objetos en tiempo real.

Para hacer esto, necesitaremos:

1. Instale la biblioteca TensorFlow.js.
2. Instale la biblioteca Node.js.
3. Cree un servidor Node.js.
4. Implemente el modelo en el servidor.

Veamos cómo podemos hacer esto en código:

```javascript
// Install the TensorFlow.js library.
npm install @tensorflow/tfjs

// Install the Node.js library.
npm install node

// Create a Node.js server.
const tf = require('@tensorflow/tfjs');
const express = require('express');
const app = express();

//Deploy the model to the server.
app.use(express.static(__dirname + '/model'));

// Process incoming images and detect objects in real-time.
app.post('/api/detect', async (req, res) => {
  // Classify the image.
  const predictions = await model.classify(req.body.image);

  // Send the predictions to the client.
  res.json(predictions);
});

// Start the server.
app.listen(3000, () => console.log('Server is running on port 3000'));
```

## 3. Usar el servidor para procesar imágenes entrantes y detectar objetos en tiempo real

Una vez que nuestro servidor está en funcionamiento, podemos usarlo para procesar imágenes entrantes y detectar objetos en tiempo real.

Para hacer esto, necesitaremos:

1. Envía una imagen al servidor.
2. El servidor procesará la imagen y devolverá las predicciones.
3. Podemos usar las predicciones para detectar objetos en la imagen.

Veamos cómo podemos hacer esto en código:

```javascript
// Send an image to the server.
const image = 'some-image.jpg';

fetch('/api/detect', {
  method: 'POST',
  body: JSON.stringify({ image }),
})
  .then(res => res.json())
  .then(predictions => {
    // Use the predictions to detect objects in the image.
    console.log(predictions);
  });
```

## Conclusión

En esta publicación, hemos aprendido a usar TensorFlow.js y Node.js para realizar la detección de objetos en tiempo real.