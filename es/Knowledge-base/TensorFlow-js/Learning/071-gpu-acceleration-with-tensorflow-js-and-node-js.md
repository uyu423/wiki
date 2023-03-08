---
title: 071: aceleración de GPU con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T20:24:33.649Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:24:31.993Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [071: GPU Acceleration with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/071-gpu-acceleration-with-tensorflow-js-and-node-js)
{.links-list}


# Aceleración de GPU con TensorFlow.js y Node.js

TensorFlow.js es una biblioteca de JavaScript potente y flexible para entrenar e implementar modelos de aprendizaje automático. Node.js es un tiempo de ejecución de JavaScript que permite secuencias de comandos del lado del servidor y aplicaciones de red rápidas.

Con TensorFlow.js y Node.js, puede entrenar e implementar modelos de aprendizaje automático en la web y en servidores Node.js. TensorFlow.js proporciona una API de JavaScript para entrenar e implementar modelos de aprendizaje automático en navegadores web y servidores Node.js. Node.js le permite ejecutar JavaScript en un servidor.

En esta publicación, le mostraremos cómo usar TensorFlow.js y Node.js para entrenar e implementar modelos de aprendizaje automático en la web y en servidores Node.js.

## Requisitos previos

Para seguir con esta publicación, necesitarás:

- Una computadora con un navegador web y conexión a Internet
- Un editor de texto
- Node.js instalado en su computadora

## Instalación de TensorFlow.js

Para instalar TensorFlow.js, puede usar el administrador de paquetes de Node.js (npm):

```
npm install @tensorflow/tfjs
```

## Hola, TensorFlow.js

Comencemos entrenando e implementando un modelo de aprendizaje automático simple con TensorFlow.js. Usaremos el conjunto de datos MNIST, que consta de imágenes de dígitos escritos a mano.

Primero, necesitaremos cargar el conjunto de datos MNIST. Podemos hacer esto con la clase de conjunto de datos TensorFlow.js MNIST:

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = new tf.MNISTDataset();
```

A continuación, necesitaremos entrenar un modelo de aprendizaje automático en el conjunto de datos MNIST. Usaremos un modelo de aprendizaje profundo llamado red neuronal convolucional (CNN). Una CNN es un tipo de red neuronal que está diseñada para trabajar con imágenes.

Podemos entrenar una CNN con la API de capas de TensorFlow.js:

```javascript
const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});
```

Ahora que tenemos un modelo de aprendizaje automático, podemos entrenarlo en el conjunto de datos MNIST. Usaremos la API de ajuste de TensorFlow.js para entrenar el modelo:

```javascript
const trainXs = mnistData.getTrainImagesAsTensors();
const trainYs = mnistData.getTrainLabelsAsTensors();

model.fit(trainXs, trainYs, {
  epochs: 10,
  batchSize: 64
});
```

Una vez que se ha entrenado el modelo, podemos evaluarlo en el conjunto de datos de prueba MNIST. Usaremos la API de evaluación de TensorFlow.js para evaluar el modelo:

```javascript
const testXs = mnistData.getTestImagesAsTensors();
const testYs = mnistData.getTestLabelsAsTensors();

model.evaluate(testXs, testYs);
```

La API de evaluación devolverá la pérdida y la precisión del modelo en el conjunto de datos de prueba.

## Implementación de un modelo TensorFlow.js

Una vez que se ha entrenado un modelo de aprendizaje automático, puede implementarlo en un servidor web o en un servidor Node.js.

Comenzaremos implementando el modelo en un servidor web. Podemos hacer esto con la API de conversión de modelos de TensorFlow.js:

```javascript
const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

const converter = tf.modelConverter.createConverter({
  from: 'tensorflowjs_layers_model'
});

const json = converter.toJSON(model);
```

La API del convertidor de modelos devolverá una representación JSON del modelo. Esta representación JSON se puede usar para implementar el modelo en un servidor web.

Para implementar el modelo en un servidor web, deberá crear un archivo HTML y un archivo JavaScript. El archivo HTML contendrá un elemento en el que se cargará el modelo TensorFlow.js. El archivo JavaScript contendrá el código para cargar el modelo en el elemento.

Aquí hay un archivo HTML de ejemplo:

```html
<html>
  <head>
    <title>TensorFlow.js MNIST Example</title>
  </head>
  <body>
    <h1>TensorFlow.js MNIST Example</h1>
    <div id="container"></div>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs"></script>
    <script src="mnist.js"></script>
  </body>
</html>
```

Y aquí hay un archivo JavaScript de ejemplo:

```javascript
const tf = require('@tensorflow/tfjs');

const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

const mnistData = new tf.MNISTDataset();

const testXs = mnistData.getTestImagesAsTensors();
const testYs = mnistData.getTestLabelsAsTensors();

model.evaluate(testXs, testYs);

const converter = tf.modelConverter.createConverter({
  from: 'tensorflowjs_layers_model'
});

const json = converter.toJSON(model);

tf.loadLayersModel('http://localhost:8080/model.json').then(function(model) {
  model.predict(testXs).then(function(predictions) {
    console.log(predictions);
  });
});
```

En el archivo HTML, hemos incluido el script TensorFlow.js y el script mnist.js. El script mnist.js contiene el código para cargar el modelo en el elemento con el id "contenedor".

Para ejecutar el archivo HTML, deberá iniciar un servidor web. Puede usar el módulo de servidor http de Node.js para iniciar un servidor web:

```
npm install http-server -g

http-server
```

El módulo del servidor http iniciará un servidor web en el puerto 8080. Puede acceder al archivo HTML en http://localhost:8080.

## Ejecutar un modelo TensorFlow.js en un servidor Node.js

También puede ejecutar un modelo TensorFlow.js en un servidor Node.js. Para hacer esto, deberá usar la API TensorFlow.js Node.js:

```javascript
const tf = require('@tensorflow/tfjs');

const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

const mnistData = new tf.MNISTDataset();

const testXs = mnistData.getTestImagesAsTensors();
const testYs = mnistData.getTestLabelsAsTensors();

model.evaluate(testXs, testYs);

const converter = tf.modelConverter.createConverter({
  from: 'tensorflowjs_layers_model'
});

const json = converter.toJSON(model);

tf.loadLayersModel('http://localhost:8080/model.json').then(function(model) {
  model.predict(testXs).then(function(predictions) {
    console.log(predictions);
  });
});
```

En el código anterior, cargamos el conjunto de datos MNIST y entrenamos un modelo de aprendizaje automático en él. Luego, convertimos el modelo en una representación JSON y lo cargamos en un servidor Node.js.

Para ejecutar el código anterior, deberá iniciar un servidor Node.js. Puede usar el módulo Node.js Express para iniciar un servidor Node.js:

```
npm install express -g

express
```

El módulo Express iniciará un servidor Node.js en el puerto 3000. Puede acceder al servidor en http://localhost:3000.

## Conclusión

En esta publicación, le mostramos cómo usar TensorFlow.js y Node.js para entrenar e implementar modelos de aprendizaje automático en la web y en servidores Node.js.

TensorFlow.js es una biblioteca de JavaScript potente y flexible para entrenar e implementar modelos de aprendizaje automático. Node.js es un tiempo de ejecución de JavaScript que permite secuencias de comandos del lado del servidor y aplicaciones de red rápidas.

Con TensorFlow.js y Node.js, puede entrenar e implementar modelos de aprendizaje automático en la web y en servidores Node.js. TensorFlow.js proporciona una API de JavaScript para entrenar e implementar modelos de aprendizaje automático en navegadores web y servidores Node.js. Node.js le permite ejecutar JavaScript en un servidor.