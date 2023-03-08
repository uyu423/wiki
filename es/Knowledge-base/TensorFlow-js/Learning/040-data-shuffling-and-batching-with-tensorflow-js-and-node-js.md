---
title: 040: Mezcla y agrupación de datos con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T16:17:34.750Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:17:33.109Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [040: Data Shuffling and Batching with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/040-data-shuffling-and-batching-with-tensorflow-js-and-node-js)
{.links-list}


# Reorganización y procesamiento por lotes de datos con TensorFlow.js y Node.js

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático en el navegador y en Node.js.

En este tutorial, aprenderemos a mezclar y agrupar datos con TensorFlow.js. Cubriremos los siguientes temas:

* ¿Qué es el barajado de datos y por qué es importante?
* ¿Cómo mezclar datos con TensorFlow.js?
* ¿Cómo agrupar datos por lotes con TensorFlow.js?
* ¿Cómo barajar y agrupar datos junto con TensorFlow.js?

## ¿Qué es el barajado de datos y por qué es importante?

Al entrenar modelos de aprendizaje automático, es importante mezclar los datos antes de cada época. Esto se debe a que, si los datos no se mezclan, el modelo podría sobreajustarse en las primeras muestras del conjunto de datos.

El barajado de datos es el proceso de reordenar aleatoriamente las muestras en un conjunto de datos. Esto se puede hacer antes o después de cada época.

Hay dos ventajas principales de mezclar datos:

* Ayuda a evitar que el modelo se sobreajuste en las primeras muestras del conjunto de datos.
* Puede ayudar a que el modelo converja más rápido, ya que ve diferentes muestras en cada época.

## ¿Cómo mezclar datos con TensorFlow.js?

Para mezclar datos con TensorFlow.js, primero debemos convertir nuestros datos en un `tf.data.Dataset`.

Podemos hacer esto usando los métodos `tf.data.array()` o `tf.data.tensor()`:

```js
// Convert an array into a dataset
const dataset = tf.data.array([1, 2, 3, 4, 5]);

// Convert a tensor into a dataset
const dataset = tf.data.tensor([1, 2, 3, 4, 5]);
```

Una vez que tengamos nuestro conjunto de datos, podemos usar `tf.data. método shuffle()` para mezclar los datos:

```js
const shuffledDataset = dataset.shuffle();
```

## ¿Cómo agrupar datos por lotes con TensorFlow.js?

Para agrupar datos con TensorFlow.js, primero debemos convertir nuestros datos en un `tf.data.Dataset`.

Podemos hacer esto usando los métodos `tf.data.array()` o `tf.data.tensor()`:

```js
// Convert an array into a dataset
const dataset = tf.data.array([1, 2, 3, 4, 5]);

// Convert a tensor into a dataset
const dataset = tf.data.tensor([1, 2, 3, 4, 5]);
```

Una vez que tengamos nuestro conjunto de datos, podemos usar `tf.data. método batch()` para agrupar los datos:

```js
const batchedDataset = dataset.batch(2);
```

## ¿Cómo barajar y agrupar datos junto con TensorFlow.js?

Para mezclar y agrupar datos junto con TensorFlow.js, primero debemos convertir nuestros datos en un `tf.data.Dataset`.

Podemos hacer esto usando los métodos `tf.data.array()` o `tf.data.tensor()`:

```js
// Convert an array into a dataset
const dataset = tf.data.array([1, 2, 3, 4, 5]);

// Convert a tensor into a dataset
const dataset = tf.data.tensor([1, 2, 3, 4, 5]);
```

Una vez que tengamos nuestro conjunto de datos, podemos usar `tf.data. barajar()` y `tf.data. Batch()` métodos para mezclar y procesar por lotes los datos:

```js
const shuffledAndBatchedDataset = dataset.shuffle().batch(2);
```