---
title: 050: Optimización de Adam con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T18:36:28.043Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:36:26.413Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [050: Adam Optimization with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/050-adam-optimization-with-tensorflow-js-and-node-js)
{.links-list}


# Optimización de Adam con TensorFlow.js y Node.js

En esta publicación, exploraremos cómo usar el algoritmo de optimización de Adam con TensorFlow.js y Node.js. Adam es un algoritmo de optimización que se puede utilizar para entrenar redes neuronales. Adam es una combinación de los algoritmos de optimización AdaGrad y RMSProp.

La optimización de Adam es un método computacionalmente eficiente para entrenar redes neuronales. Adam es muy adecuado para entrenar redes neuronales profundas. Adam se puede utilizar con cualquier función de pérdida diferenciable.

## Empezando

Para comenzar, necesitaremos instalar las dependencias de TensorFlow.js y Node.js. Podemos instalar TensorFlow.js y Node.js usando los siguientes comandos:

```
npm install @tensorflow/tfjs
npm install node
```

## Definición del modelo

A continuación, debemos definir el modelo que queremos entrenar. Usaremos una red neuronal simple con una capa oculta. La capa oculta tendrá 100 neuronas. Podemos definir el modelo usando el siguiente código:

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({units: 100, inputShape: [1], activation: 'relu'}));
model.add(tf.layers.dense({units: 1, activation: 'linear'}));
```

## Compilando el modelo

Después de haber definido el modelo, necesitamos compilarlo. Compilar el modelo nos permite especificar el optimizador y la función de pérdida que queremos usar. Usaremos el optimizador de Adam y la función de pérdida de error cuadrático medio. Podemos compilar el modelo usando el siguiente código:

```javascript
model.compile({optimizer: 'adam', loss: 'meanSquaredError'});
```

## Entrenamiento del modelo

Ahora que hemos compilado el modelo, podemos entrenarlo. Entrenaremos el modelo durante 10 épocas. Una época es una iteración sobre todo el conjunto de datos de entrenamiento. Podemos entrenar el modelo usando el siguiente código:

```javascript
model.fit(x, y, {epochs: 10});
```

## Evaluación del modelo

Después de entrenar el modelo, podemos evaluarlo. Evaluaremos el modelo en un conjunto de datos de prueba. Podemos evaluar el modelo usando el siguiente código:

```javascript
model.evaluate(xTest, yTest);
```

## Haciendo predicciones

Finalmente, podemos usar el modelo entrenado para hacer predicciones. Haremos predicciones sobre un nuevo conjunto de datos. Podemos hacer predicciones usando el siguiente código:

```javascript
model.predict(xPred);
```

## Conclusión

En esta publicación, hemos visto cómo usar el algoritmo de optimización de Adam con TensorFlow.js y Node.js. Adam es un algoritmo de optimización eficiente que se puede utilizar para entrenar redes neuronales. Adam se puede utilizar con cualquier función de pérdida diferenciable.