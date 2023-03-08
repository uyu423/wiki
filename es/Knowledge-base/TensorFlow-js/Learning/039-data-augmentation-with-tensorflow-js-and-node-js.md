---
title: 039: Aumento de datos con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T16:04:31.586Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:04:29.954Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [039: Data Augmentation with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/039-data-augmentation-with-tensorflow-js-and-node-js)
{.links-list}


# Aumento de datos con TensorFlow.js y Node.js

## Introducción

El aumento de datos es una técnica utilizada para aumentar artificialmente el tamaño de un conjunto de datos mediante la generación de nuevas muestras de datos a partir de las existentes. Esto es especialmente útil cuando el conjunto de datos original es pequeño y desea entrenar un modelo de aprendizaje automático con la mayor cantidad de datos posible.

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. Node.js es un entorno de tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript fuera de un navegador web.

En esta publicación, aprenderemos a usar TensorFlow.js y Node.js para realizar el aumento de datos. Comenzaremos analizando qué es el aumento de datos y por qué es útil. Luego veremos cómo implementar el aumento de datos en TensorFlow.js. Finalmente, aprenderemos a usar Node.js para ejecutar nuestro código de aumento de datos.

## ¿Qué es el aumento de datos?

El aumento de datos es una técnica utilizada para aumentar artificialmente el tamaño de un conjunto de datos mediante la generación de nuevas muestras de datos a partir de las existentes. Esto es especialmente útil cuando el conjunto de datos original es pequeño y desea entrenar un modelo de aprendizaje automático con la mayor cantidad de datos posible.

El aumento de datos funciona aplicando un conjunto de transformaciones a las muestras de datos existentes. Las muestras transformadas se utilizan luego como nuevas muestras de datos. Por ejemplo, si tenemos un conjunto de datos de imágenes, podemos realizar un aumento de datos aplicando transformaciones como rotación, recorte y volteo de las imágenes. Esto generará nuevas imágenes que se pueden usar como parte del conjunto de datos.

El beneficio del aumento de datos es que puede ayudar a mejorar el rendimiento de los modelos de aprendizaje automático. Esto se debe a que el conjunto de datos aumentado es más grande y contiene más variedad que el conjunto de datos original. Esto puede ayudar al modelo a aprender patrones más generalizables.

## Aumento de datos en TensorFlow.js

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. Se puede usar en el navegador o en un entorno Node.js.

El aumento de datos se puede realizar en TensorFlow.js usando la API `tf.data.Dataset`. Esta API le permite aplicar transformaciones a un conjunto de datos. El módulo `tf.image` contiene un conjunto de funciones que se pueden usar para realizar el aumento de imágenes.

Para usar el aumento de datos en TensorFlow.js, primero debemos crear un objeto `tf.data.Dataset`. Luego podemos aplicar transformaciones a este conjunto de datos usando el módulo `tf.image`. Finalmente, podemos usar el método `.forEachAsync()` para ejecutar el código de aumento en cada muestra de datos.

## Nodo.js

Node.js es un entorno de tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript fuera de un navegador web. Se puede utilizar para crear aplicaciones del lado del servidor.

Node.js viene con un conjunto de módulos integrados que se pueden usar para realizar varias tareas. Para el aumento de datos, usaremos el módulo `fs`, que nos permite leer y escribir archivos.

## Ejemplo

En este ejemplo, usaremos el conjunto de datos MNIST. Este conjunto de datos contiene imágenes de dígitos escritos a mano. Usaremos el módulo `tf.image` para realizar el aumento de datos en este conjunto de datos.

Primero, necesitaremos cargar el conjunto de datos MNIST. Podemos hacer esto usando el módulo `fs`.


```javascript
var fs = require('fs');

var mnistData = fs.readFileSync('mnist.csv', {encoding: 'utf-8'});
```

A continuación, necesitaremos analizar los datos de MNIST. Podemos hacer esto usando el módulo `tf.data.csv`.


```javascript
var csv = require('@tensorflow/tfjs-data/src/data/csv');

var mnistDataset = csv.parse(mnistData, {
  columnConfigs: {
    label: {
      isLabel: true
    }
  }
});
```

Ahora que tenemos nuestro conjunto de datos, podemos comenzar a aplicar el aumento de datos. Comenzaremos creando un objeto `tf.data.Dataset`.


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: sample.xs,
    ys: sample.ys
  };
});
```

A continuación, aplicaremos la transformación `tf.image.resizeBilinear()` al conjunto de datos. Esta transformación cambiará el tamaño de las imágenes.


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: tf.image.resizeBilinear(sample.xs, [28, 28]),
    ys: sample.ys
  };
});
```

También podemos aplicar la transformación `tf.image.rotate()` al conjunto de datos. Esta transformación rotará las imágenes.


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: tf.image.rotate(sample.xs, tf.scalar(Math.random() * 2.0 * Math.PI)),
    ys: sample.ys
  };
});
```

Finalmente, aplicaremos la transformación `tf.image.flipLeftRight()` al conjunto de datos. Esta transformación volteará las imágenes horizontalmente.


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: tf.image.flipLeftRight(sample.xs),
    ys: sample.ys
  };
});
```

Ahora que hemos aplicado nuestras transformaciones, podemos usar el método `.forEachAsync()` para ejecutar el código de aumento de datos en cada muestra de datos.


```javascript
mnistDataset.forEachAsync(function(sample) {
  // augment data here
});
```

## Conclusión

En esta publicación, aprendimos a usar TensorFlow.js y Node.js para realizar el aumento de datos. Hemos visto cómo usar la API `tf.data.Dataset` para aplicar transformaciones a un conjunto de datos. También hemos visto cómo usar el método `.forEachAsync()` para ejecutar el código de aumento de datos en cada muestra de datos.