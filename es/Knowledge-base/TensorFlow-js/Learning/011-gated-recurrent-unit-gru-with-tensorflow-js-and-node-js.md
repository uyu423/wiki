---
title: 011: Unidad recurrente cerrada (GRU) con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T09:17:22.473Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:17:20.888Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [011: Gated Recurrent Unit (GRU) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/011-gated-recurrent-unit-gru-with-tensorflow-js-and-node-js)
{.links-list}


# Unidad recurrente cerrada (GRU) con TensorFlow.js y Node.js

En esta publicación, aprenderemos sobre las unidades recurrentes cerradas (GRU) y cómo implementarlas con TensorFlow.js y Node.js.

## ¿Qué son las unidades recurrentes cerradas?

Las GRU son un tipo de red neuronal recurrente (RNN). Las RNN son redes neuronales que pueden procesar secuencias de datos, como texto, audio o datos de series temporales.

Las GRU son un tipo de RNN que utiliza puertas para controlar el flujo de información en la red. Las puertas ayudan a la red a aprender mejor las dependencias a largo plazo.

## Implementando una GRU con TensorFlow.js

Usaremos TensorFlow.js para implementar una GRU. TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático en el navegador y en Node.js.

Primero, necesitaremos instalar TensorFlow.js. Esto lo podemos hacer con el siguiente comando:

```
npm install @tensorflow/tfjs
```

A continuación, necesitaremos cargar los datos que usaremos para entrenar el modelo. Usaremos el conjunto de datos MNIST, que es un conjunto de datos de dígitos escritos a mano.

Podemos cargar el conjunto de datos MNIST con el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MNIST dataset.
const mnistData = require('mnist-data');

// Convert the MNIST data to a TensorFlow.js tensor.
const mnistTensor = tf.tensor3d(mnistData.images, [mnistData.images.length, 28, 28]);
```

Ahora que tenemos los datos cargados, podemos definir el modelo. Usaremos un GRU con 64 unidades.

```javascript
// Define the model.
const model = tf.sequential();
model.add(tf.layers.gru({units: 64, inputShape: [28, 28]}));
model.add(tf.layers.dense({units: 10, activation: 'softmax'}));
```

A continuación, necesitaremos compilar el modelo. Usaremos el optimizador de Adam y la función de pérdida de entropía cruzada categórica.

```javascript
// Compile the model.
model.compile({optimizer: 'adam', loss: 'categoricalCrossentropy', metrics: ['accuracy']});
```

Ahora, podemos entrenar el modelo. Lo entrenaremos durante 10 épocas.

```javascript
// Train the model.
model.fit(mnistTensor, mnistData.labels, {epochs: 10}).then(() => {
  // The model is trained!
});
```

¡Eso es! Ahora hemos capacitado a una GRU para clasificar los dígitos escritos a mano.

## Implementando una GRU con Node.js

También podemos usar Node.js para entrenar una GRU. Node.js es un tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript fuera del navegador.

Primero, necesitaremos instalar TensorFlow.js. Esto lo podemos hacer con el siguiente comando:

```
npm install @tensorflow/tfjs
```

A continuación, necesitaremos cargar los datos que usaremos para entrenar el modelo. Usaremos el conjunto de datos MNIST, que es un conjunto de datos de dígitos escritos a mano.

Podemos cargar el conjunto de datos MNIST con el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MNIST dataset.
const mnistData = require('mnist-data');

// Convert the MNIST data to a TensorFlow.js tensor.
const mnistTensor = tf.tensor3d(mnistData.images, [mnistData.images.length, 28, 28]);
```

Ahora que tenemos los datos cargados, podemos definir el modelo. Usaremos un GRU con 64 unidades.

```javascript
// Define the model.
const model = tf.sequential();
model.add(tf.layers.gru({units: 64, inputShape: [28, 28]}));
model.add(tf.layers.dense({units: 10, activation: 'softmax'}));
```

A continuación, necesitaremos compilar el modelo. Usaremos el optimizador de Adam y la función de pérdida de entropía cruzada categórica.

```javascript
// Compile the model.
model.compile({optimizer: 'adam', loss: 'categoricalCrossentropy', metrics: ['accuracy']});
```

Ahora, podemos entrenar el modelo. Lo entrenaremos durante 10 épocas.

```javascript
// Train the model.
model.fit(mnistTensor, mnistData.labels, {epochs: 10}).then(() => {
  // The model is trained!
});
```

¡Eso es! Ahora hemos capacitado a una GRU para clasificar los dígitos escritos a mano.