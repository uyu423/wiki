---
title: 054: Creación de API REST con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T19:36:27.280Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:36:25.588Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [054: Creating REST APIs with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/054-creating-rest-apis-with-tensorflow-js-and-node-js)
{.links-list}


# Creación de API REST con TensorFlow.js y Node.js

## Introducción

En esta publicación, le mostraremos cómo crear API REST con TensorFlow.js y Node.js. Repasaremos todos los pasos necesarios para poner en marcha su proyecto, incluida la instalación de las dependencias requeridas, la configuración de su proyecto y la escritura de su código.

Al final de esta publicación, podrá crear sus propias API REST con TensorFlow.js y Node.js.

## Requisitos previos

Antes de comenzar, hay algunas cosas que deberá tener para seguir:

- Un editor de texto. Recomendamos [Visual Studio Code](https://code.visualstudio.com/).
- [Node.js](https://nodejs.org/en/) instalado en su máquina.
- [npm](https://www.npmjs.com/) instalado en su máquina.
- [TensorFlow.js](https://js.tensorflow.org/) instalado en su máquina.

## Configurando tu proyecto

Una vez que haya configurado los requisitos previos, estará listo para comenzar a configurar su proyecto.

Primero, cree un nuevo directorio para su proyecto. Llamaremos al nuestro `tfjs-rest-api`.

A continuación, inicialice su proyecto ejecutando `npm init` en el directorio de su proyecto. Esto creará un archivo `package.json` para su proyecto.

Ahora que tiene un archivo `package.json`, puede instalar las dependencias para su proyecto. Ejecute el siguiente comando para instalar [Express](https://expressjs.com/), [Body-Parser](https://www.npmjs.com/package/body-parser) y [TensorFlow.js]( https://www.npmjs.com/package/@tensorflow/tfjs):

```
npm install express body-parser @tensorflow/tfjs --save
```

Esto instalará las dependencias y las agregará a su archivo `package.json`.

## Escribiendo tu código

Ahora que tiene su proyecto configurado, está listo para comenzar a escribir su código.

Abra su editor de texto y cree un nuevo archivo en el directorio de su proyecto. Llamaremos al nuestro `index.js`.

En este archivo, comenzaremos solicitando las dependencias que instalamos anteriormente:

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const tf = require('@tensorflow/tfjs');
```

A continuación, configuraremos nuestro servidor Express:

```javascript
const app = express();
const port = 3000;

app.use(bodyParser.json());

app.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});
```

Ahora que nuestro servidor está configurado, podemos comenzar a escribir nuestros puntos finales de API.

Nuestro primer punto final será una solicitud `GET` a `/` que devolverá un mensaje simple:

```javascript
app.get('/', (req, res) => {
  res.send('Hello, world!');
});
```

Nuestro segundo punto final será una solicitud `POST` a `/predict` que tomará una serie de números y devolverá una predicción basada en esos números:

```javascript
app.post('/predict', (req, res) => {
  const input = tf.tensor2d([req.body.numbers], [1, req.body.numbers.length]);
  const output = model.predict(input);
  res.send(output.dataSync());
});
```

En este punto final, usamos un modelo [TensorFlow.js](https://js.tensorflow.org/) entrenado previamente para hacer nuestras predicciones. Puede encontrar este modelo [aquí](https://storage.googleapis.com/tfjs-models/tfjs/mnist_model/model.json).

## Probando tu API

Ahora que tiene configurados los puntos finales de la API, está listo para probarlos.

Para probar su punto final `GET`, puede usar una herramienta como [Postman] (https://www.getpostman.com/).

Para probar su punto final `POST`, puede usar el siguiente comando:

```
curl -X POST -H "Content-Type: application/json" -d '{"numbers": [1, 2, 3, 4, 5]}' http://localhost:3000/predict
```

Esto debería devolver una predicción de `[6]`.

## Conclusión

En esta publicación, le mostramos cómo crear API REST con TensorFlow.js y Node.js. Cubrimos todos los pasos necesarios para poner en marcha su proyecto, incluida la instalación de las dependencias requeridas, la configuración de su proyecto y la escritura de su código.

Al final de esta publicación, debería poder crear sus propias API REST con TensorFlow.js y Node.js.