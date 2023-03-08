---
title: 005: Regresión lineal con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T07:43:33.550Z
tags: 
editor: markdown
dateCreated: 2023-02-02T07:43:31.956Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [005: Linear Regression with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/005-linear-regression-with-tensorflow-js-and-node-js)
{.links-list}


# Regresión lineal con TensorFlow.js y Node.js

En esta publicación, aprenderemos cómo realizar una regresión lineal con TensorFlow.js y Node.js. Comenzaremos revisando brevemente la regresión lineal y luego veremos cómo implementarla usando TensorFlow.js.

## ¿Qué es la regresión lineal?

La regresión lineal es una técnica estadística que se utiliza para modelar la relación entre una variable dependiente y una o más variables independientes. La variable dependiente es la variable que se predice, mientras que las variables independientes son las variables que se utilizan para predecir la variable dependiente.

En un modelo de regresión lineal, la variable dependiente es una función lineal de las variables independientes. Es decir, la variable dependiente es una función lineal de las variables independientes.

## ¿Cómo realizar una regresión lineal con TensorFlow.js?

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. También se utiliza para el cálculo numérico. En esta sección, veremos cómo usar TensorFlow.js para la regresión lineal.

Usaremos los siguientes datos para nuestro ejemplo de regresión lineal:

| X | Y |
|---|---|
| 1 | 2 |
| 2 | 4 |
| 3 | 6 |

El primer paso es importar la biblioteca TensorFlow.js. Podemos hacer esto usando la función require():

```javascript
const tf = require('@tensorflow/tfjs');
```

A continuación, necesitamos definir las variables independientes y dependientes. Podemos hacer esto usando la función tf.tensor():

```javascript
// Define the independent variable
const x = tf.tensor([1, 2, 3], [3, 1]);

// Define the dependent variable
const y = tf.tensor([2, 4, 6], [3, 1]);
```

Ahora que hemos definido las variables independientes y dependientes, podemos definir el modelo de regresión lineal. Podemos hacer esto usando la función tf.layers.dense():

```javascript
// Define the linear regression model
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));
```

El siguiente paso es compilar el modelo de regresión lineal. Podemos hacer esto usando la función tf.model.compile():

```javascript
// Compile the linear regression model
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});
```

Finalmente, podemos entrenar el modelo de regresión lineal. Podemos hacer esto usando la función tf.model.fit():

```javascript
// Train the linear regression model
model.fit(x, y, {epochs: 100}).then(() => {
  // Use the model to predict the value of y for x = 4
  model.predict(tf.tensor([4], [1, 1])).print();
});
```

## Conclusión

En esta publicación, hemos visto cómo realizar una regresión lineal usando TensorFlow.js y Node.js. También hemos visto cómo usar el modelo de regresión lineal para predecir el valor de una variable dependiente para una variable independiente dada.