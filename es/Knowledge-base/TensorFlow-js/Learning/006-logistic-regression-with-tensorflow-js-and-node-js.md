---
title: 006: Regresión logística con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T08:04:27.378Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:04:25.797Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [006: Logistic Regression with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/006-logistic-regression-with-tensorflow-js-and-node-js)
{.links-list}


# Regresión logística con TensorFlow.js y Node.js

En esta publicación, aprenderemos cómo construir un modelo de regresión logística usando TensorFlow.js y Node.js.

La regresión logística es un método estadístico para predecir resultados binarios. Es decir, puede usarse para predecir si un evento ocurrirá o no. Por ejemplo, podemos usar la regresión logística para predecir si un paciente desarrollará una enfermedad, en función de ciertas características.

La regresión logística es un tipo de regresión lineal, pero con algunas diferencias importantes. Primero, la variable de resultado es binaria, lo que significa que solo puede tomar dos valores (0 o 1). En segundo lugar, el modelo se ajusta utilizando una estimación de máxima verosimilitud, en lugar de mínimos cuadrados.

## Empezando

Para comenzar, debemos instalar TensorFlow.js y Node.js. Esto lo podemos hacer usando los siguientes comandos:

```
npm install -g tensorflow
npm install -g node
```

Una vez que TensorFlow.js y Node.js están instalados, podemos crear un nuevo archivo llamado `logistic-regression.js` y comenzar a codificar.

## Datos

El primer paso es cargar nuestros datos. Usaremos la biblioteca `tensorflow.js` para cargar los datos en un objeto `tf.tensor`.

```javascript
const tf = require('tensorflow');

// Load the data
const data = tf.tensor([
  [1, 2],
  [2, 3],
  [3, 4],
  [4, 5],
]);
```

## Modelo

A continuación, necesitamos definir nuestro modelo. Usaremos un modelo de regresión logística con dos características de entrada (`x1` y `x2`) y una de salida (`y`).

```javascript
// Define the model
const model = tf.sequential();
model.add(tf.layers.dense({ units: 1, inputShape: [2] }));
model.compile({ loss: 'binaryCrossentropy', optimizer: 'sgd' });
```

## Capacitación

Ahora que tenemos nuestros datos y modelo, podemos entrenar nuestro modelo. Usaremos el método `fit` para entrenar nuestro modelo en los datos.

```javascript
// Train the model
model.fit(data, tf.tensor([1, 1, 0, 0]), {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    },
  },
});
```

## Predicción

Una vez que nuestro modelo está entrenado, podemos usarlo para hacer predicciones. Usaremos el método `predict` para predecir la salida de nuevos datos.

```javascript
// Make predictions
model.predict(tf.tensor([[5, 6]])).print(); // [[0.5]]
model.predict(tf.tensor([[6, 7]])).print(); // [[0.5]]
```

Como podemos ver, nuestro modelo predice la salida como 0.5 para ambas entradas. Esto significa que nuestro modelo predice un 50% de probabilidad de que ocurra el evento.

## Conclusión

En esta publicación, aprendimos cómo construir un modelo de regresión logística usando TensorFlow.js y Node.js. También hemos visto cómo usar nuestro modelo para hacer predicciones sobre nuevos datos.