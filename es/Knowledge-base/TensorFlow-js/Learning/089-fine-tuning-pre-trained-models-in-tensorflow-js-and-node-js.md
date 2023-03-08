---
title: 089: Ajuste fino de modelos preentrenados en TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T03:44:04.110Z
tags: 
editor: markdown
dateCreated: 2023-02-03T03:43:59.389Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [089: Fine-Tuning Pre-Trained Models in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/089-fine-tuning-pre-trained-models-in-tensorflow-js-and-node-js)
{.links-list}


# 089: Ajuste fino de modelos preentrenados en TensorFlow.js y Node.js

TensorFlow.js es una poderosa herramienta que nos permite entrenar e implementar modelos de aprendizaje automático en el navegador. En esta publicación, aprenderemos cómo ajustar modelos previamente entrenados en TensorFlow.js y Node.js.

## ¿Qué son los modelos preentrenados?

Los modelos preentrenados son modelos de aprendizaje automático que se han entrenado en un gran conjunto de datos. Estos modelos se pueden utilizar para realizar tareas como la clasificación de imágenes, la detección de objetos y la clasificación de textos.

## ¿Por qué ajustar modelos preentrenados?

El ajuste fino de modelos previamente entrenados es una técnica común en el aprendizaje automático. Nos permite adaptar modelos pre-entrenados a nuestro propio conjunto de datos. Esto puede ser útil cuando nuestro conjunto de datos es pequeño o cuando queremos mejorar el rendimiento de un modelo previamente entrenado en nuestro conjunto de datos.

## ¿Cómo afinar los modelos preentrenados?

Hay dos formas comunes de ajustar modelos preentrenados:

1. **Aprendizaje de transferencia**: podemos usar un modelo previamente entrenado como punto de partida y luego entrenarlo en nuestro propio conjunto de datos. Esta es una técnica común cuando nuestro conjunto de datos es pequeño.

2. **Ajuste fino**: Podemos usar un modelo previamente entrenado y luego ajustarlo en nuestro propio conjunto de datos. Esta es una técnica común cuando queremos mejorar el rendimiento de un modelo previamente entrenado en nuestro conjunto de datos.

En esta publicación, nos centraremos en ajustar modelos pre-entrenados.

## Ajuste fino de modelos previamente entrenados en TensorFlow.js

TensorFlow.js proporciona una API de alto nivel para ajustar modelos previamente entrenados. Usaremos la función `tf.fineTuneModel()` para ajustar un modelo previamente entrenado.

Primero, necesitamos cargar un modelo previamente entrenado. Usaremos la función `tf.loadLayersModel()` para cargar un modelo previamente entrenado desde una URL.

A continuación, necesitamos definir las entradas y salidas del modelo. Usaremos las funciones `tf.input()` y `tf.output()` para definir las entradas y salidas del modelo.

Finalmente, necesitamos llamar a la función `tf.fineTuneModel()` para ajustar el modelo pre-entrenado. Tendremos que especificar el optimizador, la pérdida y las métricas.

Este es un ejemplo de cómo ajustar un modelo previamente entrenado en TensorFlow.js:

```javascript
// Load a pre-trained model
const model = tf.loadLayersModel('https://model-url');

// Define the inputs and outputs of the model
const input = tf.input({shape: [28, 28, 1]});
const output = model.outputs[0];

// Fine-tune the model
const model = tf.fineTuneModel(
    model,
    {
      optimizer: tf.train.adam(0.001),
      loss: tf.losses.softmaxCrossEntropy,
      metrics: ['accuracy']
    },
    {
      // We will use a validation split of 0.1
      validationSplit: 0.1
    }
);
```

## Ajuste fino de modelos preentrenados en Node.js

TensorFlow.js proporciona una API de Node.js para ajustar modelos preentrenados. Usaremos la función `tf.node.fineTuneModel()` para ajustar un modelo previamente entrenado.

Primero, necesitamos cargar un modelo previamente entrenado. Usaremos la función `tf.node.loadLayersModel()` para cargar un modelo previamente entrenado desde una URL.

A continuación, necesitamos definir las entradas y salidas del modelo. Usaremos las funciones `tf.node.input()` y `tf.node.output()` para definir las entradas y salidas del modelo.

Finalmente, necesitamos llamar a la función `tf.node.fineTuneModel()` para ajustar el modelo pre-entrenado. Tendremos que especificar el optimizador, la pérdida y las métricas.

Este es un ejemplo de cómo ajustar un modelo previamente entrenado en Node.js:

```javascript
// Load a pre-trained model
const model = tf.node.loadLayersModel('https://model-url');

// Define the inputs and outputs of the model
const input = tf.node.input({shape: [28, 28, 1]});
const output = model.outputs[0];

// Fine-tune the model
const model = tf.node.fineTuneModel(
    model,
    {
      optimizer: tf.train.adam(0.001),
      loss: tf.losses.softmaxCrossEntropy,
      metrics: ['accuracy']
    },
    {
      // We will use a validation split of 0.1
      validationSplit: 0.1
    }
);
```

## Conclusión

En esta publicación, aprendimos cómo ajustar modelos previamente entrenados en TensorFlow.js y Node.js. Vimos que TensorFlow.js proporciona una API de alto nivel para ajustar modelos preentrenados. También vimos que TensorFlow.js proporciona una API de Node.js para ajustar modelos preentrenados.