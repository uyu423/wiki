---
title: 007: Perceptrón multicapa (MLP) con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T08:17:32.657Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:17:30.975Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [007: Multilayer Perceptron (MLP) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/007-multilayer-perceptron-mlp-with-tensorflow-js-and-node-js)
{.links-list}


## Introducción

En esta publicación, cubriremos cómo construir un perceptrón multicapa (MLP) con TensorFlow.js y Node.js. Repasaremos los conceptos fundamentales detrás de las redes neuronales y el aprendizaje profundo, y cómo implementarlos usando TensorFlow.js. Al final de esta publicación, podrá crear sus propias redes neuronales y usarlas para resolver problemas del mundo real.

## ¿Qué es un perceptrón multicapa?

Un perceptrón multicapa (MLP) es un tipo de red neuronal. Las redes neuronales son un tipo de algoritmo de aprendizaje automático que se utilizan para modelar patrones complejos en los datos. Las MLP son un tipo específico de red neuronal que se compone de múltiples capas de neuronas.

La primera capa de un MLP es la capa de entrada, que recibe los datos de entrada. La segunda capa es la capa oculta, que transforma los datos de entrada en una nueva representación. La capa oculta es seguida por la capa de salida, que produce la salida del MLP.

## Construyendo un MLP con TensorFlow.js

TensorFlow.js es una biblioteca de JavaScript para crear redes neuronales y modelos de aprendizaje automático. Se puede usar tanto en el navegador como en Node.js.

Para usar TensorFlow.js, primero debemos instalarlo. Podemos hacer esto usando el Administrador de paquetes de nodos (NPM):

```
npm install @tensorflow/tfjs
```

Una vez instalado TensorFlow.js, podemos importarlo a nuestro proyecto:

```javascript
const tf = require('@tensorflow/tfjs');
```

Ahora que tenemos instalado e importado TensorFlow.js, podemos comenzar a construir nuestro MLP.

El primer paso es definir la capa de entrada. Podemos hacer esto usando la función `input`:

```javascript
const inputLayer = tf.input({shape: [2]});
```

La función `input` toma un objeto como argumento. La propiedad `shape` de este objeto define la forma de los datos de entrada. En este caso, estamos usando una entrada bidimensional, por lo que la propiedad `shape` se establece en `[2]`.

A continuación, necesitamos definir la capa oculta. Podemos hacer esto usando la función `layers`:

```javascript
const hiddenLayer = tf.layers.dense({
  units: 4,
  activation: 'sigmoid',
  inputShape: [2]
});
```

La función `layers` toma un objeto como argumento. La propiedad `unidades` define el número de neuronas en la capa. La propiedad `activación` define la función de activación de la capa. En este caso, estamos usando la función de activación sigmoidea. La propiedad `inputShape` define la forma de los datos de entrada.

Finalmente, necesitamos definir la capa de salida. Podemos hacer esto usando la función `layers`:

```javascript
const outputLayer = tf.layers.dense({
  units: 1,
  activation: 'sigmoid',
  inputShape: [4]
});
```

Al igual que con la capa oculta, la propiedad `unidades` define el número de neuronas en la capa. La propiedad `activación` define la función de activación de la capa. En este caso, estamos usando nuevamente la función de activación sigmoidea. La propiedad `inputShape` define la forma de los datos de entrada.

Ahora que hemos definido las capas de nuestro MLP, necesitamos conectarlas. Podemos hacer esto usando la función `secuencial`:

```javascript
const model = tf.sequential();
```

La función `secuencial` toma una matriz de capas como argumento. En este caso, estamos pasando nuestra capa de entrada, capa oculta y capa de salida.

Ahora que nuestro modelo está definido, necesitamos compilarlo. Podemos hacer esto usando la función `compilar`:

```javascript
model.compile({
  optimizer: 'sgd',
  loss: 'meanSquaredError'
});
```

La función `compilar` toma un objeto como argumento. La propiedad `optimizer` define el optimizador que se usará para entrenar el modelo. En este caso, estamos utilizando el optimizador de descenso de gradiente estocástico (SGD). La propiedad `loss` define la función de pérdida que se utilizará para evaluar el modelo. En este caso, estamos usando la función de pérdida del error cuadrático medio (MSE).

Ahora que nuestro modelo está compilado, podemos entrenarlo. Podemos hacer esto usando la función `fit`:

```javascript
model.fit(x, y, {
  epochs: 100,
  batchSize: 32
});
```

La función `fit` toma tres argumentos: los datos de entrenamiento (`x`), los datos objetivo (`y`) y un objeto que especifica los parámetros de entrenamiento. La propiedad `epochs` define el número de épocas de entrenamiento. La propiedad `batchSize` define el número de muestras en cada lote de entrenamiento.

Una vez que el modelo está entrenado, podemos usarlo para hacer predicciones. Podemos hacer esto usando la función `predecir`:

```javascript
model.predict(x).print();
```

La función `predecir` toma una matriz de datos de entrada (`x`) y devuelve una matriz de predicciones. La función `imprimir` imprime las predicciones en la consola.

## Conclusión

En esta publicación, cubrimos cómo construir un perceptrón multicapa (MLP) con TensorFlow.js y Node.js. Repasamos los conceptos fundamentales detrás de las redes neuronales y el aprendizaje profundo, y cómo implementarlos usando TensorFlow.js. Al final de esta publicación, debería poder construir sus propias redes neuronales y usarlas para resolver problemas del mundo real.