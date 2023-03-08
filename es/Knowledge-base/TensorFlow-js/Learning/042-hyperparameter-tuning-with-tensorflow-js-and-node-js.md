---
title: 042: Ajuste de hiperparámetros con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T16:44:18.750Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:44:14.181Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [042: Hyperparameter Tuning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/042-hyperparameter-tuning-with-tensorflow-js-and-node-js)
{.links-list}


# 042: Ajuste de hiperparámetros con TensorFlow.js y Node.js

En esta publicación, aprenderemos a usar TensorFlow.js y Node.js para el ajuste de hiperparámetros.

El ajuste de hiperparámetros es el proceso de optimizar un modelo de aprendizaje automático eligiendo los mejores valores para los hiperparámetros del modelo. El objetivo del ajuste de hiperparámetros es encontrar los valores de hiperparámetros que dan como resultado el mejor rendimiento del modelo en datos no vistos.

Hay algunas formas diferentes de abordar el ajuste de hiperparámetros. Un método popular es la búsqueda en cuadrícula, que implica buscar exhaustivamente los mejores valores de los hiperparámetros probando todas las combinaciones posibles de valores.

Otro método popular es la optimización bayesiana, que utiliza un modelo probabilístico para guiar la búsqueda de los mejores valores de los hiperparámetros.

En esta publicación, usaremos TensorFlow.js y Node.js para implementar un experimento simple de ajuste de hiperparámetros mediante la optimización bayesiana.

## Requisitos previos

Antes de comenzar, hay algunas cosas que deberá tener para seguir:

- Una comprensión básica del aprendizaje automático y cómo funciona.
- Un editor de texto o IDE
- Node.js instalado en su máquina

## Empezando

Comenzaremos creando un nuevo proyecto de Node.js. Cree un nuevo directorio para su proyecto e inicialícelo con npm:

```
mkdir hyperparameter-tuning
cd hyperparameter-tuning
npm init -y
```

A continuación, instalaremos las dependencias que necesitaremos para nuestro proyecto. Necesitaremos los paquetes [ BayesOptimization ](https://www.npmjs.com/package/bayesopt) y [ TensorFlow.js ](https://www.npmjs.com/package/@tensorflow/tfjs):

```
npm install --save bayesopt @tensorflow/tfjs
```

Con nuestras dependencias instaladas, ahora podemos crear nuestros archivos de proyecto. Cree un archivo llamado `index.js` en el directorio de su proyecto y agregue el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs');
const BayesOptimization = require('bayesopt');

// TODO: implement our hyperparameter tuning experiment
```

Comenzaremos requiriendo las dependencias que instalamos. También crearemos un comentario TODO para recordarnos dónde debemos implementar nuestro experimento de ajuste de hiperparámetros.

## Implementando el Experimento de Ajuste de Hiperparámetros

Ahora que tenemos nuestro proyecto configurado, podemos comenzar a implementar nuestro experimento de ajuste de hiperparámetros.

Comenzaremos definiendo los parámetros que queremos optimizar. Para este experimento, optimizaremos la tasa de aprendizaje y el tamaño del lote para un modelo de regresión lineal simple. También definiremos el rango de valores que queremos buscar para cada parámetro:

```javascript
const params = {
  learningRate: {
    type: 'float',
    min: 0.0001,
    max: 0.1
  },
  batchSize: {
    type: 'int',
    min: 1,
    max: 100
  }
};
```

A continuación, definiremos nuestra función objetivo. Esta es la función que vamos a optimizar. En este caso, queremos encontrar los valores de los hiperparámetros que dan como resultado el error más bajo en el conjunto de validación:

```javascript
const objective = (params, done) => {
  // TODO: implement our objective function
};
```

Implementaremos nuestra función objetivo en un momento. Por ahora, solo tenemos que definirlo.

Con nuestros parámetros y función objetivo definidos, ahora podemos crear nuestro objeto de optimización bayesiana:

```javascript
const bo = new BayesOptimization(params, objective);
```

Ahora podemos comenzar a optimizar nuestra función objetivo. Ejecutaremos nuestra optimización durante 20 iteraciones y usaremos la función de adquisición predeterminada (mejora esperada):

```javascript
bo.optimize(20, (err, result) => {
  if (err) {
    console.error(err);
  } else {
    console.log(result);
  }
});
```

Ahora podemos implementar nuestra función objetivo. Comenzaremos cargando el [conjunto de datos de viviendas de Boston] (https://archive.ics.uci.edu/ml/datasets/Housing) y dividiéndolo en conjuntos de entrenamiento y validación:

```javascript
const loadData = () =>
  tf.data.csv('https://archive.ics.uci.edu/ml/machine-learning-databases/housing/housing.data', {
    columnConfigs: {
      medv: {
        isLabel: true
      }
    }
  });

const splitData = (data) =>
  data.shuffle().splitBatch(0.2);
```

A continuación, definiremos nuestro modelo de regresión lineal:

```javascript
const createModel = () =>
  tf.sequential({
    layers: [
      tf.layers.dense({ inputShape: [13], units: 1 })
    ]
  });
```

Ahora podemos implementar nuestra función objetivo. Comenzaremos obteniendo los valores de los hiperparámetros del objeto `params`:

```javascript
const objective = (params, done) => {
  const learningRate = params.learningRate;
  const batchSize = params.batchSize;
  // TODO: implement our objective function
};
```

A continuación, cargaremos los datos y los dividiremos en conjuntos de entrenamiento y validación:

```javascript
const objective = (params, done) => {
  const learningRate = params.learningRate;
  const batchSize = params.batchSize;

  loadData()
    .then(splitData)
    .then(([train, val]) => {
      // TODO: implement our objective function
    });
};
```

Ahora podemos crear nuestro modelo y compilarlo con los hiperparámetros que estamos optimizando:

```javascript
const objective = (params, done) => {
  const learningRate = params.learningRate;
  const batchSize = params.batchSize;

  loadData()
    .then(splitData)
    .then(([train, val]) => {
      const model = createModel();
      model.compile({
        loss: 'meanSquaredError',
        optimizer: tf.train.sgd(learningRate)
      });
      // TODO: implement our objective function
    });
};
```

Finalmente, podemos entrenar nuestro modelo y evaluarlo en el conjunto de validación. Calcularemos el error cuadrático medio en el conjunto de validación y lo devolveremos como el valor de nuestra función objetivo:

```javascript
const objective = (params, done) => {
  const learningRate = params.learningRate;
  const batchSize = params.batchSize;

  loadData()
    .then(splitData)
    .then(([train, val]) => {
      const model = createModel();
      model.compile({
        loss: 'meanSquaredError',
        optimizer: tf.train.sgd(learningRate)
      });

      model.fit(train, {
        epochs: 10,
        batchSize: batchSize,
        validationData: val,
        callbacks: {
          onEpochEnd: (epoch, logs) => {
            console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
          }
        }
      })
        .then(() => {
          const valLoss = model.evaluate(val);
          console.log(`Validation loss: ${valLoss}`);
          done(null, valLoss);
        });
    });
};
```

¡Eso es! Ahora implementamos un experimento simple de ajuste de hiperparámetros usando TensorFlow.js y Node.js.

## Conclusión

En esta publicación, aprendimos a usar TensorFlow.js y Node.js para el ajuste de hiperparámetros. Hemos implementado un experimento simple de ajuste de hiperparámetros utilizando la optimización bayesiana.

Hay mucho más en el ajuste de hiperparámetros que lo que hemos cubierto en esta publicación. Si está interesado en obtener más información, le recomiendo consultar los siguientes recursos:

- [Optimización de hiperparámetros en aprendizaje automático](https://towardsdatascience.com/hyperparameter-optimization-in-machine-learning-part-1-of-4-cca2b1c265a2)
- [Un enfoque bayesiano para el ajuste de hiperparámetros](https://towardsdatascience.com/a-bayesian-approach-to-hyperparameter-tuning-part-1-of-3-c8f8e527e97b)
- [Ajuste de hiperparámetros con TensorFlow](https://medium.com/tensorflow/hyperparameter-tuning-with-tensorflow-part-1-fae4f2bae5e1)