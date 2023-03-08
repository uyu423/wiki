---
title: 020: Análisis de sentimiento con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T11:36:30.927Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:36:29.274Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [020: Sentiment Analysis with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/020-sentiment-analysis-with-tensorflow-js-and-node-js)
{.links-list}


# 020: Análisis de sentimiento con TensorFlow.js y Node.js

## Introducción

En esta publicación, cubriremos cómo hacer un análisis de sentimiento con TensorFlow.js y Node.js. El análisis de sentimientos es un proceso de determinar computacionalmente si un escrito es positivo, negativo o neutral. A menudo se usa para medir la opinión pública en las redes sociales y tiene una amplia gama de otras aplicaciones.

Usaremos la biblioteca TensorFlow.js, que es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. TensorFlow.js se puede usar en un entorno Node.js, que usaremos para nuestro análisis de opiniones.

## Empezando

Antes de comenzar, hay algunas cosas que deberá configurar. En primer lugar, deberá tener instalado Node.js en su máquina. Puede descargarlo desde el [sitio web de Node.js] (https://nodejs.org/en/).

Una vez que haya instalado Node.js, deberá instalar la biblioteca TensorFlow.js. Puedes hacer esto con el siguiente comando:

```
npm install @tensorflow/tfjs
```

A continuación, deberá crear un nuevo archivo para nuestro programa de análisis de opiniones. Lo llamaremos `sentiment.js`. Puedes hacer esto con tu editor de texto favorito.

## Inicializar el entorno TensorFlow.js

Lo primero que debemos hacer en nuestro archivo `sentiment.js` es inicializar el entorno TensorFlow.js. Esto lo podemos hacer con el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs');
```

Esto cargará la biblioteca TensorFlow.js en nuestro programa para que podamos usarla.

## Cargando el conjunto de datos

Ahora que tenemos configurado el entorno TensorFlow.js, necesitamos cargar el conjunto de datos que usaremos para entrenar nuestro modelo de análisis de sentimiento. Usaremos el [conjunto de datos de reseñas de películas de IMDB](https://ai.stanford.edu/~amaas/data/sentiment/). Este conjunto de datos contiene 50 000 reseñas de películas, cada una con una etiqueta de 0 (negativa) o 1 (positiva).

Podemos cargar este conjunto de datos en nuestro programa con el siguiente código:

```javascript
const dataset = tf.data.csv('https://storage.googleapis.com/tfjs-datasets/imdb_reviews.csv');
```

Esto cargará el conjunto de datos en una variable `conjunto de datos`.

## Preprocesamiento del conjunto de datos

Antes de que podamos usar el conjunto de datos para el entrenamiento, debemos preprocesarlo. Esto implica dividir el conjunto de datos en conjuntos de entrenamiento y prueba, y convertir los datos de texto en vectores numéricos.

Esto lo podemos hacer con el siguiente código:

```javascript
const [train, test] = dataset.split(0.8);

const vectorizer = new tf.layers.Embedding(10000, 16);

const trainX = train.map(example => vectorizer.apply(example.text));
const testX = test.map(example => vectorizer.apply(example.text));
const trainY = train.map(example => example.label);
const testY = test.map(example => example.label);
```

Este código dividirá el conjunto de datos en conjuntos de entrenamiento y prueba, y luego vectorizará los datos de texto. Los datos vectorizados se almacenarán en las variables `trainX` y `testX` para los conjuntos de entrenamiento y prueba, respectivamente. Las etiquetas para los conjuntos de entrenamiento y prueba se almacenarán en las variables `trainY` y `testY`, respectivamente.

## Construyendo el modelo

Ahora que tenemos nuestro conjunto de datos preprocesado, podemos construir el modelo que usaremos para el análisis de sentimientos. Usaremos una red neuronal simple con una capa oculta.

Podemos construir el modelo con el siguiente código:

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({ units: 16, activation: 'relu', inputShape: [16] }));
model.add(tf.layers.dense({ units: 1, activation: 'sigmoid' }));
model.compile({ loss: 'binaryCrossentropy', optimizer: 'adam' });
```

Este código creará un nuevo modelo "secuencial" y luego agregará una capa oculta y una capa de salida al modelo. La capa oculta tendrá 16 unidades y la capa de salida tendrá una unidad. El modelo se compilará con la función de pérdida `binaryCrossentropy` y el optimizador `adam`.

## Entrenamiento del modelo

Ahora que tenemos nuestro modelo construido, podemos entrenarlo en nuestro conjunto de datos. Lo entrenaremos durante 10 épocas, lo que significa que el modelo verá los datos de entrenamiento 10 veces.

Podemos entrenar el modelo con el siguiente código:

```javascript
model.fit(trainX, trainY, { epochs: 10 })
  .then(() => {
    // evaluate the model on the test set
  });
```

Este código entrenará el modelo en el conjunto de entrenamiento y luego lo evaluará en el conjunto de prueba.

## Evaluación del modelo

Una vez que el modelo ha sido entrenado, podemos evaluar su desempeño en el conjunto de prueba. Usaremos el método `model.evaluate()` para hacer esto.

Podemos evaluar el modelo con el siguiente código:

```javascript
model.evaluate(testX, testY)
  .then(results => {
    // log the results
  });
```

Este código evaluará el modelo en el conjunto de prueba e imprimirá los resultados.

## Haciendo predicciones

Ahora que tenemos un modelo entrenado, podemos usarlo para hacer predicciones sobre nuevos datos. Para hacer esto, usaremos el método `model.predict()`.

Podemos hacer predicciones con el siguiente código:

```javascript
const prediction = model.predict(tf.tensor2d([[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16]]));
prediction.print();
```

Este código hará una predicción sobre los datos `[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16]`. El método `print()` imprimirá la predicción en la consola.

## Conclusión

En esta publicación, cubrimos cómo hacer un análisis de sentimiento con TensorFlow.js y Node.js. Cubrimos cómo cargar y preprocesar el conjunto de datos, construir el modelo, entrenar el modelo y hacer predicciones con el modelo.