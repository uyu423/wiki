---
title: 084: uso de TensorFlow.js con otras bibliotecas de JavaScript en Node.js
description: 
published: true
date: 2023-02-03T02:37:09.759Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:37:08.086Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [084: Using TensorFlow.js with Other JavaScript Libraries in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/084-using-tensorflow-js-with-other-javascript-libraries-in-node-js)
{.links-list}


# Uso de TensorFlow.js con otras bibliotecas de JavaScript en Node.js

TensorFlow.js es una poderosa herramienta para el aprendizaje automático en JavaScript y funciona muy bien con otras bibliotecas de JavaScript. En esta publicación, le mostraremos cómo usar TensorFlow.js con Node.js y Express.

## Requisitos previos

Para seguir con esta publicación, necesitará algunas cosas:

- Node.js y npm instalados
- Un editor de texto - recomendamos Visual Studio Code
- Conocimientos básicos de JavaScript

## Empezando

Primero, creemos un nuevo directorio para nuestro proyecto:

```
mkdir tensorflowjs-node
cd tensorflowjs-node
```

A continuación, inicializaremos nuestro proyecto con npm:

```
npm init -y
```

Ahora que nuestro proyecto está configurado, podemos instalar las dependencias que necesitaremos. Usaremos las siguientes bibliotecas:

- [TensorFlow.js](https://www.tensorflow.org/js)
- [Exprés](https://expressjs.com/)
- [analizador de cuerpo] (https://www.npmjs.com/package/analizador-de-cuerpo)

Podemos instalar estas dependencias con el siguiente comando:

```
npm install --save @tensorflow/tfjs express body-parser
```

## ¡Hola, TensorFlow.js!

Ahora que tenemos nuestras dependencias instaladas, podemos comenzar a escribir algo de código. Comencemos por crear un archivo llamado `index.js`. En este archivo, escribiremos un script simple para imprimir "¡Hola, TensorFlow.js!" a la consola:

```javascript
// index.js

const tf = require('@tensorflow/tfjs');

console.log('Hello, TensorFlow.js!');
```

Si ejecutamos este script con Node.js, deberíamos ver el siguiente resultado:

```
$ node index.js
Hello, TensorFlow.js!
```

## Uso de TensorFlow.js con Express

Ahora que hemos visto cómo usar TensorFlow.js en un script de Node.js, echemos un vistazo a cómo podemos usarlo con Express. Para este ejemplo, crearemos un servidor simple que responda a las solicitudes `GET` con una lista de números.

Primero, pidamos las dependencias que necesitaremos:

```javascript
// index.js

const tf = require('@tensorflow/tfjs');
const express = require('express');
const bodyParser = require('body-parser');
```

A continuación, crearemos una instancia `Express` y configuraremos `body-parser` para analizar cuerpos JSON:

```javascript
// index.js

const app = express();
app.use(bodyParser.json());
```

Ahora, definamos una ruta que responderá a las solicitudes `GET` con una lista de números:

```javascript
// index.js

app.get('/numbers', (req, res) => {
  const numbers = [1, 2, 3, 4, 5];
  res.json(numbers);
});
```

Finalmente, iniciaremos el servidor en el puerto `3000`:

```javascript
// index.js

app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

Si ejecutamos este script con Node.js, deberíamos ver el siguiente resultado:

```
$ node index.js
Server is listening on port 3000
```

Ahora podemos enviar solicitudes `GET` a `http://localhost:3000/numbers` y recibiremos una respuesta JSON con una lista de números.

## Usando TensorFlow.js con Express y body-parser

En la sección anterior, vimos cómo usar TensorFlow.js con Express. En esta sección, ampliaremos nuestro ejemplo para mostrar cómo podemos usar `body-parser` para analizar cuerpos JSON.

Primero, pidamos las dependencias que necesitaremos:

```javascript
// index.js

const tf = require('@tensorflow/tfjs');
const express = require('express');
const bodyParser = require('body-parser');
```

A continuación, crearemos una instancia `Express` y configuraremos `body-parser` para analizar cuerpos JSON:

```javascript
// index.js

const app = express();
app.use(bodyParser.json());
```

Ahora, definamos una ruta que responderá a las solicitudes `POST` con el cuerpo de la solicitud:

```javascript
// index.js

app.post('/body', (req, res) => {
  res.json(req.body);
});
```

Finalmente, iniciaremos el servidor en el puerto `3000`:

```javascript
// index.js

app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

Si ejecutamos este script con Node.js, deberíamos ver el siguiente resultado:

```
$ node index.js
Server is listening on port 3000
```

Ahora podemos enviar solicitudes `POST` a `http://localhost:3000/body` con un cuerpo JSON y recibiremos una respuesta JSON con el cuerpo de la solicitud.

## Usando TensorFlow.js con Express y body-parser

En la sección anterior, vimos cómo usar TensorFlow.js con Express y body-parser. En esta sección, ampliaremos nuestro ejemplo para mostrar cómo podemos usar TensorFlow.js para realizar inferencias en el cuerpo de la solicitud.

Primero, pidamos las dependencias que necesitaremos:

```javascript
// index.js

const tf = require('@tensorflow/tfjs');
const express = require('express');
const bodyParser = require('body-parser');
```

A continuación, crearemos una instancia `Express` y configuraremos `body-parser` para analizar cuerpos JSON:

```javascript
// index.js

const app = express();
app.use(bodyParser.json());
```

Ahora, definamos una ruta que responderá a las solicitudes `POST` con el cuerpo de la solicitud:

```javascript
// index.js

app.post('/inference', (req, res) => {
  const input = tf.tensor(req.body);
  const output = tf.add(input, 1);
  res.json(output.dataSync());
});
```

Finalmente, iniciaremos el servidor en el puerto `3000`:

```javascript
// index.js

app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

Si ejecutamos este script con Node.js, deberíamos ver el siguiente resultado:

```
$ node index.js
Server is listening on port 3000
```

Ahora podemos enviar solicitudes `POST` a `http://localhost:3000/inference` con un cuerpo JSON y recibiremos una respuesta JSON con el resultado de la inferencia.

## Terminando

En esta publicación, hemos visto cómo usar TensorFlow.js con Node.js y Express. También vimos cómo usar TensorFlow.js con body-parser para analizar cuerpos JSON.

## Recursos

- [TensorFlow.js](https://www.tensorflow.org/js)
- [Exprés](https://expressjs.com/)
- [analizador de cuerpo] (https://www.npmjs.com/package/analizador-de-cuerpo)