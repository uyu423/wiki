---
title: 098: Creación de redes antagónicas generativas (GAN) en TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T06:04:52.608Z
tags: 
editor: markdown
dateCreated: 2023-02-03T06:04:51.005Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [098: Building Generative Adversarial Networks (GANs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/098-building-generative-adversarial-networks-gans-in-tensorflow-js-and-node-js)
{.links-list}


# 098: Creación de redes antagónicas generativas (GAN) en TensorFlow.js y Node.js

Los desarrolladores que buscan construir modelos generativos usando TensorFlow.js y Node.js pueden hacerlo usando una Red adversa generativa (GAN). En esta publicación, lo guiaremos a través del proceso de creación de una GAN en TensorFlow.js y Node.js.

## ¿Qué son las GAN?

Una GAN es un tipo de red neuronal que se utiliza para generar nuevos datos desde cero. La red consta de dos partes: un generador y un discriminador. El generador se encarga de generar nuevos datos, mientras que el discriminador se encarga de determinar si los datos son reales o falsos.

## Construyendo una GAN en TensorFlow.js

El primer paso para construir una GAN es crear un nuevo archivo llamado `gan.js`. Comenzaremos solicitando los módulos `tensorflow` y `tfjs-node`:

```javascript
const tf = require('tensorflow');
const tfNode = require('tfjs-node');
```

A continuación, definiremos los modelos generador y discriminador:

```javascript
// Generator
const generator = tf.sequential();
generator.add(tf.layers.dense({units: 100, inputShape: [100]}));
generator.add(tf.layers.batchNormalization());
generator.add(tf.layers.leakyReLU());
generator.add(tf.layers.dense({units: 784, activation: 'tanh'}));

// Discriminator
const discriminator = tf.sequential();
discriminator.add(tf.layers.dense({units: 784, inputShape: [784]}));
discriminator.add(tf.layers.leakyReLU());
discriminator.add(tf.layers.dense({units: 1, activation: 'sigmoid'}));
```

En el código anterior, hemos definido un generador que toma vectores de ruido de 100 dimensiones y genera vectores de 784 dimensiones (es decir, imágenes de 28x28). También hemos definido un discriminador que toma vectores de 784 dimensiones y genera un valor único que indica si el vector es real o falso.

A continuación, necesitamos compilar los modelos:

```javascript
// Generator
generator.compile({
  optimizer: tf.train.adam(0.0001),
  loss: 'binaryCrossentropy'
});

// Discriminator
discriminator.compile({
  optimizer: tf.train.adam(0.0001),
  loss: 'binaryCrossentropy'
});
```

En el código anterior, especificamos que los modelos deben optimizarse utilizando el optimizador de Adam con una tasa de aprendizaje de 0,0001. También hemos especificado que la función de pérdida para ambos modelos debe ser entropía cruzada binaria.

## Entrenamiento de la GAN

Ahora que hemos definido y compilado los modelos, podemos comenzar a entrenar la GAN. El proceso de entrenamiento consta de dos pasos: entrenar el discriminador y entrenar el generador.

### Entrenar al discriminador

El primer paso para entrenar la GAN es entrenar el discriminador. Haremos esto generando un lote de datos falsos usando el generador y un lote de datos reales usando un conjunto de datos de entrenamiento. Luego entrenaremos al discriminador en estos dos lotes de datos.

```javascript
// Train the discriminator
for (let i = 0; i < 1000; i++) {
  // Generate a batch of fake data
  const noise = tf.randomNormal([batchSize, 100]);
  const fakeData = generator.predict(noise);

  // Generate a batch of real data
  const realData = tf.data.nextBatch(batchSize, [784]);

  // Train the discriminator
  const xs = tf.concat([fakeData, realData], 0);
  const ys = tf.concat([tf.zeros([batchSize, 1]), tf.ones([batchSize, 1])], 0);
  discriminator.fit(xs, ys);
}
```

En el código anterior, generamos un lote de datos falsos usando el generador y un lote de datos reales usando un conjunto de datos de entrenamiento. Luego concatenamos estos dos lotes de datos y entrenamos al discriminador en ellos.

### Entrenamiento del generador

Ahora que el discriminador ha sido entrenado, podemos entrenar el generador. Haremos esto generando un lote de vectores de ruido y pasándolos a través del generador. Luego entrenaremos al generador en estos vectores de ruido.

```javascript
// Train the generator
for (let i = 0; i < 1000; i++) {
  // Generate a batch of noise vectors
  const noise = tf.randomNormal([batchSize, 100]);

  // Train the generator
  const ys = tf.ones([batchSize, 1]);
  generator.fit(noise, ys);
}
```

En el código anterior, generamos un lote de vectores de ruido y los pasamos a través del generador. Luego hemos entrenado al generador en estos vectores de ruido.

## Generación de nuevos datos

Ahora que se ha entrenado la GAN, podemos usarla para generar nuevos datos. Para ello, generaremos un lote de vectores de ruido y los pasaremos por el generador.

```javascript
// Generate a batch of noise vectors
const noise = tf.randomNormal([batchSize, 100]);

// Generate new data
const generatedData = generator.predict(noise);
```

En el código anterior, generamos un lote de vectores de ruido y los pasamos a través del generador. Esto ha generado un lote de nuevos datos que se pueden utilizar para cualquier propósito.