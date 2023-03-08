---
title: 021: Reconocimiento de entidad con nombre (NER) con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T11:43:40.741Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:43:39.131Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [021: Named Entity Recognition (NER) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/021-named-entity-recognition-ner-with-tensorflow-js-and-node-js)
{.links-list}


# Reconocimiento de entidad nombrada (NER) con TensorFlow.js y Node.js

En esta publicación, veremos cómo realizar el reconocimiento de entidades nombradas (NER) en JavaScript usando TensorFlow.js y Node.js. NER es una tarea en el procesamiento del lenguaje natural (NLP) que implica identificar y clasificar entidades nombradas en el texto, como personas, lugares, organizaciones, etc.

Usaremos un modelo pre-entrenado que fue entrenado en el conjunto de datos NER CoNLL 2003. El modelo es un modelo de memoria bidireccional a largo plazo a corto plazo (BiLSTM) con una capa de campo aleatorio condicional (CRF) en la parte superior.

## Requisitos previos

Para seguir esta publicación, necesitará lo siguiente:

- Node.js (versión 8 o superior)
- Un editor de texto o IDE

## Empezando

Primero, creemos un nuevo proyecto Node.js. Usaremos el marco web Express, por lo que también necesitaremos instalarlo:

```
npm init
npm install --save express
```

A continuación, necesitaremos instalar el modelo NER de TensorFlow.js. Podemos hacerlo con el siguiente comando:

```
npm install @tensorflow-models/ner
```

Con eso, ¡estamos listos para comenzar a codificar!

## Cargando el modelo

Lo primero que tenemos que hacer es cargar el modelo. Podemos hacerlo con el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs-node');
const model = require('@tensorflow-models/ner');

async function main() {
  const ner = await model.load();
}

main();
```

En el código anterior, primero importamos TensorFlow.js y el modelo NER. Luego creamos una función asíncrona que cargará el modelo y lo almacenará en una variable.

## Predicción de entidades con nombre

Ahora que hemos cargado el modelo, podemos usarlo para predecir entidades con nombre en el texto. Podemos hacerlo con el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs-node');
const model = require('@tensorflow-models/ner');

async function main() {
  const ner = await model.load();

  const text = 'John Smith is a software engineer at Google.';

  const results = await ner.predict(text);

  console.log(results);
}

main();
```

En el código anterior, hemos agregado una cadena de texto para la que queremos predecir las entidades nombradas. Luego usamos el método `predecir` del modelo para obtener los resultados.

Los resultados serán una matriz de objetos, cada uno de los cuales representa una entidad con nombre. Cada objeto tendrá una propiedad `start` y `end` que representa los índices de inicio y finalización de la entidad nombrada en el texto de entrada, así como una propiedad `score` que representa la confianza del modelo en la predicción.

## Visualizando los resultados

Puede ser útil visualizar los resultados de la predicción. Podemos hacerlo con el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs-node');
const model = require('@tensorflow-models/ner');

async function main() {
  const ner = await model.load();

  const text = 'John Smith is a software engineer at Google.';

  const results = await ner.predict(text);

  for (const result of results) {
    console.log(
        `${text.substring(result.start, result.end)} (${result.score})`);
  }
}

main();
```

En el código anterior, agregamos un ciclo que imprimirá cada una de las entidades nombradas, así como también el puntaje de confianza del modelo para esa predicción.

## Conclusión

En esta publicación, hemos visto cómo realizar el reconocimiento de entidades con nombre en JavaScript usando TensorFlow.js y Node.js. También hemos visto cómo visualizar los resultados de la predicción.

Si está interesado en obtener más información sobre NER o TensorFlow.js, aquí hay algunos recursos que pueden resultarle útiles:

- [Reconocimiento de entidad nombrada con TensorFlow (publicación de blog)](https://blog.tensorflow.org/2018/12/named-entity-recognition-ner-tensorflow.html)
- [Modelo NER de TensorFlow.js](https://js.tensorflow.org/tutorials/tensorflow-for-js-nerds.html)
- [Conjunto de datos NER CoNLL 2003] (https://www.clips.uantwerpen.be/conll2003/ner/)