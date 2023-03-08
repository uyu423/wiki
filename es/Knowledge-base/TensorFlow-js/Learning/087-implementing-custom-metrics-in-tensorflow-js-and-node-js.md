---
title: 087: Implementación de métricas personalizadas en TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T03:17:26.668Z
tags: 
editor: markdown
dateCreated: 2023-02-03T03:17:25.102Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [087: Implementing Custom Metrics in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/087-implementing-custom-metrics-in-tensorflow-js-and-node-js)
{.links-list}


# Implementación de métricas personalizadas en TensorFlow.js y Node.js

En esta publicación, aprenderemos cómo implementar métricas personalizadas en TensorFlow.js y Node.js.

## ¿Qué son las métricas personalizadas?

Las métricas personalizadas son métricas definidas por el usuario que se pueden usar para realizar un seguimiento del rendimiento de un modelo de aprendizaje automático. Se pueden usar para rastrear cualquier cosa, desde la precisión del modelo hasta el número de iteraciones de entrenamiento.

## ¿Por qué usar métricas personalizadas?

Las métricas personalizadas se pueden usar para realizar un seguimiento del rendimiento de un modelo de aprendizaje automático de una manera más granular que las métricas integradas. También se pueden usar para realizar un seguimiento del rendimiento de un modelo en varias ejecuciones de entrenamiento.

## ¿Cómo implementar métricas personalizadas en TensorFlow.js?

TensorFlow.js proporciona una clase CustomCallback que se puede usar para implementar métricas personalizadas. La clase CustomCallback toma una función como argumento. Esta función toma dos argumentos:

- El primer argumento es el lote actual de datos.
- El segundo argumento es la época actual.

La función debe devolver un objeto con el nombre de la métrica y el valor de la métrica.

Aquí hay un ejemplo de cómo usar la clase CustomCallback para rastrear la precisión de un modelo de aprendizaje automático:

```javascript
const model = tf.sequential();

model.add(tf.layers.dense({units: 100, activation: 'relu', inputShape: [784]}));
model.add(tf.layers.dense({units: 10, activation: 'softmax'}));

model.compile({
  optimizer: 'sgd',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});

const callback = tf.callbacks.CustomCallback((batch, epoch) => {
  const acc = model.evaluate(batch.x, batch.y)[1].dataSync()[0];
  console.log('Accuracy: ', acc);
  return {'accuracy': acc};
});

model.fit(x, y, {
  epochs: 10,
  callbacks: [callback]
});
```

En este ejemplo, hemos definido una métrica personalizada para rastrear la precisión del modelo. La clase CustomCallback llamará a la función que hemos definido al final de cada época. La función evaluará el modelo en el lote actual de datos y devolverá la precisión.

## ¿Cómo implementar métricas personalizadas en Node.js?

Node.js proporciona una funcionalidad similar a TensorFlow.js con el uso de las palabras clave async/await.

Aquí hay un ejemplo de cómo usar async/await para rastrear la precisión de un modelo de aprendizaje automático:

```javascript
const model = tf.sequential();

model.add(tf.layers.dense({units: 100, activation: 'relu', inputShape: [784]}));
model.add(tf.layers.dense({units: 10, activation: 'softmax'}));

model.compile({
  optimizer: 'sgd',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});

async function run() {
  for (let i = 0; i < 10; i++) {
    const res = await model.fit(x, y);
    console.log('Accuracy: ', res.history.acc);
  }
}

run();
```

En este ejemplo, hemos definido una métrica personalizada para rastrear la precisión del modelo. Las palabras clave async/await llamarán a la función que hemos definido al final de cada época. La función evaluará el modelo en el lote actual de datos y devolverá la precisión.