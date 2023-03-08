---
title: 047: Optimización de Adagrad con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T18:04:38.901Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:04:37.336Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [047: Adagrad Optimization with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/047-adagrad-optimization-with-tensorflow-js-and-node-js)
{.links-list}


# Optimización de Adagrad con TensorFlow.js y Node.js

TensorFlow.js es una poderosa herramienta que le permite realizar aprendizaje automático en JavaScript. En esta publicación, le mostraremos cómo usar TensorFlow.js y Node.js para optimizar un modelo de aprendizaje automático mediante el algoritmo de optimización de Adagrad.

## ¿Qué es Adagrad?

Adagrad es un algoritmo de optimización muy adecuado para entrenar redes neuronales profundas. Es un algoritmo basado en gradientes que adapta la tasa de aprendizaje a los parámetros individuales del modelo. Esto se hace escalando la tasa de aprendizaje por un factor que es inversamente proporcional a la raíz cuadrada de la suma de los cuadrados de los gradientes de los parámetros.

## Cómo usar Adagrad con TensorFlow.js

Para usar Adagrad con TensorFlow.js, deberá instalar la biblioteca TensorFlow.js Node.js. Puedes hacer esto con el siguiente comando:

```
npm install @tensorflow/tfjs-node
```

Una vez que la biblioteca está instalada, puede crear un nuevo archivo y requerir la biblioteca con el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs-node');
```

A continuación, crearemos un modelo de regresión lineal simple. Usaremos la función `tf.secuencial` para crear el modelo y la función `tf.layers.dense` para crear una capa densa. Una capa densa es una capa en la que cada nodo está conectado a todos los demás nodos de la capa anterior.

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({ units: 1, inputShape: [1] }));
```

Después de crear el modelo, necesitamos compilarlo. Esto se hace con la función `tf.model.compile`. Necesitamos especificar la función de pérdida y el optimizador. Para la función de pérdida, usaremos `tf.losses.meanSquaredError`. Esta función de pérdida se utiliza para problemas de regresión. Para el optimizador, usaremos `tf.train.adagrad`.

```javascript
model.compile({
  loss: tf.losses.meanSquaredError,
  optimizer: tf.train.adagrad(0.1),
});
```

La función `tf.train.adagrad` toma una tasa de aprendizaje como argumento. Esta es la tasa de aprendizaje que utilizará el algoritmo de Adagrad.

## Cómo entrenar el modelo

Ahora que hemos compilado el modelo, podemos entrenarlo. Usaremos la función `tf.model.fit` para entrenar el modelo. Necesitamos especificar los datos de entrenamiento, el número de épocas y el tamaño del lote.

```javascript
const xs = tf.tensor1d([1, 2, 3, 4]);
const ys = tf.tensor1d([1, 3, 5, 7]);

model.fit(xs, ys, {
  epochs: 10,
  batchSize: 4,
});
```

Los datos de entrenamiento son un tensor TensorFlow.js que contiene los valores de entrada y los valores de salida. Los valores de entrada son los valores de x y los valores de salida son los valores de y. El tamaño del lote es la cantidad de ejemplos de capacitación que se utilizan en cada iteración de la capacitación. El número de épocas es el número de veces que el algoritmo de entrenamiento pasará por los datos de entrenamiento.

## Cómo usar el modelo entrenado

Después de entrenar el modelo, podemos usarlo para hacer predicciones. Usaremos la función `tf.model.predict` para hacer predicciones. Necesitamos especificar los datos de entrada.

```javascript
const xs = tf.tensor1d([5, 6, 7, 8]);
const ys = model.predict(xs);
```

Los datos de entrada son un tensor TensorFlow.js que contiene los valores de entrada. La salida de la función `tf.model.predict` es un tensor TensorFlow.js que contiene las predicciones.

## Conclusión

En esta publicación, le mostramos cómo usar TensorFlow.js y Node.js para optimizar un modelo de aprendizaje automático mediante el algoritmo de optimización de Adagrad.