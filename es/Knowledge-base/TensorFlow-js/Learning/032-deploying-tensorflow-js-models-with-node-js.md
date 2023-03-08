---
title: 032: Implementación de modelos de TensorFlow.js con Node.js
description: 
published: true
date: 2023-02-02T14:36:46.460Z
tags: 
editor: markdown
dateCreated: 2023-02-02T14:36:44.821Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [032: Deploying TensorFlow.js Models with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/032-deploying-tensorflow-js-models-with-node-js)
{.links-list}


# 032: Implementación de modelos de TensorFlow.js con Node.js

TensorFlow.js es una biblioteca JavaScript de código abierto para aprendizaje automático que permite a los desarrolladores entrenar e implementar modelos ML en el navegador o en Node.js.

En esta publicación, aprenderemos a usar TensorFlow.js para implementar un modelo de aprendizaje automático previamente entrenado en una aplicación de Node.js. También aprenderemos a usar la API de Node.js para ejecutar inferencias en el modelo.

## Requisitos previos

Antes de comenzar, necesitará lo siguiente:

* Nodo.js
* Un editor de texto
* Un navegador web

## Empezando

Primero, necesitamos instalar la biblioteca TensorFlow.js. Podemos hacer esto usando el Administrador de paquetes de nodos (NPM):

```
npm install @tensorflow/tfjs
```

A continuación, necesitamos descargar el modelo ML preentrenado. Para este ejemplo, usaremos el modelo de clasificación de imágenes [MobileNet](https://github.com/tensorflow/tfjs-models/tree/master/mobilenet).

Una vez descargado el modelo, podemos implementarlo en nuestra aplicación Node.js.

## Desplegando el modelo

Para implementar el modelo, necesitamos crear un nuevo archivo llamado `index.js`. En este archivo, usaremos la función `tf.loadModel()` para cargar el modelo previamente entrenado:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
  });
```

## Uso del modelo

Una vez que se carga el modelo, podemos usarlo para ejecutar la inferencia en una imagen. Para este ejemplo, usaremos el [ejemplo de clasificación de imágenes de TensorFlow.js](https://github.com/tensorflow/tfjs-examples/tree/master/image-classification).

Primero, necesitamos cargar la imagen en un `tf.Tensor`:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
    const img = tf.tensor3d(imageData, [224, 224, 3]);
  });
```

A continuación, necesitamos preprocesar la imagen usando la función `mobilenet.preprocessInput()`:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
    const img = tf.tensor3d(imageData, [224, 224, 3]);

    // Pre-process the image.
    const preprocessedImg = tf.mobilenet.preprocessInput(img);
  });
```

Finalmente, podemos usar la función `model.predict()` para ejecutar la inferencia en la imagen:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
    const img = tf.tensor3d(imageData, [224, 224, 3]);

    // Pre-process the image.
    const preprocessedImg = tf.mobilenet.preprocessInput(img);

    // Run inference.
    model.predict(preprocessedImg).then(predictions => {
      // Use the predictions.
    });
  });
```

La variable `predictions` contiene los resultados de la inferencia.

## Conclusión

En esta publicación, aprendimos a usar TensorFlow.js para implementar un modelo de aprendizaje automático previamente entrenado en una aplicación de Node.js. También aprendimos a usar la API de Node.js para ejecutar inferencias en el modelo.