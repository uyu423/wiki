---
title: 072: Uso de TensorFlow.js con trabajadores de Node.js
description: 
published: true
date: 2023-02-02T23:37:03.464Z
tags: 
editor: markdown
dateCreated: 2023-02-02T23:37:01.830Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [072: Using TensorFlow.js with Node.js Workers***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/072-using-tensorflow-js-with-node-js-workers)
{.links-list}


# Uso de TensorFlow.js con trabajadores de Node.js

TensorFlow.js es una poderosa herramienta para el aprendizaje automático en JavaScript, y Node.js Workers brinda una excelente manera de aprovechar los sistemas de varios núcleos y mantener el ciclo de eventos principal funcionando sin problemas.

En esta publicación, veremos cómo usar TensorFlow.js con Node.js Workers para entrenar modelos de aprendizaje automático. Comenzaremos con un ejemplo simple para poner las cosas en marcha y luego veremos un ejemplo más complejo que muestra cómo usar un grupo de Worker para entrenar varios modelos en paralelo.

## Primeros pasos con TensorFlow.js y Workers

Para comenzar, necesitaremos instalar TensorFlow.js y el complemento @tensorflow/tfjs-node Worker. Podemos hacer esto con npm:

```
npm install @tensorflow/tfjs @tensorflow/tfjs-node
```

Una vez que tengamos TensorFlow.js y el complemento Worker instalados, podemos comenzar a escribir algo de código.

Comenzaremos entrenando un modelo simple para clasificar dígitos escritos a mano del conjunto de datos MNIST. Primero, necesitaremos cargar el conjunto de datos:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MNIST dataset
const mnistData = tf.data.web('https://storage.googleapis.com/tfjs-examples/mnist_train_small.csv');
```

A continuación, definiremos una función para convertir el conjunto de datos en un formato que TensorFlow.js pueda comprender. Esta función tomará una matriz de números y devolverá un tensor TensorFlow.js:

```javascript
// Convert the dataset into a format that TensorFlow.js can understand
const convertToTensor = (data) => {
  // Wrapping this in a tidy will dispose the tensor when we're done
  return tf.tidy(() => {
    // Convert the data to a TensorFlow.js tensor
    const tensor = tf.tensor2d(data, [data.length, 784]);
    
    // Normalize the data
    return tensor.div(tf.scalar(255));
  });
};
```

Con nuestro conjunto de datos cargado y nuestra función de conversión definida, estamos listos para entrenar nuestro modelo. Definiremos un modelo secuencial simple con dos capas densas:

```javascript
// Define a simple sequential model
const model = tf.sequential();
model.add(tf.layers.dense({ units: 784, activation: 'relu', inputShape: [784] }));
model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));
```

A continuación, compilaremos el modelo utilizando el optimizador de Adam y la función de pérdida de entropía cruzada categórica:

```javascript
// Compile the model
model.compile({
  optimizer: tf.train.adam(),
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy'],
});
```

Ahora estamos listos para entrenar el modelo. Usaremos el método fitDataset(), que toma un objeto tf.data.Dataset y entrena el modelo en el conjunto de datos:

```javascript
// Train the model
model.fitDataset(mnistData, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}, accuracy = ${logs.acc}`);
    },
  },
});
```

¡Eso es! Ahora hemos entrenado un modelo de aprendizaje automático simple con TensorFlow.js y Node.js Workers.

## Entrenando múltiples modelos en paralelo

En la sección anterior, vimos cómo usar TensorFlow.js con Node.js Workers para entrenar un solo modelo. Sin embargo, los trabajadores de Node.js también se pueden usar para entrenar varios modelos en paralelo.

Para hacer esto, primero necesitaremos crear un grupo de trabajadores. Podemos hacer esto con el complemento tf.js-node Worker:

```javascript
const { WorkerPool } = require('@tensorflow/tfjs-node');

// Create a Worker pool with two workers
const pool = new WorkerPool({ numWorkers: 2 });
```

Una vez que tenemos un grupo de trabajadores, podemos definir una función para entrenar un modelo en un conjunto de datos. Esta función tomará un conjunto de datos y un modelo, y devolverá una Promesa que se resuelve en el modelo entrenado:

```javascript
// Define a function to train a model on a dataset
const trainModel = (dataset, model) => {
  return new Promise((resolve, reject) => {
    // Use a tidy to clean up when we're done
    tf.tidy(() => {
      // Train the model
      model.fitDataset(dataset, {
        epochs: 10,
        callbacks: {
          onEpochEnd: (epoch, logs) => {
            console.log(`Epoch ${epoch}: loss = ${logs.loss}, accuracy = ${logs.acc}`);
          },
        },
      })
      .then(() => {
        // Resolve the promise with the trained model
        resolve(model);
      })
      .catch((err) => {
        // Reject the promise with the error
        reject(err);
      });
    });
  });
};
```

Con nuestra función trainModel() definida, ahora podemos entrenar varios modelos en paralelo. Haremos esto mapeando nuestra función trainModel() sobre una matriz de conjuntos de datos:

```javascript
// Create an array of datasets
const datasets = [
  tf.data.web('https://storage.googleapis.com/tfjs-examples/mnist_train_small.csv'),
  tf.data.web('https://storage.googleapis.com/tfjs-examples/mnist_test.csv'),
];

// Train multiple models in parallel
Promise.all(datasets.map((dataset) => {
  return trainModel(dataset, model);
}))
.then(() => {
  // All models have been trained
  console.log('All models have been trained');
})
.catch((err) => {
  // One or more models failed to train
  console.error(err);
});
```

En este código, usamos el método Promise.all() para entrenar varios modelos en paralelo. El método Promise.all() toma una matriz de Promises y devuelve una única Promise que se resuelve cuando se resuelven todas las Promises de la matriz.

## Terminando

En esta publicación, hemos visto cómo usar TensorFlow.js con Node.js Workers para entrenar modelos de aprendizaje automático. Hemos visto un ejemplo simple para comenzar y hemos visto cómo usar un grupo de Worker para entrenar varios modelos en paralelo.

Si está interesado en obtener más información sobre TensorFlow.js, asegúrese de consultar el sitio web de TensorFlow.js (https://js.tensorflow.org/) y los ejemplos de TensorFlow.js (https://github.com/). tensorflow/tfjs-ejemplos).