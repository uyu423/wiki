---
title: 085: Creación de flujos de trabajo de aprendizaje automático de extremo a extremo con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T02:44:28.001Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:44:26.402Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [085: Building End-to-End Machine Learning Workflows with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/085-building-end-to-end-machine-learning-workflows-with-tensorflow-js-and-node-js)
{.links-list}


# 085: Creación de flujos de trabajo de aprendizaje automático de extremo a extremo con TensorFlow.js y Node.js

En esta publicación, veremos cómo crear flujos de trabajo de aprendizaje automático de extremo a extremo con TensorFlow.js y Node.js.

TensorFlow.js es un poderoso conjunto de herramientas para crear y entrenar modelos de aprendizaje automático en el navegador. Node.js es un tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript fuera del navegador.

Juntas, estas dos tecnologías le permiten crear flujos de trabajo completos de aprendizaje automático que se pueden implementar en cualquier lugar.

## Configuración de su entorno

Antes de sumergirnos en los detalles de cómo crear flujos de trabajo de aprendizaje automático de extremo a extremo, tomemos un momento para configurar nuestro entorno de desarrollo.

Deberá tener Node.js y npm instalados en su máquina. Puede encontrar instrucciones para hacerlo aquí:

https://nodejs.org/en/descargar/

Una vez que haya instalado Node.js y npm, puede instalar la herramienta CLI de TensorFlow.js ejecutando el siguiente comando:

```
npm install -g @tensorflow/tfjs-node
```

## Creando un nuevo proyecto

Ahora que tenemos nuestro entorno configurado, creemos un nuevo proyecto. Comenzaremos inicializando un nuevo proyecto npm:

```
npm init
```

Esto creará un archivo llamado `package.json` en el directorio de su proyecto. Este archivo contiene información sobre su proyecto, incluidas las dependencias que su proyecto necesita.

A continuación, instalaremos las dependencias de TensorFlow.js y Node.js que necesitaremos para nuestro proyecto:

```
npm install @tensorflow/tfjs @tensorflow/tfjs-node
```

## Construyendo un modelo de aprendizaje automático

Ahora que tenemos nuestro proyecto configurado, comencemos a construir nuestro modelo de aprendizaje automático.

Comenzaremos creando un archivo llamado `model.js` en nuestro directorio de proyectos. Este archivo contendrá el código para nuestro modelo de aprendizaje automático.

Primero, necesitaremos cargar las bibliotecas TensorFlow.js y Node.js que usaremos:

```javascript
const tf = require('@tensorflow/tfjs');
const fs = require('fs');
```

A continuación, definiremos algunas constantes que usaremos para configurar nuestro modelo:

```javascript
const MODEL_PATH = './model.json';
const INPUT_SHAPE = [28, 28, 1];
const NUM_CLASSES = 10;
```

La constante `MODEL_PATH` define la ruta al archivo que contendrá nuestro modelo entrenado. La constante `INPUT_SHAPE` define la forma de los datos de entrada en los que se entrenará nuestro modelo. La constante `NUM_CLASSES` define el número de clases de salida que nuestro modelo será entrenado para predecir.

A continuación, definiremos una función que construirá nuestro modelo de aprendizaje automático:

```javascript
function buildModel() {
  // We're building a simple machine learning model here
  const model = tf.sequential();
  
  // The first layer of our model is a convolutional layer
  model.add(tf.layers.conv2d({
    inputShape: INPUT_SHAPE,
    kernelSize: 3,
    filters: 16,
    activation: 'relu'
  }));
  
  // The second layer of our model is a pooling layer
  model.add(tf.layers.maxPooling2d({poolSize: 2, strides: 2}));
  
  // The third layer of our model is a flatten layer
  model.add(tf.layers.flatten());
  
  // The fourth layer of our model is a dense layer
  model.add(tf.layers.dense({units: NUM_CLASSES, activation: 'softmax'}));
  
  // We need to compile our model before we can train it
  model.compile({
    optimizer: tf.train.adam(),
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy']
  });
  
  return model;
}
```

Esta función define un modelo de aprendizaje automático simple que consta de cuatro capas:

- Una capa convolucional
- Una capa de agrupación
- Una capa plana
- Una capa densa

La capa convolucional es responsable de extraer características de los datos de entrada. La capa de agrupación es responsable de reducir la resolución de los datos. La capa flatten es responsable de aplanar los datos. La capa densa es responsable de mapear las características extraídas a las clases de salida.

Una vez que tenemos nuestro modelo definido, necesitamos compilarlo antes de poder entrenarlo. La compilación de un modelo configura el modelo para el entrenamiento. Necesitamos especificar el optimizador, la función de pérdida y las métricas que queremos usar.

En este caso, estamos usando el optimizador `adam`, la función de pérdida `categoricalCrossentropy` y la métrica `accuracy`.

## Entrenando al modelo

Ahora que tenemos nuestro modelo definido, vamos a entrenarlo. Comenzaremos cargando los datos de entrenamiento.

Los datos de entrenamiento se almacenan en el archivo `./data/train.csv`. Este archivo contiene imágenes de 28x28 de dígitos escritos a mano, junto con sus etiquetas.

Usaremos el módulo `fs` para leer el contenido de este archivo:

```javascript
const trainData = fs.readFileSync('./data/train.csv', {encoding: 'utf8'});
```

A continuación, analizaremos estos datos en una matriz de `tf.tensor`s:

```javascript
const trainTensors = tf.tensor2d(trainData.split('\n').map(row => row.split(',').map(Number)));
```

Ahora tenemos nuestros datos de entrenamiento cargados y listos para usar.

A continuación, definiremos una función que entrenará nuestro modelo:

```javascript
async function trainModel(model, trainTensors) {
  // We're training our model for 10 epochs
  const epochs = 10;
  
  // We're using a batch size of 32
  const batchSize = 32;
  
  // We're using the fit method to train our model
  await model.fit(trainTensors, {
    epochs: epochs,
    batchSize: batchSize
  });
}
```

Esta función entrena nuestro modelo durante 10 épocas utilizando un tamaño de lote de 32.

Una vez que nuestro modelo esté entrenado, lo guardaremos en el archivo `MODEL_PATH`:

```javascript
model.save(MODEL_PATH);
```

## Evaluando el modelo

Ahora que nuestro modelo está entrenado, vamos a evaluarlo. Comenzaremos cargando los datos de prueba.

Los datos de prueba se almacenan en el archivo `./data/test.csv`. Este archivo contiene imágenes de 28x28 de dígitos escritos a mano, junto con sus etiquetas.

Usaremos el módulo `fs` para leer el contenido de este archivo:

```javascript
const testData = fs.readFileSync('./data/test.csv', {encoding: 'utf8'});
```

A continuación, analizaremos estos datos en una matriz de `tf.tensor`s:

```javascript
const testTensors = tf.tensor2d(testData.split('\n').map(row => row.split(',').map(Number)));
```

Ahora tenemos nuestros datos de prueba cargados y listos para usar.

A continuación, definiremos una función que evaluará nuestro modelo:

```javascript
async function evaluateModel(model, testTensors) {
  // We're using the evaluate method to evaluate our model
  const results = await model.evaluate(testTensors);
  
  // We're logging the loss and accuracy of our model
  console.log(`loss: ${results[0]} - accuracy: ${results[1]}`);
}
```

Esta función evalúa nuestro modelo en los datos de prueba.

## Predecir con el modelo

Ahora que nuestro modelo está entrenado y evaluado, usémoslo para hacer predicciones.

Comenzaremos cargando la imagen sobre la que queremos hacer una predicción. La imagen se almacena en el archivo `./data/image.png`.

Usaremos el módulo `fs` para leer el contenido de este archivo:

```javascript
const imageData = fs.readFileSync('./data/image.png');
```

A continuación, analizaremos estos datos en un `tf.tensor`:

```javascript
const imageTensor = tf.tensor3d(imageData, [28, 28, 1]);
```

Ahora tenemos nuestros datos de imagen cargados y listos para usar.

A continuación, definiremos una función que hará una predicción usando nuestro modelo:

```javascript
async function predict(model, imageTensor) {
  // We're using the predict method to make a prediction
  const prediction = await model.predict(imageTensor);
  
  // We're logging the prediction that our model made
  console.log(prediction);
}
```

Esta función hace una predicción sobre los datos de la imagen.

## Conclusión

En esta publicación, hemos visto cómo crear flujos de trabajo de aprendizaje automático de extremo a extremo con TensorFlow.js y Node.js.

Hemos visto cómo configurar nuestro entorno de desarrollo, cómo crear un nuevo proyecto, cómo construir un modelo de aprendizaje automático, cómo entrenar el modelo, cómo evaluar el modelo y cómo usar el modelo para hacer predicciones.

Si está interesado en obtener más información sobre TensorFlow.js y Node.js, aquí hay algunos recursos que pueden resultarle útiles:

- La documentación de TensorFlow.js: https://js.tensorflow.org/
- La documentación de Node.js: https://nodejs.org/en/docs/