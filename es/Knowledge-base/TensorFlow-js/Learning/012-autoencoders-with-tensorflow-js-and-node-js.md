---
title: 012: Codificadores automáticos con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T09:36:40.398Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:36:38.732Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [012: Autoencoders with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/012-autoencoders-with-tensorflow-js-and-node-js)
{.links-list}


# Codificadores automáticos con TensorFlow.js y Node.js

El aprendizaje profundo es una herramienta poderosa para aprender representaciones complejas de datos. Un autocodificador es un tipo de red neuronal que se puede utilizar para aprender estas representaciones sin supervisión.

En esta publicación, usaremos TensorFlow.js y Node.js para crear un codificador automático simple. Usaremos el conjunto de datos MNIST, que consta de imágenes de dígitos escritos a mano.

## Empezando

Primero, necesitamos instalar las dependencias. Usaremos las siguientes bibliotecas:

* [TensorFlow.js](https://www.tensorflow.org/js)
* [mnist](https://www.npmjs.com/package/mnist)

Puede instalarlos usando npm:

```
npm install tensorflowjs mnist
```

A continuación, necesitamos cargar el conjunto de datos MNIST. Usaremos la biblioteca mnist para hacer esto:

```javascript
const mnist = require('mnist');

// Load the dataset
const dataset = mnist.set(0.7, 0.3);

// Get the training and test sets
const [train, test] = dataset.getTrainingAndTestSets();
```

El conjunto de datos MNIST consta de imágenes de dígitos escritos a mano, cada uno de los cuales tiene 28x28 píxeles. Tendremos que aplanar estas imágenes en vectores de tamaño 784 antes de poder usarlas como entrada para nuestro codificador automático.

```javascript
// Flatten the images into vectors
const trainX = train.map(example => example.input);
const testX = test.map(example => example.input);
```

## Construyendo el codificador automático

Ahora que tenemos el conjunto de datos, podemos comenzar a construir el codificador automático. Usaremos una red neuronal completamente conectada con una capa oculta. La capa oculta tendrá un número menor de unidades que la capa de entrada, lo que obligará a la red a aprender una representación comprimida de los datos.

```javascript
// Create the model
const model = tf.sequential();

// Add the input layer
model.add(tf.layers.dense({
  inputShape: [784],
  units: 64
}));

// Add the hidden layer
model.add(tf.layers.dense({
  units: 32
}));

// Add the output layer
model.add(tf.layers.dense({
  units: 784
}));
```

Necesitamos especificar un optimizador y una función de pérdida para el modelo. Usaremos el optimizador de Adam y la función de pérdida del error cuadrático medio (MSE).

```javascript
// Compile the model
model.compile({
  optimizer: 'adam',
  loss: 'meanSquaredError'
});
```

## Entrenamiento del codificador automático

Ahora que tenemos el modelo, podemos entrenarlo en el conjunto de entrenamiento. Entrenaremos el modelo durante 20 épocas.

```javascript
// Train the model
model.fit(tf.tensor2d(trainX), tf.tensor2d(trainX), {
  epochs: 20
}).then(() => {
  // Evaluate the model on the test set
  model.evaluate(tf.tensor2d(testX), tf.tensor2d(testX));
});
```

## Visualizando los resultados

Para visualizar los resultados del entrenamiento, podemos usar la biblioteca `tensorflow-vis` para trazar las imágenes reconstruidas.

```javascript
// Install the library
npm install @tensorflow/tfjs-vis

// Load the library
const tfvis = require('@tensorflow/tfjs-vis');

// Plot the results
tfvis.show.image3d(
  model.predict(tf.tensor2d(testX)),
  {
    width: 28,
    height: 28
  }
);
```

## Conclusión

En esta publicación, hemos visto cómo usar TensorFlow.js y Node.js para crear un codificador automático simple. También hemos visto cómo entrenar el codificador automático y visualizar los resultados.

Los codificadores automáticos se pueden usar para una variedad de tareas, como la reducción de dimensionalidad, la eliminación de ruido y el modelado generativo. Si está interesado en obtener más información sobre los codificadores automáticos, le recomiendo los siguientes recursos:

* [Aprendizaje profundo 101: Introducción a los codificadores automáticos] (https://towardsdatascience.com/deep-learning-101-introduction-to-autoencoders-3e44bffe2b7d)
* [Codificadores automáticos](http://cs.stanford.edu/people/karpathy/convnetjs/demo/autoencoder.html)
* [Codificadores automáticos variacionales](https://jmetzen.github.io/2015-11-27/vae.html)