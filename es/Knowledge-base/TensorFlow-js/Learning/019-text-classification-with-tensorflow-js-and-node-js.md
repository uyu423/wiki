---
title: 019: Clasificación de texto con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T11:19:05.726Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:19:04.021Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [019: Text Classification with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/019-text-classification-with-tensorflow-js-and-node-js)
{.links-list}


# Clasificación de texto con TensorFlow.js y Node.js

En esta publicación, aprenderemos cómo crear un modelo de clasificación de texto usando TensorFlow.js y Node.js. La clasificación de texto es una tarea común en el procesamiento del lenguaje natural, que es el proceso de analizar y trabajar con datos del lenguaje humano.

Usaremos un conjunto de datos de reseñas de películas del sitio web Rotten Tomatoes. El conjunto de datos contiene texto para cada reseña, así como una etiqueta que indica si la reseña es positiva o negativa. Usaremos este conjunto de datos para entrenar un modelo que pueda leer nuevas reseñas y predecir si son positivas o negativas.

## Requisitos previos

Antes de comenzar, hay algunas cosas que necesitará:

- Node.js y npm instalados en su computadora
- Un editor de texto o IDE
- Conocimientos básicos de JavaScript

## Empezando

Primero, necesitamos crear un nuevo proyecto Node.js. Cree un nuevo directorio para su proyecto e inicialícelo con npm:

```
mkdir text-classification
cd text-classification
npm init -y
```

Esto creará un archivo package.json para su proyecto. A continuación, necesitamos instalar las dependencias que usaremos. Usaremos TensorFlow.js, una biblioteca para trabajar con aprendizaje automático en JavaScript, y la biblioteca natural, que proporciona algunas funciones útiles para trabajar con datos de lenguaje humano.

```
npm install --save @tensorflow/tfjs natural
```

Con las dependencias instaladas, ahora podemos comenzar a codificar. Cree un nuevo archivo llamado index.js en el directorio de su proyecto y agregue el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here
```

Esto importa TensorFlow.js y las bibliotecas naturales, que usaremos en la siguiente sección.

## Preparando los datos

Antes de que podamos entrenar nuestro modelo, necesitamos preparar los datos. El conjunto de datos de reseñas de películas se encuentra en un archivo llamado reviews.csv, que puede [descargar aquí](https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv).

Agregue el siguiente código a index.js para cargar y preparar los datos:

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here

// Load the dataset
const csvUrl = 'https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv';
const { data, labels } = tf.data.csv(csvUrl);

// Shuffle the data
const shuffledData = data.shuffle();

// Split the data into training and test sets
const [trainData, testData] = shuffledData.split([0.8, 0.2]);

// Convert the labels to a one-hot encoding
const trainLabels = trainData.map((_, i) => labels[i]).oneHot(2);
const testLabels = testData.map((_, i) => labels[i]).oneHot(2);

// Normalize the data
const trainDataNormalized = trainData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

const testDataNormalized = testData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});
```

Echemos un vistazo a lo que hace este código:

- La primera línea carga el conjunto de datos desde una URL. Este conjunto de datos está en formato CSV, por lo que usamos la función tf.data.csv() para cargarlo.
- La segunda línea mezcla los datos. Esto es importante porque no queremos que el modelo aprenda el orden de las revisiones, solo las revisiones mismas.
- La tercera línea divide los datos en un conjunto de entrenamiento y un conjunto de prueba. El conjunto de entrenamiento se usa para entrenar el modelo y el conjunto de prueba se usa para evaluar el modelo.
- La cuarta línea convierte las etiquetas en una codificación one-hot. Esta es una forma común de representar datos categóricos en el aprendizaje automático.
- Las líneas quinta y sexta normalizan los datos. Este paso es importante porque garantiza que el modelo no se ajuste en exceso a los datos de entrenamiento.

## Construyendo el modelo

Ahora que tenemos los datos preparados, podemos construir el modelo. Usaremos un modelo de memoria bidireccional a largo y corto plazo (BiLSTM), que es un tipo de red neuronal recurrente (RNN).

Agregue el siguiente código a index.js para construir el modelo:

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here

// Load the dataset
const csvUrl = 'https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv';
const { data, labels } = tf.data.csv(csvUrl);

// Shuffle the data
const shuffledData = data.shuffle();

// Split the data into training and test sets
const [trainData, testData] = shuffledData.split([0.8, 0.2]);

// Convert the labels to a one-hot encoding
const trainLabels = trainData.map((_, i) => labels[i]).oneHot(2);
const testLabels = testData.map((_, i) => labels[i]).oneHot(2);

// Normalize the data
const trainDataNormalized = trainData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

const testDataNormalized = testData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

// Build the model
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 1000,
  outputDim: 32,
  inputLength: 100
}));
model.add(tf.layers.bidirectional({
  layer: tf.layers.lstm({
    units: 32
  })
}));
model.add(tf.layers.dense({
  units: 2,
  activation: 'softmax'
}));
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

// Train the model
model.fit(trainDataNormalized, trainLabels, {
  epochs: 5,
  validationData: [testDataNormalized, testLabels]
}).then(() => {
  // Evaluate the model
  const results = model.evaluate(testDataNormalized, testLabels);
  console.log(results);
});
```

Este código hace lo siguiente:

- La primera línea construye el modelo utilizando un modelo secuencial. Este es un tipo de modelo que consiste en una pila lineal de capas.
- La segunda línea agrega una capa de incrustación. Esta capa se utiliza para convertir los datos de entrada en una representación vectorial.
- La tercera línea agrega una capa Bidireccional. Esta capa se utiliza para procesar los datos en ambas direcciones.
- La cuarta línea agrega una capa de Memoria a corto plazo (LSTM). Esta capa se utiliza para recordar información durante largos períodos de tiempo.
- La quinta línea agrega una capa Densa. Esta capa se utiliza para hacer predicciones basadas en los datos.
- La sexta línea compila el modelo. Este paso configura el modelo para el entrenamiento.
- La séptima línea entrena al modelo. Este paso tardará unos minutos en completarse.
- La octava línea evalúa el modelo. Este paso imprime la precisión del modelo en la consola.

## Haciendo predicciones

Ahora que tenemos un modelo entrenado, podemos usarlo para hacer predicciones. Agrega el siguiente código a index.js para hacer predicciones:

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here

// Load the dataset
const csvUrl = 'https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv';
const { data, labels } = tf.data.csv(csvUrl);

// Shuffle the data
const shuffledData = data.shuffle();

// Split the data into training and test sets
const [trainData, testData] = shuffledData.split([0.8, 0.2]);

// Convert the labels to a one-hot encoding
const trainLabels = trainData.map((_, i) => labels[i]).oneHot(2);
const testLabels = testData.map((_, i) => labels[i]).oneHot(2);

// Normalize the data
const trainDataNormalized = trainData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

const testDataNormalized = testData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

// Build the model
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 1000,
  outputDim: 32,
  inputLength: 100
}));
model.add(tf.layers.bidirectional({
  layer: tf.layers.lstm({
    units: 32
  })
}));
model.add(tf.layers.dense({
  units: 2,
  activation: 'softmax'
}));
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

// Train the model
model.fit(trainDataNormalized, trainLabels, {
  epochs: 5,
  validationData: [testDataNormalized, testLabels]
}).then(() => {
  // Evaluate the model
  const results = model.evaluate(testDataNormalized, testLabels);
  console.log(results);
  
  // Make a prediction
  const prediction = model.predict(['this movie was great']);
  console.log(prediction);
});
```

Este código hace lo siguiente:

- La primera línea carga el conjunto de datos desde una URL. Este conjunto de datos está en formato CSV, por lo que usamos la función tf.data.csv() para cargarlo.
- La segunda línea mezcla los datos. Esto es importante porque no queremos que el modelo aprenda el orden de las revisiones, solo las revisiones mismas.
- La tercera línea divide los datos en un conjunto de entrenamiento y un conjunto de prueba. El conjunto de entrenamiento se usa para entrenar el modelo y el conjunto de prueba se usa para evaluar el modelo.
- La cuarta línea convierte las etiquetas en una codificación one-hot. Esta es una forma común de representar datos categóricos en el aprendizaje automático.
- Las líneas quinta y sexta normalizan los datos. Este paso es importante porque garantiza que el modelo no se ajuste en exceso a los datos de entrenamiento.
- La séptima línea construye el modelo utilizando un modelo secuencial. Este es un tipo de modelo que consiste en una pila lineal de capas.
- La octava línea agrega una capa de incrustación. Esta capa se utiliza para convertir los datos de entrada en una representación vectorial.
- La novena línea agrega una capa Bidireccional. Esta capa se utiliza para procesar los datos en ambas direcciones.
- La décima línea agrega una capa de Memoria a corto plazo (LSTM). Esta capa se utiliza para recordar información durante largos períodos de tiempo.
- La undécima línea agrega una capa Densa. Esta capa se utiliza para hacer predicciones basadas en los datos.
- La duodécima línea compila el modelo. Este paso configura el modelo para el entrenamiento.
- La decimotercera línea entrena al modelo. Este paso tardará unos minutos en completarse.
- La decimocuarta línea evalúa el modelo. Este paso imprime la precisión del modelo en la consola.
- La línea quince hace una predicción. Este paso imprime la predicción en la consola.

## Conclusión

En esta publicación, aprendimos cómo construir un modelo de clasificación de texto usando TensorFlow.js y Node.js. Comenzamos cargando y preparando los datos, luego construimos y entrenamos un modelo. Finalmente, usamos el modelo para hacer predicciones.

La clasificación de texto es una tarea común en el procesamiento del lenguaje natural, y esta publicación muestra cómo crear un modelo de clasificación de texto usando TensorFlow.js y Node.js.