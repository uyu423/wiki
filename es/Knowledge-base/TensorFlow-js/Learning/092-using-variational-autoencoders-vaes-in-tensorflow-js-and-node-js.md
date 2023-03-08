---
title: 092: Uso de codificadores automáticos variacionales (VAEs) en TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T04:36:31.914Z
tags: 
editor: markdown
dateCreated: 2023-02-03T04:36:27.084Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [092: Using Variational Autoencoders (VAEs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/092-using-variational-autoencoders-vaes-in-tensorflow-js-and-node-js)
{.links-list}


# Uso de codificadores automáticos variacionales (VAEs) en TensorFlow.js y Node.js

Los codificadores automáticos variacionales (VAEs) son una herramienta poderosa para aprender representaciones latentes de datos. En esta publicación, veremos cómo usar un VAE para aprender una representación latente de datos MNIST en TensorFlow.js y Node.js.

## ¿Qué es un VAE?

Un VAE es un modelo probabilístico que se puede utilizar para aprender una representación latente de datos. Los VAE son similares a los codificadores automáticos en que aprenden a comprimir datos en un espacio latente. Sin embargo, los VAE son modelos probabilísticos, lo que significa que pueden usarse para generar nuevas muestras de datos a partir del espacio latente.

## ¿Cómo funcionan los VAE?

Los VAE funcionan mediante el aprendizaje de una representación latente de datos. El espacio latente es un espacio de menor dimensión que captura las características esenciales de los datos. Luego, el VAE usa este espacio latente para generar nuevas muestras de datos.

## ¿Cómo uso un VAE en TensorFlow.js?

Para usar un VAE en TensorFlow.js, primero debe instalar la biblioteca TensorFlow.js. Puede hacer esto usando el administrador de paquetes de Node.js:

```
npm install @tensorflow/tfjs
```

A continuación, debe cargar los datos MNIST. Puede hacer esto usando la API tf.data.Dataset:

```javascript
const mnistData = tf.data.dataset.mnist({
  train: true,
  testData: false
});
```

Ahora, necesita crear el VAE. Puede hacer esto usando la función tf.layers.vae():

```javascript
const vae = tf.layers.vae({
  encoder: {
    inputShape: [28, 28, 1],
    latentDimensions: 2
  },
  decoder: {
    outputShape: [28, 28, 1]
  }
});
```

Finalmente, necesitas entrenar el VAE. Puedes hacer esto usando el método fit():

```javascript
vae.fit(mnistData, {
  epochs: 10
});
```

## ¿Cómo uso un VAE en Node.js?

Para usar un VAE en Node.js, primero debe instalar la biblioteca TensorFlow.js. Puede hacer esto usando el administrador de paquetes de Node.js:

```
npm install @tensorflow/tfjs
```

A continuación, debe cargar los datos MNIST. Puede hacer esto usando la API tf.data.Dataset:

```javascript
const mnistData = tf.data.dataset.mnist({
  train: true,
  testData: false
});
```

Ahora, necesita crear el VAE. Puede hacer esto usando la función tf.layers.vae():

```javascript
const vae = tf.layers.vae({
  encoder: {
    inputShape: [28, 28, 1],
    latentDimensions: 2
  },
  decoder: {
    outputShape: [28, 28, 1]
  }
});
```

Finalmente, necesitas entrenar el VAE. Puedes hacer esto usando el método fit():

```javascript
vae.fit(mnistData, {
  epochs: 10
});
```

## Conclusión

En esta publicación, hemos visto cómo usar un VAE para aprender una representación latente de datos MNIST en TensorFlow.js y Node.js. Los VAE son una herramienta poderosa para aprender representaciones latentes de datos.