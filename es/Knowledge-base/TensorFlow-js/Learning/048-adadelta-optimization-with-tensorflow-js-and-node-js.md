---
title: 048: Optimización Adadelta con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T18:17:52.336Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:17:47.724Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [048: Adadelta Optimization with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/048-adadelta-optimization-with-tensorflow-js-and-node-js)
{.links-list}


# Optimización Adadelta con TensorFlow.js y Node.js

Adadelta es un algoritmo de optimización que se puede utilizar en lugar del descenso de gradiente estocástico tradicional (SGD) para entrenar redes neuronales profundas. Es un método más robusto y eficiente para entrenar redes neuronales y se puede usar con TensorFlow.js y Node.js.

## ¿Qué es Adadelta?

Adadelta es un algoritmo de optimización de la tasa de aprendizaje adaptativo que es muy adecuado para entrenar redes neuronales profundas. Fue propuesto en 2012 por Matthew D. Zeiler y Rob Fergus en el artículo "[ADADELTA: An Adaptive Learning Rate Method](https://arxiv.org/abs/1212.5701)", que ganó el Premio al Mejor Artículo en el International Conferencia sobre Representaciones de Aprendizaje (ICLR) en 2013.

Adadelta es una extensión de Adagrad, otro algoritmo de optimización de la tasa de aprendizaje adaptativo propuesto en 2011 por Duchi et al. en el artículo "[Métodos adaptativos de subgradiente para el aprendizaje en línea y la optimización estocástica](https://www.jmlr.org/papers/volume12/duchi11a/duchi11a.pdf)".

Tanto Adagrad como Adadelta se basan en el concepto de tasas de aprendizaje por parámetro, que se adaptan en función del gradiente de la función de pérdida con respecto a los parámetros.

## ¿Cómo funciona Adadelta?

El algoritmo de optimización de Adadelta funciona calculando la tasa de aprendizaje por parámetro para cada parámetro en la red neuronal. La tasa de aprendizaje se adapta en función del gradiente de la función de pérdida con respecto a los parámetros.

El algoritmo tiene dos parámetros:

- `rho`: Un parámetro que controla la tasa de caída de la tasa de aprendizaje. Normalmente se utiliza un valor de `0,95`.
- `epsilon`: Un pequeño parámetro que se utiliza para la estabilidad numérica. Normalmente se utiliza un valor de `1e-6`.

El algoritmo de optimización de Adadelta se puede resumir de la siguiente manera:

1. Inicialice las tasas de aprendizaje por parámetro `Delta_p` a `0`.
2. Para cada ejemplo de entrenamiento `x` y objetivo correspondiente `y`:
    1. Calcule el gradiente de la función de pérdida con respecto a los parámetros `Delta_p = gradiente (pérdida (x, y), p)`.
    2. Actualice las tasas de aprendizaje por parámetro: `Delta_p = rho * Delta_p + (1 - rho) * Delta_p^2`.
    3. Actualice los parámetros: `p = p - tasa_de_aprendizaje * Delta_p / sqrt(épsilon + gradientes_acumulados)`.

## Adadelta contra SGD

Adadelta es un método más robusto y eficiente para entrenar redes neuronales que el descenso de gradiente estocástico tradicional (SGD).

SGD es un algoritmo de optimización popular para entrenar redes neuronales, pero puede ser difícil ajustar la tasa de aprendizaje. Si la tasa de aprendizaje es demasiado baja, el proceso de formación será lento. Si la tasa de aprendizaje es demasiado alta, el proceso de formación puede divergir.

Adadelta no requiere que se especifique una tasa de aprendizaje. La tasa de aprendizaje se adapta automáticamente en función del gradiente de la función de pérdida. Esto lo hace más robusto y eficiente que SGD.

## Adadelta con TensorFlow.js y Node.js

Adadelta se puede usar con TensorFlow.js y Node.js.

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. Node.js es un tiempo de ejecución de JavaScript que se puede usar para ejecutar aplicaciones TensorFlow.js.

Para usar Adadelta con TensorFlow.js y Node.js, debe instalar los módulos `tensorflow` y `@tensorflow/tfjs-node`.

```
$ npm install --save tensorflow
$ npm install --save @tensorflow/tfjs-node
```

Luego, puede usar la función `tf.train.adadelta` para entrenar una red neuronal usando el algoritmo de optimización Adadelta.

```javascript
const tf = require('tensorflow');

// Define the neural network.
const model = tf.sequential();
model.add(tf.layers.dense({ units: 10, inputShape: [5], activation: 'relu' }));
model.add(tf.layers.dense({ units: 1, activation: 'sigmoid' }));

// Compile the model.
model.compile({
  loss: 'binaryCrossentropy',
  optimizer: tf.train.adadelta(),
  metrics: ['accuracy']
});

// Train the model.
model.fit({ x: tf.ones([100, 5]), y: tf.zeros([100]) }, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    }
  }
});
```

## Conclusión

En este post hemos visto cómo usar el algoritmo de optimización Adadelta con TensorFlow.js y Node.js. Adadelta es un método más robusto y eficiente para entrenar redes neuronales que el descenso de gradiente estocástico tradicional (SGD).