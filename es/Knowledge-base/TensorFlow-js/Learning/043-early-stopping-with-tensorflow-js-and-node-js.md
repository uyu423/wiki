---
title: 043: Detención anticipada con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T17:04:41.506Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:04:37.002Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [043: Early Stopping with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/043-early-stopping-with-tensorflow-js-and-node-js)
{.links-list}


# Detención anticipada con TensorFlow.js y Node.js

El aprendizaje profundo es una técnica de redes neuronales que ha revolucionado muchos campos, incluida la visión por computadora, el procesamiento del lenguaje natural y el modelado predictivo. TensorFlow.js es una poderosa biblioteca de código abierto para entrenar e implementar modelos de aprendizaje profundo en JavaScript.

En esta publicación, aprenderemos a usar TensorFlow.js y Node.js para implementar la detención temprana, una técnica para entrenar redes neuronales que puede ayudar a prevenir el sobreajuste.

## ¿Qué es la detención temprana?

La detención anticipada es una técnica para entrenar redes neuronales que puede ayudar a prevenir el sobreajuste. El sobreajuste ocurre cuando un modelo se entrena en un conjunto de datos que es demasiado pequeño o demasiado simple, y el modelo comienza a aprender patrones que son específicos de ese conjunto de datos. Esto puede hacer que el modelo funcione mal con los datos nuevos.

La detención temprana es una forma de combatir el sobreajuste al detener el proceso de entrenamiento antes de que el modelo tenga la oportunidad de aprender estos patrones. Podemos hacer esto monitoreando el rendimiento del modelo en un conjunto de validación y deteniendo el proceso de entrenamiento cuando el rendimiento en el conjunto de validación comienza a disminuir.

## Implementando la detención anticipada con TensorFlow.js

Comenzaremos creando una red neuronal simple usando TensorFlow.js. Esta red tomará dos valores de entrada y predecirá un tercer valor de salida continuo. Lo entrenaremos en un conjunto de datos de 100 puntos.

```javascript
const tf = require('@tensorflow/tfjs');

// Create a neural network with two input nodes,
// one hidden layer with two nodes, and one output node
const model = tf.sequential();
model.add(tf.layers.dense({units: 2, inputShape: [2]}));
model.add(tf.layers.dense({units: 1}));

// Compile the model
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

// Generate some synthetic data for training
const xs = tf.tensor2d([[0, 0], [0, 1], [1, 0], [1, 1]]);
const ys = tf.tensor2d([[0], [1], [1], [0]]);

// Train the model
model.fit(xs, ys, {
  epochs: 100,
  validationData: [xs, ys],
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    }
  }
});
```

A continuación, agregaremos una devolución de llamada que detendrá el proceso de capacitación cuando la pérdida en el conjunto de validación comience a aumentar. Lo haremos haciendo un seguimiento de la pérdida en cada época y comparando la pérdida en la época actual con la pérdida en la época anterior. Si la pérdida ha aumentado, detendremos el proceso de entrenamiento.

```javascript
let previousLoss;

model.fit(xs, ys, {
  epochs: 100,
  validationData: [xs, ys],
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);

      if (previousLoss && log.loss > previousLoss) {
        model.stopTraining = true;
      }
      previousLoss = log.loss;
    }
  }
});
```

## Pruébalo

Puedes [probar este código por ti mismo](https://jsfiddle.net/jimmykim/9h5b7eLp/).

## Información Adicional

- [TensorFlow.js](https://js.tensorflow.org/)
- [Node.js](https://nodejs.org/en/)

## Recursos para leer más

- [Sobreajuste y ajuste insuficiente con TensorFlow.js](https://js.tensorflow.org/tutorials/overfitting_and_underfitting.html)
- [Detención anticipada](https://machinelearningmastery.com/how-to-evitate-overfitting-with-early-stopping/)