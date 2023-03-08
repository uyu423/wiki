---
title: 023: Generación de Texto con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T12:17:20.864Z
tags: 
editor: markdown
dateCreated: 2023-02-02T12:17:19.212Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [023: Text Generation with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/023-text-generation-with-tensorflow-js-and-node-js)
{.links-list}


# Generación de Texto con TensorFlow.js y Node.js

En esta publicación, aprenderemos cómo generar texto usando TensorFlow.js y Node.js. Usaremos un modelo char-rnn, que es un tipo de red neuronal recurrente (RNN) que puede aprender a predecir el siguiente carácter en una secuencia de texto.

## ¿Qué es un char-rnn?

Un char-rnn es un tipo de RNN que puede aprender a predecir el siguiente carácter en una secuencia de texto. El modelo char-rnn que usaremos se basa en el que se describe en el artículo "Modelos de lenguaje neuronal conscientes del carácter" (https://arxiv.org/abs/1508.06615).

## ¿Qué es TensorFlow.js?

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático en el navegador y en Node.js.

## ¿Qué es Node.js?

Node.js es un tiempo de ejecución de JavaScript basado en el motor de JavaScript V8 de Chrome.

## Empezando

Primero, necesitamos instalar TensorFlow.js y Node.js. Usaremos el modelo char-rnn de TensorFlow.js, que es un módulo de Node.js.

```
npm install @tensorflow/tfjs-node
npm install @tensorflow/tfjs-node-charrnn
```

A continuación, necesitamos descargar los datos de entrenamiento. Para este ejemplo, usaremos un conjunto de datos de las obras de Shakespeare (https://www.kaggle.com/kinguistics/shakespeare-plays).

Una vez que tengamos los datos de entrenamiento, podemos comenzar a entrenar el modelo char-rnn. El proceso de formación puede tardar unos minutos en completarse.

```
const tf = require('@tensorflow/tfjs-node');
const charRNN = require('@tensorflow/tfjs-node-charrnn');

const model = charRNN.create(
  'https://storage.googleapis.com/tfjs-models/tfjs/charrnn/data/shakespeare_input.txt',
  {
    rnnType: 'lstm',
    embeddingSize: 128,
    rnnUnits: 128,
    batchSize: 64,
    seqLength: 128,
    temperature: 0.8,
    numEpochs: 20
  });

model.fit().then(() => {
  // The model is trained!
});
```

Una vez que el modelo está entrenado, podemos usarlo para generar texto.

```
model.generate('The').then((text) => {
  console.log(text);
});
```

## Información Adicional

- Para obtener más información sobre TensorFlow.js, consulte la documentación de TensorFlow.js (https://js.tensorflow.org/).
- Para obtener más información sobre Node.js, consulte la documentación de Node.js (https://nodejs.org/en/docs/).