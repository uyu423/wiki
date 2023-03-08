---
title: 013: Redes antagónicas generativas (GAN) con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T09:44:15.276Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:44:13.593Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [013: Generative Adversarial Networks (GAN) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/013-generative-adversarial-networks-gan-with-tensorflow-js-and-node-js)
{.links-list}


# Redes adversarias generativas (GAN) con TensorFlow.js y Node.js

En esta publicación, veremos cómo crear una red antagónica generativa (GAN) usando TensorFlow.js y Node.js. Usaremos una GAN para generar nuevas imágenes de dígitos escritos a mano, según el conjunto de datos MNIST.

## ¿Qué es una GAN?

Una GAN es un tipo de red neuronal que se utiliza para el modelado generativo. El modelado generativo es una tarea en el aprendizaje automático donde el objetivo es generar nuevos datos que sean similares a los datos de entrenamiento.

Las GAN están compuestas por dos redes neuronales, un generador y un discriminador. La red del generador toma el ruido como entrada y genera imágenes que son similares a los datos de entrenamiento. La red discriminadora toma imágenes como entrada e intenta clasificarlas como reales o falsas.

Las redes generadora y discriminadora se entrenan juntas en un juego de suma cero, donde el objetivo del generador es engañar al discriminador haciéndole creer que las imágenes generadas son reales, y el objetivo del discriminador es clasificar correctamente las imágenes como reales o falso

## Configuración del proyecto

Antes de que podamos comenzar a entrenar nuestro GAN, debemos configurar nuestro proyecto. Usaremos las siguientes bibliotecas:

- [TensorFlow.js](https://js.tensorflow.org/)
- [búsqueda de nodo](https://www.npmjs.com/package/node-fetch)
- [@tensorflow/tfjs-node](https://www.npmjs.com/package/@tensorflow/tfjs-node)

Puede instalar estas bibliotecas usando npm:

```
npm install tensorflowjs node-fetch @tensorflow/tfjs-node
```

## Cargando el conjunto de datos MNIST

Usaremos el conjunto de datos MNIST para nuestro GAN. El conjunto de datos MNIST es una colección de dígitos escritos a mano, cada uno de los cuales se representa como una imagen en escala de grises de 28x28.

Podemos usar la biblioteca de recuperación de nodos para cargar el conjunto de datos MNIST desde el repositorio de conjuntos de datos de TensorFlow.js:

```javascript
const tf = require('@tensorflow/tfjs-node');
const fetch = require('node-fetch');

// Load the MNIST dataset from the TensorFlow.js Datasets repository.
const mnistDataset = await tf.data.web('https://storage.googleapis.com/tfjs-datasets/mnist.json');
```

## Preprocesamiento del conjunto de datos MNIST

Una vez que hayamos cargado el conjunto de datos MNIST, debemos preprocesarlo para que pueda usarse para entrenar nuestro GAN.

Primero, convertiremos las imágenes en escala de grises de 28x28 en imágenes RGB de 32x32. También normalizaremos los valores de píxel para que estén en el rango [-1, 1].

```javascript
// Convert the 28x28 grayscale images into 32x32 RGB images.
const mnistImages = mnistDataset.images.map(image => tf.image.resizeBilinear(image, [32, 32]));

// Normalize the pixel values to be in the range [-1, 1].
const mnistImages = mnistImages.map(image => image.toFloat().div(tf.scalar(255)).sub(tf.scalar(1)));
```

## Creando la red de generadores

Ahora que hemos preprocesado el conjunto de datos MNIST, podemos comenzar a crear nuestro GAN.

Primero, crearemos la red del generador. La red del generador toma un vector de ruido como entrada y genera una imagen similar a los datos de entrenamiento.

Usaremos un vector de ruido con 100 dimensiones. Usaremos la capa tf.layers.dense para mapear el vector de ruido a una imagen con dimensiones de 32x32x3.

```javascript
// Create the generator network.
const generator = tf.sequential();

// Map the noise vector to an image with 32x32x3 dimensions.
generator.add(tf.layers.dense({inputShape: [100], units: 32 * 32 * 3}));
generator.add(tf.layers.reshape({targetShape: [32, 32, 3]}));
```

## Creando la red discriminadora

A continuación, crearemos la red discriminadora. La red discriminadora toma una imagen como entrada e intenta clasificarla como real o falsa.

Usaremos la capa tf.layers.conv2d para crear una red neuronal convolucional para el discriminador. También usaremos la capa tf.layers.leakyReLU para agregar no linealidad a la red.

```javascript
// Create the discriminator network.
const discriminator = tf.sequential();

// Add a convolutional layer.
discriminator.add(tf.layers.conv2d({inputShape: [32, 32, 3], filters: 16, kernelSize: 3, strides: 2, padding: 'same'}));

// Add a Leaky ReLU layer.
discriminator.add(tf.layers.leakyReLU());

// Add another convolutional layer.
discriminator.add(tf.layers.conv2d({filters: 32, kernelSize: 3, strides: 2, padding: 'same'}));

// Add another Leaky ReLU layer.
discriminator.add(tf.layers.leakyReLU());

// Add a flatten layer.
discriminator.add(tf.layers.flatten());

// Add a fully connected layer.
discriminator.add(tf.layers.dense({units: 1}));

// Add a sigmoid activation layer.
discriminator.add(tf.layers.activation({activation: 'sigmoid'}));
```

## Entrenamiento de la GAN

Ahora que hemos creado las redes generadoras y discriminadoras, podemos entrenar nuestra GAN.

Primero, crearemos un modelo GAN que combine las redes del generador y del discriminador.

A continuación, compilaremos el modelo GAN con el optimizador tf.train.adamOptimizer.

Finalmente, entrenaremos el modelo GAN usando el método tf.train.ganTrain().

```javascript
// Create a GAN model that combines the generator and discriminator.
const gan = tf.sequential();

// Add the generator to the GAN.
gan.add(generator);

// Freeze the generator.
generator.trainable = false;

// Add the discriminator to the GAN.
gan.add(discriminator);

// Compile the GAN using the Adam optimizer.
gan.compile({loss: 'binaryCrossentropy', optimizer: tf.train.adamOptimizer()});

// Train the GAN.
for (let i = 0; i < 100; i++) {
  // Get a batch of real images.
  const realImages = mnistImages.slice(i * 10, (i + 1) * 10);

  // Generate a batch of fake images.
  const noise = tf.randomNormal([10, 100]);
  const fakeImages = generator.predict(noise);

  // Create a batch of labels for the real and fake images.
  const realLabels = tf.ones([10, 1]);
  const fakeLabels = tf.zeros([10, 1]);

  // Train the discriminator on the real and fake images.
  const loss = await gan.fit([realImages, fakeImages], [realLabels, fakeLabels], {
    epochs: 1,
    batchSize: 10
  });

  // Generate and show a batch of fake images.
  const noise = tf.randomNormal([10, 100]);
  const fakeImages = generator.predict(noise);
  fakeImages.forEach((image, i) => {
    const canvas = document.createElement('canvas');
    canvas.width = 28;
    canvas.height = 28;
    const ctx = canvas.getContext('2d');
    const imageData = new ImageData(28, 28);
    const data = image.dataSync();
    for (let j = 0; j < 28 * 28; j++) {
      const k = j * 4;
      const imgIdx = j;
      imageData.data[k + 0] = (data[imgIdx + 0] + 1) * 127;
      imageData.data[k + 1] = (data[imgIdx + 1] + 1) * 127;
      imageData.data[k + 2] = (data[imgIdx + 2] + 1) * 127;
      imageData.data[k + 3] = 255;
    }
    ctx.putImageData(imageData, 0, 0);
    document.body.appendChild(canvas);
  });
}
```

## Generando nuevas imágenes

Una vez que se ha entrenado la GAN, podemos usarla para generar nuevas imágenes.

Primero, generaremos un vector de ruido con 100 dimensiones.

A continuación, usaremos la red del generador para generar una imagen a partir del vector de ruido.

Finalmente, mostraremos la imagen generada en la pantalla.

```javascript
// Generate a noise vector with 100 dimensions.
const noise = tf.randomNormal([1, 100]);

// Use the generator to generate an image from the noise vector.
const generatedImage = generator.predict(noise);

// Show the generated image.
const canvas = document.createElement('canvas');
canvas.width = 28;
canvas.height = 28;
const ctx = canvas.getContext('2d');
const imageData = new ImageData(28, 28);
const data = generatedImage.dataSync();
for (let i = 0; i < 28 * 28; i++) {
  const j = i * 4;
  const imgIdx = i;
  imageData.data[j + 0] = (data[imgIdx + 0] + 1) * 127;
  imageData.data[j + 1] = (data[imgIdx + 1] + 1) * 127;
  imageData.data[j + 2] = (data[imgIdx + 2] + 1) * 127;
  imageData.data[j + 3] = 255;
}
ctx.putImageData(imageData, 0, 0);
document.body.appendChild(canvas);
```

## Conclusión

En esta publicación, hemos visto cómo crear una GAN usando TensorFlow.js y Node.js. También hemos visto cómo usar la GAN para generar nuevas imágenes de dígitos escritos a mano.

Si desea obtener más información sobre las GAN, le recomiendo los siguientes recursos:

- [Generative Adversarial Networks](https://arxiv.org/abs/1406.2661) (documento de investigación)
- [Aprendizaje profundo con JavaScript](https://www.manning.com/livevideo/deep-learning-with-javascript) (videocurso)
- [Redes adversarias generativas en TensorFlow](https://www.tensorflow.org/tutorials/generative/gan) (tutorial)