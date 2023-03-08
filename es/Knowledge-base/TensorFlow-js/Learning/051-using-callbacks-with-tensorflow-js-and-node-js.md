---
title: 051: uso de devoluciones de llamada con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T18:43:29.401Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:43:27.810Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [051: Using Callbacks with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/051-using-callbacks-with-tensorflow-js-and-node-js)
{.links-list}


# Usar devoluciones de llamada con TensorFlow.js y Node.js

TensorFlow.js es una poderosa herramienta para el aprendizaje automático en JavaScript. Node.js es un tiempo de ejecución de JavaScript que le permite ejecutar JavaScript en el servidor. En esta publicación, le mostraremos cómo usar las devoluciones de llamada con TensorFlow.js y Node.js.

## ¿Qué son las devoluciones de llamada?

Una devolución de llamada es una función que se pasa como argumento a otra función. La función de devolución de llamada se llama cuando la otra función termina de ejecutarse. Las devoluciones de llamada se usan comúnmente en JavaScript para realizar operaciones asíncronas.

## Usar devoluciones de llamada con TensorFlow.js

TensorFlow.js proporciona una API de devolución de llamada que le permite realizar operaciones asincrónicas. La API de devolución de llamada está disponible en la clase `tf.tensor`.

Para usar la API de devolución de llamada, primero debe crear un objeto `tf.tensor`. La clase `tf.tensor` toma una matriz de datos y una matriz de forma como argumentos. La matriz de datos es una matriz de JavaScript que contiene los datos para el tensor. La matriz de formas es una matriz de JavaScript que contiene las dimensiones del tensor.

Una vez que haya creado un objeto `tf.tensor`, puede usar el método `.then()` para registrar una función de devolución de llamada. El método `.then()` toma una función de devolución de llamada como argumento. La función de devolución de llamada se llama cuando el objeto `tf.tensor` está listo.

El método `.then()` devuelve un objeto `Promise`. El objeto `Promise` representa el resultado del método `.then()`. El objeto `Promise` tiene un método `.then()` que se puede usar para registrar otra función de devolución de llamada.

Aquí hay un ejemplo del uso del método `.then()` para registrar una función de devolución de llamada:

```javascript
const tensor = tf.tensor([1, 2, 3, 4], [2, 2]);

tensor.then(t => {
  // The callback function is called when the tensor is ready.
  // The tensor is passed as an argument to the callback function.
  // The tensor can be used in the callback function.
  console.log(t);
});
```

## Usar devoluciones de llamada con Node.js

Node.js proporciona una API de devolución de llamada que le permite realizar operaciones asincrónicas. La API de devolución de llamada está disponible en el módulo `fs`.

El módulo `fs` proporciona una API para interactuar con el sistema de archivos. El módulo `fs` tiene un método `readFile()` que se puede usar para leer un archivo de forma asíncrona. El método `readFile()` toma una ruta de archivo y una función de devolución de llamada como argumentos. La función de devolución de llamada se llama cuando se lee el archivo. Los datos del archivo se pasan como argumento a la función de devolución de llamada.

Aquí hay un ejemplo del uso del método `readFile()` para leer un archivo de forma asíncrona:

```javascript
const fs = require('fs');

fs.readFile('file.txt', (err, data) => {
  // The callback function is called when the file is read.
  // The file data is passed as an argument to the callback function.
  // The file data can be used in the callback function.
  console.log(data);
});
```

## Información Adicional

- [Uso de promesas](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
- [Devoluciones de llamada de Node.js] (https://nodejs.org/api/fs.html# fs_fs_readfile_path_options_callback)