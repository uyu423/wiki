---
title: 041: Overfitting y Regularización con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T16:36:23.356Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:36:21.772Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [041: Overfitting and Regularization with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/041-overfitting-and-regularization-with-tensorflow-js-and-node-js)
{.links-list}


# Sobreajuste y Regularización con TensorFlow.js y Node.js

En el aprendizaje automático, el sobreajuste es un fenómeno en el que un modelo funciona bien con los datos de entrenamiento, pero no con los datos de prueba. Esto ocurre cuando el modelo ha memorizado los datos de entrenamiento demasiado de cerca y no generaliza bien los datos nuevos.

Una forma de combatir el sobreajuste es a través de la regularización, que es el proceso de agregar restricciones a un modelo para evitar que se sobreajuste. En esta publicación, exploraremos dos métodos de regularización, regularización de peso y regularización de abandono, y cómo implementarlos en TensorFlow.js y Node.js.

## Regularización de peso

La regularización del peso es un método para restringir los pesos de un modelo para evitar el sobreajuste. Hay dos tipos comunes de regularización de peso:

* Regularización L1: restringe los pesos para que estén cerca de cero
* Regularización L2: restringe los pesos para que tengan una pequeña magnitud

En TensorFlow.js, la regularización de peso se puede implementar especificando la fuerza de regularización `l1` o `l2` al crear el modelo:

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({
  units: 100,
  kernelRegularizer: tf.regularizers.l2({l2: 0.01}),
  inputShape: [inputShape]
}));
```

En el ejemplo anterior, estamos usando la regularización L2 con una fuerza de 0.01.

## Regularización de la deserción

La regularización de la deserción es un método para establecer aleatoriamente una fracción de los pesos en un modelo en cero. Esto obliga al modelo a aprender a funcionar con menos pesos y evita que se sobreajuste.

En TensorFlow.js, la regularización de la deserción se puede implementar especificando `dropoutRate` al crear el modelo:

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({
  units: 100,
  dropoutRate: 0.1,
  inputShape: [inputShape]
}));
```

En el ejemplo anterior, estamos utilizando abandono con una tasa de 0,1, lo que significa que el 10% de los pesos se establecerán en cero.

## Conclusión

En esta publicación, exploramos dos métodos de regularización, regularización de peso y regularización de abandono, y cómo implementarlos en TensorFlow.js y Node.js. La regularización es una herramienta poderosa para combatir el sobreajuste y se puede usar junto con otros métodos, como la validación cruzada.