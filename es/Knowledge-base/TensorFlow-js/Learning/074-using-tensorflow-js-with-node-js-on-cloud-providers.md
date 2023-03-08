---
title: 074: Uso de TensorFlow.js con Node.js en proveedores de la nube
description: 
published: true
date: 2023-02-03T00:04:39.645Z
tags: 
editor: markdown
dateCreated: 2023-02-03T00:04:37.993Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [074: Using TensorFlow.js with Node.js on Cloud Providers***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/074-using-tensorflow-js-with-node-js-on-cloud-providers)
{.links-list}


# Uso de TensorFlow.js con Node.js en proveedores de la nube

TensorFlow.js es una poderosa herramienta para el aprendizaje automático en JavaScript. Se puede usar en aplicaciones Node.js en proveedores de la nube como AWS, Azure y Google Cloud Platform.

En esta publicación, cubriremos cómo configurar una aplicación Node.js en un proveedor de la nube y usaremos TensorFlow.js para entrenar un modelo de aprendizaje automático. También implementaremos el modelo entrenado en el proveedor de la nube para que pueda usarse en una aplicación web.

## Configuración de una aplicación Node.js en un proveedor de nube

Primero, necesitaremos configurar una aplicación Node.js en un proveedor de nube. Usaremos el marco web Express para configurar una aplicación web básica.

Si no está familiarizado con Express, puede consultar la [guía de introducción] (http://expressjs.com/en/starter/installing.html).

Una vez que haya instalado Express, podemos crear un archivo llamado `app.js` con el siguiente código:

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello, world!');
});

app.listen(3000, () => {
  console.log('Example app listening on port 3000!');
});
```

Este código crea una aplicación Express básica que responde a las solicitudes HTTP con un "¡Hola, mundo!" mensaje.

A continuación, necesitaremos implementar nuestra aplicación Node.js en un proveedor de la nube. Usaremos AWS en este ejemplo, pero el proceso es similar para otros proveedores.

Primero, cree una cuenta de AWS y cree un nuevo usuario de IAM con acceso a EC2. Para obtener más información sobre cómo hacerlo, consulte la [documentación de AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html).

Una vez que haya configurado un usuario de IAM, puede crear una nueva instancia EC2. Para este ejemplo, usaremos una instancia t2.micro.

Una vez que la instancia se está ejecutando, puede acceder a ella mediante SSH e instalar las dependencias para nuestra aplicación Node.js:

```
$ sudo npm install -g express
$ sudo npm install -g ejs
```

A continuación, necesitaremos copiar nuestro archivo `app.js` en la instancia EC2. Podemos hacer esto usando el comando scp:

```
$ scp -i <path-to-pem-file> app.js ec2-user@<ec2-instance-ip>:~/
```

Una vez copiado el archivo, podemos iniciar nuestra aplicación Node.js:

```
$ node app.js
```

¡Nuestra aplicación Node.js ahora se está ejecutando en nuestra instancia EC2!

## Uso de TensorFlow.js con Node.js

Ahora que tenemos nuestra aplicación Node.js en funcionamiento, podemos comenzar a usar TensorFlow.js.

Primero, necesitaremos instalar el paquete TensorFlow.js Node.js:

```
$ npm install @tensorflow/tfjs-node
```

A continuación, crearemos un archivo llamado `train.js` con el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs-node');

// Define a model for linear regression.
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));

// Prepare the model for training: Specify the loss and the optimizer.
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

// Generate some synthetic data for training.
const xs = tf.tensor2d([1, 2, 3, 4], [4, 1]);
const ys = tf.tensor2d([1, 3, 5, 7], [4, 1]);

// Train the model using the data.
model.fit(xs, ys, {epochs: 10}).then(() => {
  // Use the model to do inference on a data point the model hasn't seen before:
  model.predict(tf.tensor2d([5], [1, 1])).print();
});
```

Este código define un modelo de regresión lineal simple usando TensorFlow.js. Luego entrenamos el modelo usando algunos datos sintéticos. Finalmente, usamos el modelo para hacer predicciones sobre nuevos puntos de datos.

Para ejecutar este código, podemos usar el comando `nodo`:

```
$ node train.js
```

## Implementación de un modelo de TensorFlow.js en un proveedor de la nube

Una vez que tenemos un modelo TensorFlow.js entrenado, podemos implementarlo en un proveedor de la nube para que pueda usarse en una aplicación web.

Usaremos AWS nuevamente en este ejemplo, pero el proceso es similar para otros proveedores.

Primero, necesitaremos crear un depósito de Amazon S3 para almacenar nuestros archivos de modelo. Para obtener más información sobre cómo hacerlo, consulte la [documentación de AWS](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html).

A continuación, necesitaremos instalar la CLI de AWS. Para obtener más información sobre cómo hacerlo, consulte la [documentación de AWS](https://docs.aws.amazon.com/cli/latest/userguide/installing.html).

Una vez que la CLI de AWS está instalada, podemos usarla para sincronizar nuestros archivos de modelos locales con nuestro depósito S3:

```
$ aws s3 sync . s3://<s3-bucket-name>
```

¡Nuestro modelo TensorFlow.js ahora está implementado en nuestro depósito S3!