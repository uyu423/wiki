---
title: 077: Integración de TensorFlow.js con dispositivos IoT en Node.js
description: 
published: true
date: 2023-02-03T00:43:19.855Z
tags: 
editor: markdown
dateCreated: 2023-02-03T00:43:18.158Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [077: Integrating TensorFlow.js with IoT Devices in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/077-integrating-tensorflow-js-with-iot-devices-in-node-js)
{.links-list}


# Integración de TensorFlow.js con dispositivos IoT en Node.js

TensorFlow.js es una biblioteca de código abierto que se puede usar para desarrollar y entrenar modelos de aprendizaje automático en el navegador. También se puede usar para ejecutar estos modelos en dispositivos IoT. En esta publicación, mostraremos cómo usar TensorFlow.js con Node.js para desarrollar una aplicación que pueda usarse para controlar un dispositivo IoT.

## Requisitos previos

Antes de comenzar, hay algunas cosas que necesitará:

- Una comprensión básica de JavaScript
- Node.js instalado en su computadora
- Un editor de texto (recomendamos [Visual Studio Code](https://code.visualstudio.com/))

## Empezando

Usaremos la biblioteca [TensorFlow.js](https://js.tensorflow.org/) para desarrollar nuestra aplicación. Lo primero que debemos hacer es incluir la biblioteca TensorFlow.js en nuestro proyecto. Podemos hacer esto agregando la siguiente línea de código al encabezado de nuestro archivo HTML:

```
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.0"> </script>
```

Ahora que tenemos la biblioteca TensorFlow.js incluida en nuestro proyecto, podemos comenzar a desarrollar nuestra aplicación.

## Desarrollo de la aplicación

Nuestra aplicación será simple y utilizará un modelo preentrenado para controlar un dispositivo IoT. Lo primero que tenemos que hacer es cargar el modelo. Podemos hacer esto usando la función tf.loadModel():

```javascript
const model = await tf.loadModel('https://my-model-url');
```

A continuación, debemos definir las entradas y salidas de nuestro modelo. Podemos hacer esto usando las funciones tf.layers.input() y tf.layers.dense():

```javascript
const input = tf.layers.input({shape: [1]});
const output = tf.layers.dense({units: 1, activation: 'sigmoid'}).apply(input);
```

Ahora que tenemos nuestro modelo cargado y las entradas y salidas definidas, podemos escribir el código que realmente controlará el dispositivo IoT. Haremos esto creando una función que tome una entrada y use el modelo para predecir la salida:

```javascript
async function predict(input) {
  const output = model.predict(input);
  return output;
}
```

Finalmente, necesitamos escribir el código que llamará a la función predict() y usar la salida para controlar el dispositivo IoT. Haremos esto usando la biblioteca Node.js [serialport](https://serialport.io/):

```javascript
const SerialPort = require('serialport');
const Readline = require('@serialport/parser-readline');

const port = new SerialPort('/dev/ttyACM0', {
  baudRate: 9600
});

const parser = port.pipe(new Readline({ delimiter: '\r\n' }));

parser.on('data', async line => {
  const input = parseFloat(line);
  const output = await predict(input);
  port.write(output);
});
```

## Conclusión

En esta publicación, mostramos cómo usar TensorFlow.js con Node.js para desarrollar una aplicación que se puede usar para controlar un dispositivo IoT. Acabamos de rascar la superficie de lo que es posible con TensorFlow.js e IoT, pero esperamos que esto le haya dado una idea de lo que es posible y lo haya inspirado a explorar más.