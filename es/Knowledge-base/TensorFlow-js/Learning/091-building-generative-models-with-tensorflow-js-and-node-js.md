---
title: 091: Creación de modelos generativos con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T04:17:28.544Z
tags: 
editor: markdown
dateCreated: 2023-02-03T04:17:26.939Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [091: Building Generative Models with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/091-building-generative-models-with-tensorflow-js-and-node-js)
{.links-list}


# 091: Construyendo Modelos Generativos con TensorFlow.js y Node.js

En esta publicación, veremos cómo crear modelos generativos con TensorFlow.js y Node.js. Los modelos generativos son una herramienta poderosa para aprender a generar nuevos datos, y TensorFlow.js es una excelente manera de comenzar con el aprendizaje profundo en JavaScript.

## ¿Qué son los modelos generativos?

Los modelos generativos son un tipo de modelo de aprendizaje automático que puede aprender a generar nuevos datos. Por ejemplo, un modelo generativo podría aprender a generar nuevas imágenes de rostros o nuevos fragmentos de texto.

Hay muchos tipos diferentes de modelos generativos, pero uno de los tipos más populares es la Red adversa generativa (GAN). Las GAN son un tipo de red neuronal que consta de dos partes: un generador y un discriminador.

El generador está capacitado para generar nuevos datos, mientras que el discriminador está capacitado para distinguir entre datos reales y generados. Las dos redes compiten entre sí y, a medida que se entrenan, el generador se vuelve cada vez mejor para engañar al discriminador.

## Construyendo un modelo generativo con TensorFlow.js

Ahora que hemos visto qué son los modelos generativos, echemos un vistazo a cómo crear uno con TensorFlow.js.

Hay dos formas de usar TensorFlow.js para crear un modelo generativo: puede usar la API de capas de alto nivel o puede usar la API de nivel inferior.

Si recién está comenzando con TensorFlow.js, le recomendamos que use la API de capas de alto nivel. La API de capas facilita la creación de modelos con solo unas pocas líneas de código y es fácil de usar con el código TensorFlow.js existente.

Para usar la API de capas, primero debemos instalar TensorFlow.js. Podemos hacer esto usando npm:

```
npm install @tensorflow/tfjs
```

Una vez instalado TensorFlow.js, podemos importarlo a nuestro programa Node.js:

```javascript
const tf = require('@tensorflow/tfjs');
```

Ahora que tenemos instalado TensorFlow.js, echemos un vistazo a cómo usarlo para construir un modelo generativo.

Comenzaremos construyendo una red de generador simple. La red del generador tomará un vector de ruido y generará una imagen a partir de ese ruido.

Primero, necesitaremos crear una función que tome un vector de ruido y devuelva una red generadora. Usaremos la API de capas para construir nuestra red de generadores:

```javascript
function createGenerator(noise_size) {
  const generator = tf.sequential();

  // First, we'll build a fully connected layer that takes in our noise vector
  // and generates an image from that noise.
  generator.add(tf.layers.dense({
    inputShape: [noise_size],
    units: 7 * 7 * 256,
    useBias: false,
    kernelInitializer: tf.initializers.truncatedNormal({ stddev: 0.02 })
  }));

  // Next, we'll add a batch normalization layer.
  generator.add(tf.layers.batchNormalization({
    epsilon: 1e-5,
    momentum: 0.9
  }));

  // Then, we'll add a Leaky ReLU activation layer.
  generator.add(tf.layers.leakyReLU(0.2));

  // Next, we'll reshape our vector into a 7x7x256 image.
  generator.add(tf.layers.reshape({
    targetShape: [7, 7, 256]
  }));

  // We'll then add a series of convolutional layers.
  generator.add(tf.layers.conv2dTranspose({
    kernelSize: [3, 3],
    filters: 256,
    strides: [2, 2],
    padding: 'same',
    kernelInitializer: tf.initializers.truncatedNormal({ stddev: 0.02 })
  }));

  generator.add(tf.layers.batchNormalization({
    epsilon: 1e-5,
    momentum: 0.9
  }));

  generator.add(tf.layers.leakyReLU(0.2));

  generator.add(tf.layers.conv2dTranspose({
    kernelSize: [3, 3],
    filters: 128,
    strides: [2, 2],
    padding: 'same',
    kernelInitializer: tf.initializers.truncatedNormal({ stddev: 0.02 })
  }));

  generator.add(tf.layers.batchNormalization({
    epsilon: 1e-5,
    momentum: 0.9
  }));

  generator.add(tf.layers.leakyReLU(0.2));

  // Finally, we'll add a convolutional layer that outputs a 28x28x1 image.
  generator.add(tf.layers.conv2dTranspose({
    kernelSize: [3, 3],
    filters: 1,
    strides: [2, 2],
    padding: 'same',
    kernelInitializer: tf.initializers.truncatedNormal({ stddev: 0.02 }),
    activation: 'tanh'
  }));

  // We'll return the generator model.
  return generator;
}
```

Ahora que tenemos nuestra red generadora, echemos un vistazo a cómo usarla para generar imágenes.

Primero, necesitaremos crear un vector de ruido. Podemos hacer esto creando un tensor con una distribución normal aleatoria:

```javascript
const noise = tf.randomNormal([1, 100]);
```

A continuación, crearemos nuestra red de generadores:

```javascript
const generator = createGenerator(100);
```

Ahora que tenemos nuestra red generadora, podemos usarla para generar una imagen a partir de nuestro vector de ruido:

```javascript
const generated_image = generator.predict(noise);
```

La imagen generada será un tensor de 28x28x1. Podemos convertirlo en una matriz de JavaScript y trazarlo usando la biblioteca plotly.js:

```javascript
const image_array = generated_image.reshape([28, 28]).arraySync();

const data = [
  {
    z: image_array,
    type: 'heatmap'
  }
];

Plotly.newPlot('generated-image', data);
```

Puede ejecutar el código anterior para generar una imagen. Debería ver algo como esto:

![imagen generada](imagen-generada.png)

## Conclusión

En esta publicación, hemos visto cómo construir un modelo generativo con TensorFlow.js y Node.js. Los modelos generativos son una herramienta poderosa para aprender a generar nuevos datos, y TensorFlow.js es una excelente manera de comenzar con el aprendizaje profundo en JavaScript.