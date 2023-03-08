---
title: 055: Integrando TensorFlow.js con MongoDB en Node.js
description: 
published: true
date: 2023-02-02T19:43:49.243Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:43:44.593Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [055: Integrating TensorFlow.js with MongoDB in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/055-integrating-tensorflow-js-with-mongodb-in-node-js)
{.links-list}


# 05: Integrando TensorFlow.js con MongoDB en Node.js

En esta publicación, aprenderemos cómo integrar TensorFlow.js con MongoDB en Node.js. Cubriremos los siguientes temas:

- ¿Qué es TensorFlow.js?
- ¿Qué es MongoDB?
- Cómo instalar TensorFlow.js y MongoDB
- Cómo integrar TensorFlow.js con MongoDB

## ¿Qué es TensorFlow.js?

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. Está desarrollado por Google y publicado bajo la licencia de código abierto Apache 2.0.

TensorFlow.js se puede usar de varias maneras, entre ellas:

- En el navegador, usando JavaScript
- En Node.js, usando JavaScript
- En una aplicación React Native
- En un contenedor Docker

## ¿Qué es MongoDB?

MongoDB es un poderoso sistema de base de datos orientado a documentos. Está desarrollado por MongoDB, Inc. y publicado bajo la Licencia Pública General GNU Affero.

MongoDB se puede usar de varias maneras, que incluyen:

- Como un sistema de base de datos tradicional
- Como una base de datos NoSQL
- Como una base de datos orientada a documentos
- Como una base de datos de gráficos

## Cómo instalar TensorFlow.js y MongoDB

Antes de que podamos integrar TensorFlow.js con MongoDB, debemos instalar tanto TensorFlow.js como MongoDB.

### Instalación de TensorFlow.js

Hay dos formas de instalar TensorFlow.js:

- Usar una etiqueta de secuencia de comandos
- Usar un administrador de paquetes

#### Uso de una etiqueta de secuencia de comandos

Puede usar una etiqueta de secuencia de comandos para incluir la biblioteca TensorFlow.js en su archivo HTML.

```html
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.3/dist/tf.min.js"></script>
```

#### Usar un administrador de paquetes

Si usa un administrador de paquetes como npm o yarn, puede instalar TensorFlow.js con el siguiente comando:

```
npm install @tensorflow/tfjs
```

### Instalación de MongoDB

Hay dos formas de instalar MongoDB:

- Usando un guión
- Usar un administrador de paquetes

#### Usando un guión

Puede usar un script para instalar MongoDB. El script descargará e instalará MongoDB por usted.

```
curl -O https://fastdl.mongodb.org/osx/mongodb-osx-x86_64-4.2.2.tgz
tar -zxvf mongodb-osx-x86_64-4.2.2.tgz
mkdir -p mongodb
cp -R -n mongodb-osx-x86_64-4.2.2/ mongodb
```

#### Usar un administrador de paquetes

Si está utilizando un administrador de paquetes como Homebrew, puede instalar MongoDB con el siguiente comando:

```
brew install mongodb
```

## Cómo integrar TensorFlow.js con MongoDB

Ahora que tenemos instalados TensorFlow.js y MongoDB, podemos comenzar a integrarlos.

Para hacer esto, tendremos que hacer lo siguiente:

- Instale el controlador MongoDB Node.js
- Conectarse a la base de datos MongoDB
- Crear un esquema
- Entrenar a un modelo
- Desplegar el modelo

### Instale el controlador MongoDB Node.js

Lo primero que debemos hacer es instalar el controlador MongoDB Node.js. Esto lo podemos hacer con el siguiente comando:

```
npm install mongodb
```

### Conectarse a la base de datos MongoDB

A continuación, necesitamos conectarnos a la base de datos MongoDB. Esto lo podemos hacer con el siguiente código:

```javascript
const MongoClient = require('mongodb').MongoClient;

const url = 'mongodb://localhost:27017';

MongoClient.connect(url, { useNewUrlParser: true }, (err, client) => {
  if (err) throw err;

  const db = client.db('test');

  console.log('Connected to MongoDB');
});
```

### Crear un esquema

Ahora que estamos conectados a la base de datos MongoDB, necesitamos crear un esquema. Esto lo podemos hacer con el siguiente código:

```javascript
const schema = new mongoose.Schema({
  name: String,
  age: Number,
  gender: String
});
```

### Entrena a un modelo

Ahora que tenemos un esquema, podemos entrenar un modelo. Esto lo podemos hacer con el siguiente código:

```javascript
const model = tf.sequential();

model.add(tf.layers.dense({ units: 1, inputShape: [1] }));

model.compile({ loss: 'meanSquaredError', optimizer: 'sgd' });

const xs = tf.tensor2d([1, 2, 3, 4], [4, 1]);
const ys = tf.tensor2d([1, 3, 5, 7], [4, 1]);

model.fit(xs, ys, { epochs: 10 }).then(() => {
  model.predict(tf.tensor2d([5], [1, 1])).print();
});
```

### Implementar el modelo

Finalmente, necesitamos implementar el modelo. Esto lo podemos hacer con el siguiente código:

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.use(express.static('public'));

app.get('/', (req, res) => {
  res.sendFile(__dirname + '/index.html');
});

app.listen(port, () => console.log(`Listening on port ${port}`));
```

## Conclusión

En esta publicación, aprendimos cómo integrar TensorFlow.js con MongoDB en Node.js. Hemos cubierto los siguientes temas:

- ¿Qué es TensorFlow.js?
- ¿Qué es MongoDB?
- Cómo instalar TensorFlow.js y MongoDB
- Cómo integrar TensorFlow.js con MongoDB

Si tiene alguna pregunta o comentario, no dude en dejarlos a continuación.