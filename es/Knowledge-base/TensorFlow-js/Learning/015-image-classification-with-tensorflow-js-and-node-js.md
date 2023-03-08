---
title: 015: Clasificación de imágenes con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T10:17:57.615Z
tags: 
editor: markdown
dateCreated: 2023-02-02T10:17:55.930Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [015: Image Classification with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/015-image-classification-with-tensorflow-js-and-node-js)
{.links-list}


# Introducción

En esta publicación, veremos cómo usar TensorFlow.js y Node.js para crear un modelo de clasificación de imágenes. Usaremos el modelo MobileNet, que es un modelo preentrenado que ha sido entrenado en un gran conjunto de datos de imágenes.

Usaremos las siguientes bibliotecas:

* [TensorFlow.js](https://js.tensorflow.org/)
* [Node.js](https://nodejs.org/en/)

## Requisitos previos

Antes de comenzar, hay algunas cosas que deberá configurar:

* Un editor de texto. Recomiendo [Visual Studio Code](https://code.visualstudio.com/).
* [Node.js](https://nodejs.org/en/). Esto se utilizará para ejecutar nuestro código.
* [TensorFlow.js](https://js.tensorflow.org/). Esta es una biblioteca de JavaScript para el aprendizaje automático.

## Empezando

1. Cree un nuevo directorio para su proyecto.

2. Cree un archivo llamado `index.js` en el directorio de su proyecto.

3. Copie el siguiente código en `index.js`:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MobileNet model.
const model = tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');

// Make a prediction through the model on our image.
const imgEl = document.getElementById('img');
model.predict(tf.fromPixels(imgEl)).then(predictions => {
  console.log('Predictions: ');
  console.log(predictions);
});
```

4. Cree un archivo llamado `index.html` en el directorio de su proyecto.

5. Copie el siguiente código en `index.html`:

```html
<html>
  <body>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.11.3"> </script>
    <script src="index.js"></script>
    <img id="img" src="https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/test_images/grace_hopper.jpg">
  </body>
</html>
```

6. Ejecute el siguiente comando para iniciar el servidor:

```
node index.js
```

Debería ver el siguiente resultado:

```
Predictions:
[
  {
    className: 'daisy',
    probability: 0.9911273956298828
  },
  {
    className: 'tulip',
    probability: 0.008872604370117188
  },
  {
    className: 'sunflower',
    probability: 0.0001983642578125
  },
  {
    className: 'dandelion',
    probability: 0.0000457763671875
  },
  {
    className: 'roses',
    probability: 0.0000095367431640625
  }
]
```

## ¿Qué esta pasando?

En el código anterior, usamos el modelo MobileNet para clasificar una imagen. MobileNet es un modelo preentrenado que ha sido entrenado en un gran conjunto de datos de imágenes.

Cuando ejecutamos el método `predict`, TensorFlow.js devolverá una serie de predicciones, cada una con un `className` y una `probability`. El `className` es el nombre de la clase a la que el modelo predice que pertenece la imagen, y la `probabilidad` es la confianza que el modelo tiene en esa predicción.

## Hacer predicciones en una cámara web

En el ejemplo anterior, usamos un modelo previamente entrenado para hacer predicciones sobre una imagen. Pero, ¿qué pasa si queremos hacer predicciones en una cámara web en vivo?

Para hacer esto, necesitaremos usar las API `tf.data` y `tf.layers`.

Primero, crearemos un objeto `webcam`. Esto se usará para capturar la transmisión de la cámara web en vivo:

```javascript
const webcam = new tf.data.webcam(document.getElementById('webcam'));
```

A continuación, crearemos una capa `convolucional`. Esta capa se utilizará para procesar la transmisión de la cámara web en vivo:

```javascript
const layer = tf.layers.conv2d({
  kernelSize: 5,
  filters: 20,
  strides: 1,
  activation: 'relu',
  kernelInitializer: 'varianceScaling',
  inputShape: [28, 28, 1]
});
```

Ahora crearemos una `función` que se usará para hacer predicciones en la transmisión de la cámara web en vivo. Esta función tomará una imagen, la procesará a través de la capa `convolucional` y devolverá una predicción:

```javascript
async function predict(image) {
  // Make a prediction through the model on the image.
  const predictions = await model.predict(image);

  // Return the highest confidence prediction.
  return predictions.as1D().argMax();
}
```

Finalmente, crearemos un `bucle` que continuamente hará predicciones en la transmisión de la cámara web en vivo:

```javascript
while (true) {
  // Get the next image from the webcam.
  const img = await webcam.capture();

  // Get the prediction from our model.
  const prediction = await predict(img);

  // Convert the prediction into a human-readable string.
  const classNames = ['daisy', 'tulip', 'sunflower', 'dandelion', 'roses'];
  const className = classNames[prediction.dataSync()[0]];

  // Display the string on the page.
  document.getElementById('prediction').innerText = className;

  // Dispose the image when we're done.
  img.dispose();

  // Give some breathing room by waiting for the next animation frame to
  // fire before making another prediction.
  await tf.nextFrame();
}
```

## Conclusión

En esta publicación, hemos visto cómo usar TensorFlow.js y Node.js para construir un modelo de clasificación de imágenes. También hemos visto cómo usar el modelo para hacer predicciones en una transmisión de cámara web en vivo.