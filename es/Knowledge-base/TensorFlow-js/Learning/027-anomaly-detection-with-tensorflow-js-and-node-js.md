---
title: 027: Detección de anomalías con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T13:17:49.078Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:17:47.456Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [027: Anomaly Detection with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/027-anomaly-detection-with-tensorflow-js-and-node-js)
{.links-list}


# Detección de anomalías con TensorFlow.js y Node.js

En esta publicación, veremos cómo crear modelos de detección de anomalías con TensorFlow.js y Node.js. Usaremos un conjunto de datos de lecturas diarias de temperatura de los últimos 140 años, que dividiremos en conjuntos de entrenamiento y prueba.

Usaremos la biblioteca TensorFlow.js para construir y entrenar nuestros modelos. TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. Node.js es un tiempo de ejecución de JavaScript que nos permite ejecutar código JavaScript fuera del navegador.

Usaremos la API del modelo secuencial de TensorFlow.js. Los modelos secuenciales son un tipo de red neuronal que se componen de una pila lineal de capas.

## Requisitos previos

Antes de comenzar, hay algunas cosas que necesitará:

- Un editor de texto. Recomiendo [Visual Studio Code](https://code.visualstudio.com/).
- [Node.js](https://nodejs.org/en/) instalado en su computadora.
- Una comprensión básica de JavaScript.

## Obtener los datos

El primer paso es obtener los datos. Usaremos un conjunto de datos de lecturas diarias de temperatura de los últimos 140 años. El conjunto de datos está disponible [aquí](https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data).

Descargue el conjunto de datos y descomprímalo. Ahora debería tener una carpeta llamada `GlobalLandTemperaturesByCountry`.

## Preparando los datos

El siguiente paso es preparar los datos. Tendremos que dividir el conjunto de datos en conjuntos de entrenamiento y prueba. También necesitaremos normalizar los datos, lo que significa escalar los datos para que estén entre 0 y 1.

Usaremos el paquete [`normalize-dataset`](https://www.npmjs.com/package/normalize-dataset) para ayudarnos con esto. Instálelo ejecutando el siguiente comando:

```
npm install --save normalize-dataset
```

Cree un nuevo archivo llamado `prepare-data.js` y agregue el siguiente código:

```javascript
const fs = require('fs');
const path = require('path');
const normalizeDataset = require('normalize-dataset');

const dataPath = path.join(__dirname, 'GlobalLandTemperaturesByCountry.csv');
const data = fs.readFileSync(dataPath, 'utf8');

// Split the data into training and testing sets
const [train, test] = normalizeDataset.splitDataset(data, 0.8);

// Save the training and testing sets to files
fs.writeFileSync(path.join(__dirname, 'train.csv'), train);
fs.writeFileSync(path.join(__dirname, 'test.csv'), test);
```

Ejecute el código ejecutando el siguiente comando:

```
node prepare-data.js
```

Ahora debería tener dos archivos nuevos en su proyecto: `train.csv` y `test.csv`. Estos son los conjuntos de entrenamiento y prueba que usaremos para entrenar y probar nuestros modelos.

## Construyendo el modelo

Ahora que tenemos nuestros datos, podemos comenzar a construir nuestro modelo. Usaremos la API del modelo secuencial de TensorFlow.js. Los modelos secuenciales son un tipo de red neuronal que se componen de una pila lineal de capas.

Cree un nuevo archivo llamado `model.js` y agregue el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs');

// Create a sequential model
const model = tf.sequential();

// Add a single hidden layer
model.add(tf.layers.dense({ units: 1, inputShape: [1] }));

// Add an output layer
model.add(tf.layers.dense({ units: 1, activation: 'sigmoid' }));

// Compile the model
model.compile({
  loss: 'binaryCrossentropy',
  optimizer: 'adam'
});

module.exports = model;
```

En el código anterior, hemos creado un modelo secuencial con una capa oculta y una capa de salida. También compilamos el modelo utilizando la función de pérdida `binaryCrossentropy` y el optimizador `adam`.

## Entrenamiento del modelo

Ahora que tenemos nuestro modelo, necesitamos entrenarlo. Haremos esto proporcionando al modelo el conjunto de entrenamiento que preparamos anteriormente.

Cree un nuevo archivo llamado `train.js` y agregue el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs');
const fs = require('fs');
const path = require('path');

const model = require('./model');

// Read the training set from a file
const trainPath = path.join(__dirname, 'train.csv');
const trainData = tf.data.csv(trainPath, {
  columnConfigs: {
    label: {
      isLabel: true
    }
  }
});

// Train the model
model.fitDataset(trainData, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    }
  }
});
```

En el código anterior, hemos leído el conjunto de entrenamiento de un archivo y lo hemos pasado a la función `fitDataset`. Esta función entrenará el modelo durante 10 épocas. Una época es una iteración sobre todo el conjunto de entrenamiento.

También hemos configurado la devolución de llamada `onEpochEnd` para registrar la pérdida después de cada época. La pérdida es una medida de qué tan bien está funcionando el modelo. Queremos que la pérdida sea lo más baja posible.

## Probando el modelo

Ahora que hemos entrenado nuestro modelo, necesitamos probarlo. Haremos esto proporcionando al modelo el conjunto de prueba que preparamos anteriormente.

Cree un nuevo archivo llamado `test.js` y agregue el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs');
const fs = require('fs');
const path = require('path');

const model = require('./model');

// Read the testing set from a file
const testPath = path.join(__dirname, 'test.csv');
const testData = tf.data.csv(testPath, {
  columnConfigs: {
    label: {
      isLabel: true
    }
  }
});

// Evaluate the model
model.evaluateDataset(testData).then(results => {
  console.log(`Loss: ${results.loss}`);
});
```

En el código anterior, hemos leído el conjunto de pruebas de un archivo y lo hemos pasado a la función `evaluateDataset`. Esta función evaluará el modelo y devolverá la pérdida.

## Conclusión

En esta publicación, hemos visto cómo crear modelos de detección de anomalías con TensorFlow.js y Node.js. Hemos preparado los datos, construido el modelo y entrenado y probado el modelo.