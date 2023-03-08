---
title: 067: Creación de aplicaciones de escritorio con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T22:36:28.419Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:36:26.667Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [067: Creating Desktop Applications with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/067-creating-desktop-applications-with-tensorflow-js-and-node-js)
{.links-list}


# 067: Creando Aplicaciones de Escritorio con TensorFlow.js y Node.js

En esta publicación, veremos cómo crear aplicaciones de escritorio con TensorFlow.js y Node.js.

TensorFlow.js es una poderosa herramienta para el aprendizaje automático en JavaScript. Node.js es un tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript fuera del navegador.

Juntas, estas dos tecnologías se pueden usar para crear aplicaciones de escritorio que usan el aprendizaje automático.

## Empezando

Para comenzar, deberá instalar Node.js y TensorFlow.js.

Node.js se puede descargar desde el [sitio web de Node.js] (https://nodejs.org/en/). TensorFlow.js se puede instalar usando el [administrador de paquetes de Node.js] (https://www.npmjs.com/):

```
npm install @tensorflow/tfjs
```

Una vez que haya instalado Node.js y TensorFlow.js, estará listo para comenzar a crear su aplicación de escritorio.

## Creación de una aplicación de escritorio

Para crear una aplicación de escritorio con TensorFlow.js y Node.js, deberá crear un archivo Node.js y un archivo HTML.

El archivo Node.js se usará para ejecutar su código de aprendizaje automático. El archivo HTML se utilizará para mostrar los resultados de su código de aprendizaje automático.

Comenzaremos creando un archivo Node.js llamado `main.js`. En este archivo, necesitaremos la biblioteca TensorFlow.js y cargaremos un modelo previamente entrenado.

```javascript
const tf = require('@tensorflow/tfjs');

// Load a pre-trained model.
const model = tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

A continuación, crearemos un archivo HTML llamado `index.html`. En este archivo, incluiremos el siguiente código:

```html
<html>
  <head>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs"></script>
    <script src="main.js"></script>
  </head>
  <body>
    <h1>Hello, TensorFlow.js!</h1>
  </body>
</html>
```

Este código incluye la biblioteca TensorFlow.js y el archivo `main.js`. También contiene una etiqueta simple `<h1>`.

Finalmente, necesitaremos ejecutar el archivo `index.html` usando Node.js. Esto lo podemos hacer ejecutando el siguiente comando:

```
node index.html
```

Esto iniciará un servidor local y abrirá el archivo `index.html` en su navegador web predeterminado.

## Conclusión

En esta publicación, hemos visto cómo crear aplicaciones de escritorio con TensorFlow.js y Node.js. También vimos cómo cargar un modelo previamente entrenado y ejecutarlo en un archivo Node.js.

Si está interesado en obtener más información sobre TensorFlow.js y Node.js, le recomiendo consultar los siguientes recursos:

- [Introducción a TensorFlow.js](https://js.tensorflow.org/tutorials/getting-started.html)
- [TensorFlow.js para principiantes](https://www.youtube.com/watch?v=HEQDRWMK6yY)
- [Node.js para principiantes](https://www.youtube.com/watch?v=U8XF6AFGqlc)