---
title: 083: Uso de TensorFlow.js con otros marcos de aprendizaje automático en Node.js
description: 
published: true
date: 2023-02-03T02:17:27.353Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:17:25.699Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [083: Using TensorFlow.js with Other ML Frameworks in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/083-using-tensorflow-js-with-other-ml-frameworks-in-node-js)
{.links-list}


# Uso de TensorFlow.js con otros marcos de ML en Node.js

TensorFlow.js es una poderosa biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. Se puede usar con otros marcos de ML, como TensorFlow Lite, para ejecutar inferencias en Node.js.

En esta publicación, le mostraremos cómo usar TensorFlow.js con otros marcos de ML en Node.js. También brindaremos algunos consejos sobre cómo aprovechar TensorFlow.js al máximo.

## Uso de TensorFlow.js con TensorFlow Lite

TensorFlow.js se puede usar con TensorFlow Lite para ejecutar inferencias en Node.js. TensorFlow Lite es un marco ligero para ejecutar modelos de aprendizaje automático en dispositivos móviles.

Para usar TensorFlow.js con TensorFlow Lite, deberá instalar los enlaces de TensorFlow Lite Node.js. Puedes hacer esto con npm:

```
npm install @tensorflow/tfjs-node
```

Una vez que se instalan los enlaces, puede usar el módulo `tensorflow.js` para cargar un modelo de TensorFlow Lite y ejecutar la inferencia en él.

Este es un ejemplo de cómo usar TensorFlow.js con TensorFlow Lite:

```javascript
const tf = require('@tensorflow/tfjs-node');

// Load a TensorFlow Lite model.
const model = await tf.loadLiteModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_1.0_224/model.json');

// Run inference on a TensorFlow Lite model.
const output = model.predict(tf.zeros([1, 224, 224, 3]));

// Print the output of the model.
console.log(output);
```

## Uso de TensorFlow.js con otros marcos de ML

TensorFlow.js también se puede usar con otros marcos de ML, como Keras, para ejecutar inferencias en Node.js.

Para usar TensorFlow.js con Keras, deberá instalar los enlaces TensorFlow.js Node.js. Puedes hacer esto con npm:

```
npm install @tensorflow/tfjs
```

Una vez que se instalan los enlaces, puede usar el módulo `tf` para cargar un modelo de Keras y ejecutar la inferencia en él.

Aquí hay un ejemplo de cómo usar TensorFlow.js con Keras:

```javascript
const tf = require('@tensorflow/tfjs');

// Load a Keras model.
const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_1.0_224/model.json');

// Run inference on a Keras model.
const output = model.predict(tf.zeros([1, 224, 224, 3]));

// Print the output of the model.
console.log(output);
```

## Sugerencias para usar TensorFlow.js

Estos son algunos consejos para usar TensorFlow.js:

- Si es nuevo en TensorFlow.js, le recomendamos que comience con la [guía de introducción a TensorFlow.js] (https://js.tensorflow.org/tutorials/getting-started.html).
- Si usa TensorFlow.js con otros marcos de aprendizaje automático, le recomendamos que use los [enlaces TensorFlow.js Node.js] (https://www.npmjs.com/package/@tensorflow/tfjs).
- Si usa TensorFlow.js con TensorFlow Lite, le recomendamos que use los [enlaces de Node.js de TensorFlow Lite] (https://www.npmjs.com/package/@tensorflow/tfjs-node).
- Si usa TensorFlow.js con un navegador web, le recomendamos que use un [backend basado en WebAssembly] (https://js.tensorflow.org/api/0.12.0/# habilitation-webassembly-support).