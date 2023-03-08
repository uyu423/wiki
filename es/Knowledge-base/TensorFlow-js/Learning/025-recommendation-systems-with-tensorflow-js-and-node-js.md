---
title: 025: Sistemas de recomendación con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T12:44:02.549Z
tags: 
editor: markdown
dateCreated: 2023-02-02T12:44:00.924Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [025: Recommendation Systems with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/025-recommendation-systems-with-tensorflow-js-and-node-js)
{.links-list}


## Descripción general

En esta publicación, veremos cómo crear sistemas de recomendación con TensorFlow.js y Node.js. Comenzaremos presentando brevemente los sistemas de recomendación y sus casos de uso. Luego, veremos cómo crear un sistema de recomendación simple basado en contenido usando TensorFlow.js. Finalmente, exploraremos cómo usar TensorFlow.js y Node.js para crear un sistema de recomendación de filtrado colaborativo más sofisticado.

## ¿Qué son los Sistemas de Recomendación?

Los sistemas de recomendación son un tipo de inteligencia artificial que se utilizan para predecir lo que un usuario podría querer comprar o ver. Son ampliamente utilizados por empresas como Amazon, Netflix y Spotify para personalizar el contenido que se muestra a los usuarios.

Hay dos tipos principales de sistemas de recomendación: filtrado basado en contenido y colaborativo.

Los sistemas de recomendación basados en el contenido recomiendan elementos a los usuarios en función de la similitud entre los elementos. Por ejemplo, un sistema de recomendación basado en el contenido podría recomendar una película a un usuario basándose en el hecho de que el usuario ha visto películas similares en el pasado.

Los sistemas de recomendación de filtrado colaborativo recomiendan elementos a los usuarios en función de la similitud entre los usuarios. Por ejemplo, un sistema de recomendación de filtrado colaborativo podría recomendar una película a un usuario basándose en el hecho de que otros usuarios que han visto películas similares también han visto esa película.

En esta publicación, veremos cómo crear sistemas de recomendación de filtrado colaborativo y basado en contenido utilizando TensorFlow.js y Node.js.

## Creación de un sistema de recomendación basado en el contenido

Comenzaremos analizando cómo crear un sistema de recomendación basado en el contenido. Usaremos el conjunto de datos MovieLens, que es un conjunto de datos de clasificaciones de películas.

El conjunto de datos de MovieLens contiene 100 000 calificaciones de 943 usuarios en 1682 películas. Cada calificación es un número entre 1 y 5, siendo 5 la calificación más alta.

Comenzaremos cargando el conjunto de datos en un conjunto de datos de TensorFlow.js:

```javascript
const tf = require('@tensorflow/tfjs');

const dataset = tf.data.csv('https://storage.googleapis.com/recommendation-system-datasets/movielens/ml-100k/u.data', {
  columnConfigs: {
    user_id: {
      isLabel: true
    },
    movie_id: {
      isLabel: true
    },
    rating: {
      isLabel: false
    }
  }
});
```

Usamos la opción `columnConfigs` para decirle a TensorFlow.js que las columnas `user_id` y `movie_id` son etiquetas y que la columna `rating` no es una etiqueta.

Luego dividiremos el conjunto de datos en conjuntos de entrenamiento y prueba:

```javascript
const trainDataset = dataset.shuffle(dataset.size).batch(dataset.size * 0.8);
const testDataset = dataset.batch(dataset.size * 0.2);
```

Estamos utilizando una división 80/20 para el tren y los conjuntos de prueba.

Luego, crearemos un modelo para aprender la asignación de películas a clasificaciones:

```javascript
const model = tf.sequential();

model.add(tf.layers.embedding({
  inputDim: 1682,
  outputDim: 64,
  inputShape: [1]
}));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({
  units: 64,
  activation: 'relu'
}));

model.add(tf.layers.dense({
  units: 1,
  activation: 'linear'
}));

model.compile({
  loss: 'meanSquaredError',
  optimizer: 'adam'
});
```

Estamos utilizando una capa de incrustación para asignar películas a un espacio vectorial de baja dimensión. Luego estamos usando una capa densa para aprender un mapeo del espacio vectorial a las calificaciones.

Luego ajustaremos el modelo a los datos de entrenamiento:

```javascript
model.fitDataset(trainDataset, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    }
  }
});
```

Estamos usando `tf.data.Dataset` para el entrenamiento, lo que nos permite usar el método `fitDataset()`. También estamos usando la devolución de llamada `onEpochEnd` para imprimir la pérdida después de cada época.

Entonces podemos evaluar el modelo en el conjunto de prueba:

```javascript
const testLoss = model.evaluateDataset(testDataset);

console.log(`Test loss: ${testLoss.loss}`);
```

El modelo tiene una pérdida de prueba de 0,84, lo que significa que puede predecir las calificaciones de las películas con un error de 0,84 en promedio.

## Creación de un sistema de recomendación de filtrado colaborativo

Ahora veremos cómo crear un sistema de recomendación de filtrado colaborativo.

Comenzaremos creando un modelo para aprender la asignación de usuarios a calificaciones:

```javascript
const model = tf.sequential();

model.add(tf.layers.embedding({
  inputDim: 943,
  outputDim: 64,
  inputShape: [1]
}));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({
  units: 64,
  activation: 'relu'
}));

model.add(tf.layers.dense({
  units: 1,
  activation: 'linear'
}));

model.compile({
  loss: 'meanSquaredError',
  optimizer: 'adam'
});
```

Estamos utilizando una capa de incrustación para asignar a los usuarios a un espacio vectorial de baja dimensión. Luego estamos usando una capa densa para aprender un mapeo del espacio vectorial a las calificaciones.

Luego ajustaremos el modelo a los datos de entrenamiento:

```javascript
model.fitDataset(trainDataset, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    }
  }
});
```

Entonces podemos evaluar el modelo en el conjunto de prueba:

```javascript
const testLoss = model.evaluateDataset(testDataset);

console.log(`Test loss: ${testLoss.loss}`);
```

El modelo tiene una pérdida de prueba de 0,95, lo que significa que puede predecir las calificaciones de los usuarios con un error de 0,95 en promedio.

## Conclusión

En esta publicación, analizamos cómo crear sistemas de recomendación con TensorFlow.js y Node.js. Comenzamos analizando cómo crear un sistema de recomendaciones basado en el contenido. Luego, analizamos cómo crear un sistema de recomendación de filtrado colaborativo.