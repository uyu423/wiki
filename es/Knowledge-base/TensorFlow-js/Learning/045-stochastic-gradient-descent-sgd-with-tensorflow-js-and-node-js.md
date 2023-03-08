---
title: 045: descenso de gradiente estocástico (SGD) con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T17:36:46.296Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:36:41.301Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [045: Stochastic Gradient Descent (SGD) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/045-stochastic-gradient-descent-sgd-with-tensorflow-js-and-node-js)
{.links-list}


# Descenso de gradiente estocástico (SGD) con TensorFlow.js y Node.js

El descenso de gradiente estocástico (SGD) es un método de optimización ampliamente utilizado para entrenar modelos de aprendizaje profundo. SGD funciona actualizando iterativamente los pesos de un modelo en la dirección que minimiza la función de costo.

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático en el navegador o en Node.js. En este tutorial, mostraremos cómo usar TensorFlow.js y SGD para entrenar un modelo de regresión lineal simple.

## Empezando

Primero, instalemos TensorFlow.js y sus dependencias. Necesitaremos Node.js y npm instalados para hacer esto.

    $ npm install @tensorflow/tfjs @tensorflow/tfjs-node

A continuación, necesitaremos crear un archivo para nuestro código. Lo llamaremos `sgd.js`.

## Los datos

Usaremos un conjunto de datos muy simple para este tutorial. Consta de solo dos columnas: `x` e `y`. `x` es una lista de números del 1 al 100, y `y` es una lista de los cuadrados de esos números.

Podemos generar este conjunto de datos fácilmente con TensorFlow.js:

```javascript
const xs = tf.range(1, 100, 1);
const ys = xs.square();
```

## El modelo

Nuestro modelo será un modelo de regresión lineal muy simple. Los modelos de regresión lineal se utilizan para predecir un valor continuo, como un precio o una cantidad.

Nuestro modelo tendrá un solo peso y un sesgo:

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({ units: 1, inputShape: [1] }));
```

## La función de costo

La función de costo es una medida de qué tan bien está funcionando nuestro modelo. Queremos minimizar la función de costo, lo que significa que queremos encontrar el conjunto de pesos y sesgos que hacen que las predicciones de nuestro modelo se acerquen lo más posible a los valores reales.

Hay muchas funciones de costo diferentes que se pueden usar para la regresión lineal. Para este tutorial, usaremos la función de costo del error cuadrático medio:

```javascript
function meanSquaredError(labels, predictions) {
  const error = labels.sub(predictions).square().mean();
  return error;
}
```

## El Optimizador

El optimizador es el algoritmo que usamos para actualizar los pesos y sesgos de nuestro modelo. SGD es una opción popular para los optimizadores, pero hay muchos otros para elegir.

Para este tutorial, usaremos el optimizador SGD con una tasa de aprendizaje de 0,1:

```javascript
const optimizer = tf.train.sgd(0.1);
```

## Entrenamiento del modelo

Ahora que tenemos nuestros datos, nuestro modelo, nuestra función de costo y nuestro optimizador, estamos listos para entrenar nuestro modelo.

Entrenar un modelo en TensorFlow.js es fácil. Solo necesitamos llamar al método `fit` en nuestro modelo, pasando nuestros datos y el número de épocas (iteraciones) para las que queremos entrenar:

```javascript
model.fit(xs, ys, {
  epochs: 100,
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    }
  }
});
```

## Evaluación del modelo

Una vez que el modelo está entrenado, podemos evaluarlo con nuevos datos. Para este tutorial, generaremos un nuevo conjunto de datos con valores `x` del 1 al 10 y valores `y` del 1 al 100.

```javascript
const xs = tf.range(1, 10, 1);
const ys = tf.range(1, 100, 1);
```

Podemos usar el método `predecir` para hacer predicciones sobre estos nuevos datos:

```javascript
const predictions = model.predict(xs);
```

Finalmente, podemos comparar las predicciones con los valores reales para ver qué tan bien funcionó nuestro modelo:

```javascript
predictions.print();
ys.print();
```

## Información Adicional

- [Documentación de TensorFlow.js](https://js.tensorflow.org/)
- [Tutorial de regresión lineal](https://machinelearningmastery.com/linear-regression-tutorial-machine-learning/)
- [Documentación de SGD Optimizer](https://www.tensorflow.org/api_docs/python/tf/train/GradientDescentOptimizer)