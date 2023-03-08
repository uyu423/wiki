---
title: 076: Uso de TensorFlow.js con Node.js en Edge Computing
description: 
published: true
date: 2023-02-03T00:37:57.430Z
tags: 
editor: markdown
dateCreated: 2023-02-03T00:37:55.801Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [076: Using TensorFlow.js with Node.js in Edge Computing***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/076-using-tensorflow-js-with-node-js-in-edge-computing)
{.links-list}


# Uso de TensorFlow.js con Node.js en Edge Computing

TensorFlow.js es una biblioteca de código abierto para el cálculo numérico mediante gráficos de flujo de datos. Se puede usar en Node.js para entrenar e implementar modelos de aprendizaje automático en dispositivos perimetrales.

En esta publicación, veremos cómo usar TensorFlow.js con Node.js para entrenar e implementar modelos de aprendizaje automático en dispositivos perimetrales.

## ¿Qué es TensorFlow.js?

TensorFlow.js es una biblioteca de código abierto para el cálculo numérico mediante gráficos de flujo de datos. TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático en el navegador y en Node.js.

TensorFlow.js fue desarrollado originalmente por el equipo de Google Brain para su uso con la plataforma de aprendizaje automático TensorFlow.

## ¿Qué es Node.js?

Node.js es un tiempo de ejecución de JavaScript basado en el motor de JavaScript V8 de Chrome. Node.js es un entorno de tiempo de ejecución multiplataforma de código abierto para desarrollar aplicaciones del lado del servidor.

Las aplicaciones de Node.js están escritas en JavaScript y se pueden ejecutar dentro del tiempo de ejecución de Node.js en OS X, Microsoft Windows, Linux y FreeBSD.

## Empezando

Para usar TensorFlow.js con Node.js, deberá instalar lo siguiente:

- Nodo.js
-TensorFlow.js

Puede instalar Node.js y TensorFlow.js usando los siguientes comandos:

```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
```

```
npm install @tensorflow/tfjs
```

## Hola Mundo

Comencemos por crear un programa simple "Hello World" usando TensorFlow.js y Node.js.

Cree un archivo llamado "hello-world.js" y agregue el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs');

tf.tensor([1, 2, 3, 4]).print();
```

Ejecute el programa usando el siguiente comando:

```
node hello-world.js
```

Debería ver el siguiente resultado:

```
Tensor
    [[1],
     [2],
     [3],
     [4]]
```

## Entrenamiento de un modelo de aprendizaje automático

Ahora que hemos visto cómo usar TensorFlow.js con Node.js, intentemos entrenar un modelo de aprendizaje automático simple.

Usaremos el conjunto de datos MNIST, que consta de 70 000 imágenes en escala de grises de dígitos escritos a mano. Las imágenes tienen un tamaño de 28x28 píxeles.

El conjunto de datos MNIST se divide en tres partes: 60 000 imágenes para entrenamiento, 10 000 imágenes para prueba y 10 000 imágenes para validación.

Usaremos la API de capas TensorFlow.js para construir nuestro modelo de aprendizaje automático. La API de capas es una API de alto nivel que facilita la construcción de redes neuronales.

Primero, necesitaremos cargar el conjunto de datos MNIST. Podemos hacer esto usando la API tf.data.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();
}

run();
```

A continuación, definiremos nuestro modelo de aprendizaje automático mediante la API tf.secuencial.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });
}

run();
```

Ahora que hemos definido nuestro modelo de aprendizaje automático, debemos entrenarlo. Podemos hacer esto usando la API tf.fit.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  return model.fit(images, labels, {
    batchSize,
    epochs
  });
}

run();
```

Una vez que nuestro modelo de aprendizaje automático está entrenado, podemos usarlo para hacer predicciones sobre nuevos datos.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  model.fit(images, labels, {
    batchSize,
    epochs
  });

  const testImages = images.slice(0, 1000);
  const testLabels = labels.slice(0, 1000);

  const accuracy = model.evaluate(testImages, testLabels);

  console.log('Accuracy:', accuracy[1]);
}

run();
```

## Implementación de un modelo de aprendizaje automático

Una vez que hemos entrenado nuestro modelo de aprendizaje automático, podemos implementarlo en un dispositivo perimetral para la inferencia.

Usaremos la API TensorFlow.js Node.js para implementar nuestro modelo de aprendizaje automático en un dispositivo perimetral. La API de Node.js es una API de bajo nivel que le permite ejecutar programas TensorFlow.js en Node.js.

Primero, necesitaremos convertir nuestro modelo de aprendizaje automático al formato TensorFlow.js Node.js. Podemos hacer esto usando la API tf.node.save.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  model.fit(images, labels, {
    batchSize,
    epochs
  });

  tf.node.save(model, 'model.json');
}

run();
```

Una vez que nuestro modelo de aprendizaje automático se convierte al formato TensorFlow.js Node.js, podemos implementarlo en un dispositivo perimetral.

Tendremos que instalar la API TensorFlow.js Node.js en nuestro dispositivo perimetral. Esto lo podemos hacer usando el siguiente comando:

```
npm install @tensorflow/tfjs-node
```

Ahora que la API TensorFlow.js Node.js está instalada, podemos usar la API tf.node.load para cargar nuestro modelo de aprendizaje automático.

```javascript
const tf = require('@tensorflow/tfjs-node');

async function run() {
  const model = await tf.node.load('model.json');
}

run();
```

Una vez que nuestro modelo de aprendizaje automático está cargado, podemos usarlo para hacer predicciones sobre nuevos datos.

```javascript
const tf = require('@tensorflow/tfjs-node');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  model.fit(images, labels, {
    batchSize,
    epochs
  });

  tf.node.save(model, 'model.json');

  const testImages = images.slice(0, 1000);
  const testLabels = labels.slice(0, 1000);

  const accuracy = model.evaluate(testImages, testLabels);

  console.log('Accuracy:', accuracy[1]);
}

run();
```

## Conclusión

En esta publicación, hemos visto cómo usar TensorFlow.js con Node.js para entrenar e implementar modelos de aprendizaje automático en dispositivos perimetrales.

TensorFlow.js es una poderosa biblioteca para computación numérica que se puede usar para entrenar e implementar modelos de aprendizaje automático en dispositivos perimetrales.

Node.js es un tiempo de ejecución de JavaScript que se puede usar para ejecutar programas TensorFlow.js en dispositivos perimetrales.

La API TensorFlow.js Node.js es una API de bajo nivel que le permite ejecutar programas TensorFlow.js en Node.js.

## Recursos

- [TensorFlow.js](https://js.tensorflow.org/)
- [Node.js](https://nodejs.org/en/)
- [Conjunto de datos MNIST](http://yann.lecun.com/exdb/mnist/)