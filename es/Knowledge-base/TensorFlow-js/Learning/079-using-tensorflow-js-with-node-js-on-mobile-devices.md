---
title: 079: Uso de TensorFlow.js con Node.js en dispositivos móviles
description: 
published: true
date: 2023-02-03T01:17:41.898Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:17:40.286Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [079: Using TensorFlow.js with Node.js on Mobile Devices***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/079-using-tensorflow-js-with-node-js-on-mobile-devices)
{.links-list}


## Introducción

TensorFlow.js es una biblioteca de código abierto que se puede usar para desarrollar y entrenar modelos de aprendizaje automático en el navegador o en un servidor Node.js. En esta publicación, nos centraremos en usar TensorFlow.js con Node.js en dispositivos móviles.

TensorFlow.js ofrece muchos beneficios sobre los marcos tradicionales de aprendizaje automático del lado del servidor, como una mayor flexibilidad y portabilidad. Los dispositivos móviles suelen tener recursos limitados, por lo que poder ejecutar modelos de aprendizaje automático en el dispositivo es una gran ventaja.

## Configuración del entorno

Antes de comenzar, debemos configurar nuestro entorno de desarrollo. Necesitaremos instalar Node.js y la biblioteca TensorFlow.js.

Node.js se puede descargar e instalar desde el sitio web oficial (https://nodejs.org/en/). Una vez que se instala Node.js, podemos usar Node Package Manager (npm) para instalar TensorFlow.js.

```
npm install @tensorflow/tfjs
```

## ¡Hola, TensorFlow.js!

Ahora que tenemos nuestro entorno configurado, ¡escribamos nuestro primer programa TensorFlow.js!

```javascript
// Load the TensorFlow.js library
const tf = require('@tensorflow/tfjs');

// Define a TensorFlow.js model
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));

// Compile the model
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

// Fit the model to the data
const xs = tf.tensor2d([-1.0, 0.0, 1.0, 2.0, 3.0, 4.0], [6, 1]);
const ys = tf.tensor2d([-3.0, -1.0, 1.0, 3.0, 5.0, 7.0], [6, 1]);

model.fit(xs, ys, {epochs: 500}).then(() => {
  // Use the model to predict the output of a new Tensor
  model.predict(tf.tensor2d([5], [1, 1])).print();
});
```

En este programa, primero cargamos la biblioteca TensorFlow.js usando la función require(). Luego definimos un modelo secuencial usando la función tf.secuencial().

Luego, agregamos una capa densa al modelo usando la función tf.layers.dense(). Esta capa tiene una unidad y espera una entrada de tamaño uno.

Después de agregar la capa, compilamos el modelo usando la función tf.compile(). Especificamos que queremos usar la función de pérdida de error cuadrático medio y el optimizador de descenso de gradiente estocástico.

Finalmente, ajustamos el modelo a los datos usando la función tf.fit(). Especificamos que queremos ejecutar 500 épocas de entrenamiento.

Una vez que se entrena el modelo, usamos la función tf.predict() para predecir la salida de un nuevo tensor. En este caso, predecimos la salida para el Tensor [5].

## Ejecutar TensorFlow.js en un dispositivo móvil

Ahora que hemos visto cómo escribir un programa TensorFlow.js, veamos cómo podemos ejecutarlo en un dispositivo móvil.

Hay dos formas de ejecutar TensorFlow.js en un dispositivo móvil: usando el navegador web o usando una aplicación nativa.

Si queremos usar el navegador web, debemos asegurarnos de que nuestro programa TensorFlow.js se esté ejecutando en un servidor web. Podemos usar cualquier servidor web, pero para este ejemplo usaremos Node.js.

Primero, necesitamos instalar el paquete npm del servidor http.

```
npm install http-server
```

Una vez que el paquete del servidor http está instalado, podemos usarlo para iniciar un servidor web desde la línea de comandos.

```
http-server
```

Esto iniciará un servidor web en el puerto 8080. Ahora podemos acceder a nuestro programa TensorFlow.js yendo a http://localhost:8080 en nuestro navegador web.

Si queremos usar una aplicación nativa, debemos usar una biblioteca TensorFlow.js específica de la plataforma. Para iOS, podemos usar la biblioteca TensorFlow Lite Swift (https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/swift). Para Android, podemos usar la biblioteca de Android TensorFlow Lite (https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/android).

## Conclusión

En esta publicación, hemos visto cómo usar TensorFlow.js con Node.js en dispositivos móviles. TensorFlow.js ofrece muchos beneficios sobre los marcos tradicionales de aprendizaje automático del lado del servidor, como una mayor flexibilidad y portabilidad. Los dispositivos móviles suelen tener recursos limitados, por lo que poder ejecutar modelos de aprendizaje automático en el dispositivo es una gran ventaja.