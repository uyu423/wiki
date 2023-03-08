---
title: 052: Devoluciones de llamadas personalizadas con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T19:04:49.223Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:04:47.423Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [052: Custom Callbacks with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/052-custom-callbacks-with-tensorflow-js-and-node-js)
{.links-list}


# Devoluciones de llamadas personalizadas con TensorFlow.js y Node.js

En esta publicación, aprenderemos cómo crear devoluciones de llamadas personalizadas con TensorFlow.js y Node.js.

TensorFlow.js es una poderosa herramienta para el aprendizaje automático en JavaScript. Le permite crear, entrenar e implementar modelos de aprendizaje automático en el navegador o en Node.js.

Node.js es un tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript en su servidor. Node.js también es una plataforma importante para TensorFlow.js, ya que le permite implementar modelos de aprendizaje automático en producción.

Crear una devolución de llamada personalizada con TensorFlow.js es una excelente manera de ampliar la funcionalidad de sus modelos de aprendizaje automático. Las devoluciones de llamada le permiten definir funciones personalizadas que se ejecutan en puntos específicos durante el proceso de capacitación. Por ejemplo, puede usar una devolución de llamada para rastrear la pérdida de entrenamiento o para guardar el modelo después de cada época.

En esta publicación, aprenderemos cómo crear una devolución de llamada personalizada con TensorFlow.js y Node.js. También aprenderemos a usar la devolución de llamada para rastrear la pérdida de entrenamiento y guardar el modelo después de cada época.

## ¿Qué es una devolución de llamada?

Una devolución de llamada es una función que se ejecuta en un punto específico durante el proceso de entrenamiento. Las devoluciones de llamada son una forma poderosa de ampliar la funcionalidad de sus modelos de aprendizaje automático.

Hay dos tipos de devoluciones de llamada en TensorFlow.js:

* **Devoluciones de llamada de capas:** Estas devoluciones de llamada se ejecutan cuando se crea una capa.
* **Devoluciones de llamada del modelo:** estas devoluciones de llamada se ejecutan cuando se compila el modelo y comienza el entrenamiento.

En esta publicación, nos centraremos en las devoluciones de llamada del modelo.

## Creación de una devolución de llamada personalizada

Crear una devolución de llamada personalizada con TensorFlow.js es simple. Primero, necesitamos crear un nuevo archivo JavaScript e importar la biblioteca TensorFlow.js.

A continuación, necesitamos crear una nueva clase que amplíe la clase Callback. Esta clase contendrá nuestras funciones de devolución de llamada personalizadas.

En nuestro ejemplo, crearemos una devolución de llamada personalizada que rastrea la pérdida de entrenamiento y guarda el modelo después de cada época.

```javascript
const tf = require('@tensorflow/tfjs');

class CustomCallback extends tf.Callback {
  onTrainBegin(logs) {
    // This function is executed when training begins.
    // We can use it to initialize our custom variables.
    this.losses = [];
  }

  onTrainEnd(logs) {
    // This function is executed when training ends.
    // We can use it to save our custom variables.
    console.log('Final loss: ', this.losses[-1]);
  }

  onBatchEnd(batch, logs) {
    // This function is executed at the end of each training batch.
    // We can use it to track the training loss.
    this.losses.push(logs.loss);
  }

  onEpochEnd(epoch, logs) {
    // This function is executed at the end of each training epoch.
    // We can use it to save the model.
    console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    this.model.save(`model_at_epoch_${epoch}.h5`);
  }
}
```

En este ejemplo, hemos creado cuatro funciones de devolución de llamada personalizadas:

* onTrainBegin: Esta función se ejecuta cuando comienza el entrenamiento. Podemos usarlo para inicializar nuestras variables personalizadas.
* onTrainEnd: Esta función se ejecuta cuando finaliza el entrenamiento. Podemos usarlo para guardar nuestras variables personalizadas.
* onBatchEnd: esta función se ejecuta al final de cada lote de entrenamiento. Podemos usarlo para rastrear la pérdida de entrenamiento.
* onEpochEnd: Esta función se ejecuta al final de cada época de entrenamiento. Podemos usarlo para guardar el modelo.

## Uso de la devolución de llamada personalizada

Ahora que hemos creado nuestra devolución de llamada personalizada, veamos cómo usarla.

Primero, necesitamos crear un nuevo modelo TensorFlow.js. En este ejemplo, usaremos un modelo secuencial simple.

A continuación, debemos compilar el modelo utilizando la devolución de llamada personalizada.

Finalmente, podemos entrenar el modelo usando el método de ajuste.

```javascript
const model = tf.sequential();

model.compile({
  optimizer: 'sgd',
  loss: 'binaryCrossentropy',
  callbacks: new CustomCallback()
});

model.fit(x, y, {
  epochs: 10
});
```

En este ejemplo, hemos usado la devolución de llamada personalizada para rastrear la pérdida de entrenamiento y guardar el modelo después de cada época.

## Conclusión

En esta publicación, aprendimos cómo crear devoluciones de llamadas personalizadas con TensorFlow.js y Node.js. También aprendimos cómo usar la devolución de llamada para rastrear la pérdida de entrenamiento y guardar el modelo después de cada época.

Crear devoluciones de llamada personalizadas es una excelente manera de ampliar la funcionalidad de sus modelos de aprendizaje automático. Las devoluciones de llamada le permiten definir funciones personalizadas que se ejecutan en puntos específicos durante el proceso de capacitación.

Si está interesado en obtener más información sobre TensorFlow.js, asegúrese de consultar el sitio web de TensorFlow.js (https://js.tensorflow.org/).