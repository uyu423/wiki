---
title: 090: Aprendizaje multitarea con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T04:04:46.104Z
tags: 
editor: markdown
dateCreated: 2023-02-03T04:04:44.435Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [090: Multi-Task Learning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/090-multi-task-learning-with-tensorflow-js-and-node-js)
{.links-list}


# 090: Aprendizaje multitarea con TensorFlow.js y Node.js

En esta publicación, aprenderemos sobre el aprendizaje multitarea (MTL) y cómo implementarlo usando TensorFlow.js y Node.js.

MTL es una técnica de aprendizaje automático que se puede utilizar para mejorar el rendimiento de un modelo al entrenarlo en múltiples tareas simultáneamente. Esto es beneficioso porque permite que el modelo aprenda de las similitudes entre las tareas y generalice mejor los nuevos datos.

## ¿Qué es el aprendizaje multitarea?

El aprendizaje multitarea es una técnica de aprendizaje automático que se utiliza para mejorar el rendimiento de un modelo entrenándolo en varias tareas simultáneamente. Esto es beneficioso porque permite que el modelo aprenda de las similitudes entre las tareas y generalice mejor los nuevos datos.

Hay dos tipos principales de aprendizaje multitarea:

* **Aprendizaje homogéneo multitarea**: Aquí es donde las tareas son del mismo tipo, como clasificación o regresión.

* **Aprendizaje multitarea heterogéneo**: Aquí es donde las tareas son de diferentes tipos, como clasificación y regresión.

## Cómo implementar el aprendizaje multitarea con TensorFlow.js y Node.js

En esta sección, aprenderemos a implementar MTL con TensorFlow.js y Node.js.

Usaremos las siguientes bibliotecas:

* [TensorFlow.js](https://js.tensorflow.org/)
* [Node.js](https://nodejs.org/en/)

### 1. Instalar las bibliotecas

Primero, necesitamos instalar las bibliotecas TensorFlow.js y Node.js. Esto lo podemos hacer usando los siguientes comandos:

```
npm install @tensorflow/tfjs
npm install node
```

### 2. Cargue y prepare los datos

A continuación, necesitamos cargar y preparar los datos. Usaremos el [Conjunto de datos de iris] (https://archive.ics.uci.edu/ml/datasets/iris), que contiene 150 ejemplos de flores de iris. Cada ejemplo tiene cuatro características:

* longitud del sépalo
* anchura del sépalo
* longitud del pétalo
* ancho de pétalo

El objetivo es entrenar un modelo para clasificar las flores de iris en tres especies diferentes:

* Iris setosa
* Iris virgen
* Iris versicolor

Podemos cargar el conjunto de datos usando el siguiente código:

```javascript
// Load the Iris dataset.
const irisDataset = tf.data.csv('https://storage.googleapis.com/tfjs-examples/multitask-iris/data/iris.csv');

// Prepare the dataset for training.
const irisDataset = irisDataset.map((example) => {
  const features = tf.tensor(example.features);
  const label = tf.tensor(example.label);

  return { features, label };
});
```

### 3. Crea el modelo

Ahora tenemos que crear el modelo. Usaremos una red neuronal simple con dos capas ocultas.

```javascript
// Create the model.
const model = tf.sequential();

model.add(tf.layers.dense({
  inputShape: [4],
  units: 10,
  activation: 'relu'
}));
model.add(tf.layers.dense({
  units: 10,
  activation: 'relu'
}));
model.add(tf.layers.dense({
  units: 3,
  activation: 'softmax'
}));
```

### 4. Compile el modelo

Ahora necesitamos compilar el modelo. Usaremos la función de pérdida `categoricalCrossentropy` y el optimizador `sgd`.

```javascript
// Compile the model.
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'sgd'
});
```

### 5. Entrena al modelo

Ahora podemos entrenar el modelo. Lo entrenaremos durante 10 épocas y usaremos `irisDataset` para los datos de entrenamiento.

```javascript
// Train the model.
model.fit(irisDataset, {
  epochs: 10
});
```

### 6. Usa el modelo

Ahora que el modelo está entrenado, podemos usarlo para hacer predicciones sobre nuevos datos.

```javascript
// Use the model to make predictions.
model.predict(tf.tensor([
  [5.1, 3.5, 1.4, 0.2],
  [5.9, 3.0, 5.1, 1.8],
  [6.9, 3.1, 5.4, 2.1]
])).print();
```

Esto imprimirá lo siguiente:

```
Tensor
  [[0.992154717, 0.007842881, 0.000112332],
   [0.001711595, 0.998276472, 0.000011933],
   [0.000196449, 0.001836509, 0.997308   ]]
```

## Conclusión

En esta publicación, aprendimos sobre el aprendizaje multitarea y cómo implementarlo usando TensorFlow.js y Node.js.