---
title: 093: Creación de redes antagónicas generativas convolucionales profundas (DC-GAN) en TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T04:44:37.018Z
tags: 
editor: markdown
dateCreated: 2023-02-03T04:44:35.188Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [093: Building Deep Convolutional Generative Adversarial Networks (DC-GANs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/093-building-deep-convolutional-generative-adversarial-networks-dc-gans-in-tensorflow-js-and-node-js)
{.links-list}


# 093: Creación de redes antagónicas generativas convolucionales profundas (DC-GAN) en TensorFlow.js y Node.js

Las redes antagónicas generativas convolucionales profundas (DC-GAN) son un tipo de red antagónica generativa (GAN) que se utilizan para generar nuevas imágenes a partir de un conjunto de datos de entrenamiento.

Las GAN son un tipo de red neuronal que se compone de dos partes: un generador y un discriminador. El generador crea nuevas imágenes que son similares a los datos de entrenamiento, mientras que el discriminador trata de distinguir entre las imágenes de entrenamiento reales y las imágenes falsas generadas por el generador.

Las DC-GAN son un tipo de GAN que utiliza redes neuronales convolucionales profundas tanto para el generador como para el discriminador.

En este tutorial, usaremos TensorFlow.js y Node.js para construir un DC-GAN. Usaremos el conjunto de datos MNIST, que es un conjunto de datos de dígitos escritos a mano.

## Empezando

Primero, necesitamos instalar TensorFlow.js y Node.js. Esto lo podemos hacer usando el siguiente comando:

```
npm install -g @tensorflow/tfjs-node
```

A continuación, necesitamos descargar el conjunto de datos MNIST. Esto lo podemos hacer usando el siguiente comando:

```
wget http://yann.lecun.com/exdb/mnist/train-images-idx3-ubyte.gz
wget http://yann.lecun.com/exdb/mnist/train-labels-idx1-ubyte.gz
wget http://yann.lecun.com/exdb/mnist/t10k-images-idx3-ubyte.gz
wget http://yann.lecun.com/exdb/mnist/t10k-labels-idx1-ubyte.gz
```

También necesitamos descomprimir los archivos descargados. Esto lo podemos hacer usando el siguiente comando:

```
gunzip *
```

## Preprocesamiento de los datos

Ahora que tenemos el conjunto de datos MNIST, debemos preprocesarlo para que DC-GAN pueda usarlo.

Primero, necesitamos convertir las imágenes del conjunto de datos MNIST a un formato que pueda usar DC-GAN. Esto lo podemos hacer usando el siguiente comando:

```
tensorflowjs_converter --input_format=tfjs-layers-model --output_format=tfjs-layers-model --output_node_names='input,output' ./mnist_model.h5 ./tfjs_model
```

Este comando convertirá el conjunto de datos MNIST a un formato que pueda ser utilizado por DC-GAN.

A continuación, debemos dividir el conjunto de datos MNIST en un conjunto de entrenamiento y un conjunto de prueba. Esto lo podemos hacer usando el siguiente comando:

```
tensorflowjs_converter --input_format=tfjs-layers-model --output_format=tfjs-layers-model --output_node_names='input,output' --train_test_split=0.8 ./mnist_model.h5 ./tfjs_model
```

Este comando dividirá el conjunto de datos MNIST en un conjunto de entrenamiento y un conjunto de prueba. El conjunto de entrenamiento se usará para entrenar la DC-GAN, mientras que el conjunto de prueba se usará para evaluar la DC-GAN.

## Construyendo el DC-GAN

Ahora que tenemos el conjunto de datos MNIST, podemos comenzar a construir el DC-GAN.

Primero, necesitamos crear la red del generador. La red generadora tomará como entrada un vector de ruido y generará una imagen similar al conjunto de datos MNIST.

Podemos crear la red del generador usando el siguiente código:

```javascript
const generator = tf.sequential();

generator.add(tf.layers.dense({inputShape: [100], units: 7*7*256}));
generator.add(tf.layers.batchNormalization());
generator.add(tf.layers.leakyReLU());

generator.add(tf.layers.reshape({targetShape: [7, 7, 256]}));
generator.add(tf.layers.conv2dTranspose({
    kernelSize: 5,
    filters: 128,
    strides: 2,
    padding: 'same',
    useBias: false
}));
generator.add(tf.layers.batchNormalization());
generator.add(tf.layers.leakyReLU());

generator.add(tf.layers.conv2dTranspose({
    kernelSize: 5,
    filters: 64,
    strides: 2,
    padding: 'same',
    useBias: false
}));
generator.add(tf.layers.batchNormalization());
generator.add(tf.layers.leakyReLU());

generator.add(tf.layers.conv2dTranspose({
    kernelSize: 5,
    filters: 1,
    strides: 2,
    padding: 'same',
    useBias: false,
    activation: 'tanh'
}));
```

La red generadora toma como entrada un vector de ruido y genera una imagen similar al conjunto de datos MNIST.

A continuación, necesitamos crear la red discriminadora. La red discriminadora tomará como entrada una imagen y generará un valor que indica si la imagen es real o falsa.

Podemos crear la red discriminadora usando el siguiente código:

```javascript
const discriminator = tf.sequential();

discriminator.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 64,
    strides: 2,
    padding: 'same',
    inputShape: [28, 28, 1]
}));
discriminator.add(tf.layers.leakyReLU());
discriminator.add(tf.layers.dropout({rate: 0.3}));

discriminator.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 128,
    strides: 2,
    padding: 'same'
}));
discriminator.add(tf.layers.leakyReLU());
discriminator.add(tf.layers.dropout({rate: 0.3}));

discriminator.add(tf.layers.flatten());
discriminator.add(tf.layers.dense({units: 1, activation: 'sigmoid'}));
```

La red discriminadora toma como entrada una imagen y emite un valor que indica si la imagen es real o falsa.

## Entrenamiento del DC-GAN

Ahora que tenemos las redes del generador y el discriminador, podemos comenzar a entrenar el DC-GAN.

Primero, necesitamos definir la función de pérdida. La función de pérdida se utiliza para medir el rendimiento de la DC-GAN.

Podemos definir la función de pérdida usando el siguiente código:

```javascript
function dLoss(yTrue, yPred) {
    return tf.losses.sigmoidCrossEntropy(yTrue, yPred);
}

function gLoss(yTrue, yPred) {
    return tf.losses.sigmoidCrossEntropy(yTrue, yPred);
}
```

La función de pérdida se utiliza para medir el rendimiento de la DC-GAN.

A continuación, necesitamos definir los optimizadores. Los optimizadores se utilizan para actualizar los pesos de las redes generadora y discriminadora.

Podemos definir los optimizadores usando el siguiente código:

```javascript
const dOptimizer = tf.train.RMSPropOptimizer(0.0003);
const gOptimizer = tf.train.RMSPropOptimizer(0.0001);
```

Los optimizadores se utilizan para actualizar los pesos de las redes generadora y discriminadora.

Ahora, podemos comenzar a entrenar el DC-GAN. Entrenaremos el DC-GAN durante 100 épocas.

Podemos entrenar el DC-GAN usando el siguiente código:

```javascript
async function train() {
    for (let i = 0; i < 100; i++) {
        // Train the discriminator
        let dLosses = [];
        for (let j = 0; j < 10; j++) {
            const noise = tf.randomNormal([BATCH_SIZE, 100]);
            const generatedImages = generator.predict(noise);
            const realImages = tf.data.Dataset.fromTensorSlices(images).batch(BATCH_SIZE).take(BATCH_SIZE).toArray();
            const dRealLabels = tf.ones([BATCH_SIZE, 1]);
            const dFakeLabels = tf.zeros([BATCH_SIZE, 1]);
            const dLossReal = dLoss(dRealLabels, discriminator.predict(realImages));
            const dLossFake = dLoss(dFakeLabels, discriminator.predict(generatedImages));
            const dLoss = dLossReal + dLossFake;
            dLosses.push(dLoss);
            dOptimizer.minimize(dLoss);
        }
        const dAvgLoss = tf.mean(dLosses);
        
        // Train the generator
        const noise = tf.randomNormal([BATCH_SIZE, 100]);
        const gLabels = tf.ones([BATCH_SIZE, 1]);
        const gLoss = gLoss(gLabels, discriminator.predict(generator.predict(noise)));
        gOptimizer.minimize(gLoss);
        
        // Log the losses
        if (i % 10 === 0) {
            console.log(`Epoch: ${i}`);
            console.log(`dLoss: ${dLoss.dataSync()[0]}`);
            console.log(`gLoss: ${gLoss.dataSync()[0]}`);
        }
    }
}

train();
```

Este código entrenará el DC-GAN durante 100 épocas.

## Generación de nuevas imágenes

Ahora que el DC-GAN está entrenado, podemos usarlo para generar nuevas imágenes.

Primero, necesitamos generar un vector de ruido. Esto lo podemos hacer usando el siguiente código:

```javascript
const noise = tf.randomNormal([1, 100]);
```

A continuación, necesitamos usar la red del generador para generar una nueva imagen a partir del vector de ruido. Esto lo podemos hacer usando el siguiente código:

```javascript
const generatedImage = generator.predict(noise);
```

Finalmente, podemos visualizar la imagen generada usando el siguiente código:

```javascript
const imageTensor = generatedImage.reshape([28, 28]);
const imageData = imageTensor.dataSync();
const canvas = document.createElement('canvas');
canvas.width = 28;
canvas.height = 28;
const ctx = canvas.getContext('2d');
const imageDataArray = Array.from(imageData);
imageDataArray.forEach((value, index) => {
    const i = Math.floor(index / 28);
    const j = index % 28;
    ctx.fillStyle = `rgb(${value}, ${value}, ${value})`;
    ctx.fillRect(j, i, 1, 1);
});
document.body.appendChild(canvas);
```

Este código generará una nueva imagen a partir del vector de ruido.

## Conclusión

En este tutorial, hemos visto cómo construir un DC-GAN en TensorFlow.js y Node.js. También hemos visto cómo usar el DC-GAN para generar nuevas imágenes.