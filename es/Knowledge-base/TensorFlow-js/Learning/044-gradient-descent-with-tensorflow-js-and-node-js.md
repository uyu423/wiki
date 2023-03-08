---
title: 044: Descenso de gradiente con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T17:18:33.793Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:18:32.060Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [044: Gradient Descent with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/044-gradient-descent-with-tensorflow-js-and-node-js)
{.links-list}


# 044: Descenso de gradiente con TensorFlow.js y Node.js

El descenso de gradiente es un algoritmo de optimización que se utiliza para encontrar los valores de los parámetros (como pesos y sesgos) que minimizan una función de costo. Es un algoritmo popular para entrenar redes neuronales.

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. Node.js es un tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript en un servidor.

En este tutorial, usaremos TensorFlow.js y Node.js para entrenar una red neuronal simple para realizar una regresión lineal. Usaremos el descenso de gradiente para encontrar los valores óptimos para los pesos y sesgos de la red.

## ¿Qué es la regresión lineal?

La regresión lineal es un algoritmo de aprendizaje automático que se utiliza para predecir un valor continuo. Por ejemplo, podríamos usar la regresión lineal para predecir el precio de una casa según su tamaño, la cantidad de habitaciones y la cantidad de baños.

La regresión lineal es un tipo de aprendizaje supervisado, lo que significa que debemos proporcionar al algoritmo datos de entrenamiento. Los datos de entrenamiento consisten en un conjunto de valores de entrada (x) y los valores de salida correspondientes (y). Para nuestro ejemplo del precio de la vivienda, los valores de entrada podrían ser el tamaño, la cantidad de dormitorios y la cantidad de baños, y el valor de salida sería el precio.

## ¿Cómo funciona la regresión lineal?

La regresión lineal funciona al encontrar un conjunto de pesos (w) y sesgos (b) que minimizan el error entre los valores predichos (ŷ) y los valores reales (y).

![Regresión lineal](https://cdn-images-1.medium.com/max/1600/1*d7Cg5UC5tM7GtLjTvW0MzA.png)

Los valores pronosticados se calculan tomando los valores de entrada (x) y multiplicándolos por los pesos (w), y luego sumando los sesgos (b).

![Valores previstos](https://cdn-images-1.medium.com/max/1600/1*j_q-F1lrVxKbV-_d7JKV2w.png)

El error se calcula tomando la diferencia entre los valores predichos (ŷ) y los valores reales (y).

![Error](https://cdn-images-1.medium.com/max/1600/1*7VtEOzAj_sXXuTzXrT7yYQ.png)

Luego podemos usar el descenso de gradiente para encontrar los pesos y sesgos que minimizan el error.

## ¿Qué es el descenso de gradiente?

El descenso de gradiente es un algoritmo de optimización que se utiliza para encontrar los valores de los parámetros (como pesos y sesgos) que minimizan una función de costo.

![Función de costo](https://cdn-images-1.medium.com/max/1600/1*Xu7B5y9gp0iL5ooBj7LtWw.png)

La función de costo es una medida de qué tan lejos están los valores pronosticados (ŷ) de los valores reales (y). Queremos encontrar los pesos y sesgos que minimizan la función de costo.

![Pesos y sesgos](https://cdn-images-1.medium.com/max/1600/1*n6sVxWAz7VUgX6Sj7K1vUw.png)

El descenso de gradiente funciona mediante la actualización iterativa de los pesos y sesgos en la dirección que minimiza la función de costo. El tamaño de la actualización está determinado por la tasa de aprendizaje.

![Descenso de gradiente](https://cdn-images-1.medium.com/max/1600/1*jw7UwKLnA0sCgq_QPV-_lA.png)

## Implementando el Descenso de Gradiente en TensorFlow.js

Ahora que hemos visto cómo funciona el descenso de gradiente, veamos cómo implementarlo en TensorFlow.js.

Primero, necesitamos definir los valores de entrada (x), los valores de salida (y) y los valores iniciales para los pesos (w) y los sesgos (b).

```javascript
// Define the input values
const x = tf.tensor([
  [1, 2, 3, 4],
  [2, 3, 4, 5],
  [3, 4, 5, 6],
  [4, 5, 6, 7]
]);

// Define the output values
const y = tf.tensor([
  [2],
  [4],
  [6],
  [8]
]);

// Define the initial values for the weights and biases
const w = tf.variable(tf.zeros([4, 1]));
const b = tf.variable(tf.zeros([1]));
```

A continuación, necesitamos definir la función de costo. Usaremos la función de costo del error cuadrático medio.

```javascript
// Define the cost function
function cost(pred, labels) {
  const diff = pred.sub(labels);
  const sqrDiff = diff.square();
  const meanSqrDiff = sqrDiff.mean();
  return meanSqrDiff;
}
```

Ahora, podemos definir el algoritmo de descenso de gradiente. Actualizaremos iterativamente los pesos y sesgos en la dirección que minimice la función de costo.

```javascript
// Define the gradient descent algorithm
async function train(x, y, w, b, epochs, learningRate) {
  for (let i = 0; i < epochs; i++) {
    // Calculate the predicted values
    const pred = x.matMul(w).add(b);

    // Calculate the cost
    const c = cost(pred, y);

    // Print the cost
    console.log("Epoch: " + i + " Cost: " + c.dataSync()[0]);

    // Calculate the gradients
    const grads = tf.grads(c, [w, b]);
    const dw = grads[0];
    const db = grads[1];

    // Update the weights and biases
    w.sub(dw.mul(learningRate));
    b.sub(db.mul(learningRate));
  }
}
```

Finalmente, podemos llamar a la función `train` para entrenar el modelo. Entrenaremos el modelo durante 100 épocas con una tasa de aprendizaje de 0,1.

```javascript
// Train the model
train(x, y, w, b, 100, 0.1);
```

## Entrenamiento del modelo

Ahora que hemos visto cómo implementar el descenso de gradiente en TensorFlow.js, veamos cómo usarlo para entrenar una red neuronal para realizar una regresión lineal.

Primero, necesitamos definir los valores de entrada (x), los valores de salida (y) y los valores iniciales para los pesos (w) y los sesgos (b).

```javascript
// Define the input values
const x = tf.tensor([
  [1, 2, 3, 4],
  [2, 3, 4, 5],
  [3, 4, 5, 6],
  [4, 5, 6, 7]
]);

// Define the output values
const y = tf.tensor([
  [2],
  [4],
  [6],
  [8]
]);

// Define the initial values for the weights and biases
const w = tf.variable(tf.zeros([4, 1]));
const b = tf.variable(tf.zeros([1]));
```

A continuación, necesitamos definir la función de costo. Usaremos la función de costo del error cuadrático medio.

```javascript
// Define the cost function
function cost(pred, labels) {
  const diff = pred.sub(labels);
  const sqrDiff = diff.square();
  const meanSqrDiff = sqrDiff.mean();
  return meanSqrDiff;
}
```

Ahora, podemos definir el algoritmo de descenso de gradiente. Actualizaremos iterativamente los pesos y sesgos en la dirección que minimice la función de costo.

```javascript
// Define the gradient descent algorithm
async function train(x, y, w, b, epochs, learningRate) {
  for (let i = 0; i < epochs; i++) {
    // Calculate the predicted values
    const pred = x.matMul(w).add(b);

    // Calculate the cost
    const c = cost(pred, y);

    // Print the cost
    console.log("Epoch: " + i + " Cost: " + c.dataSync()[0]);

    // Calculate the gradients
    const grads = tf.grads(c, [w, b]);
    const dw = grads[0];
    const db = grads[1];

    // Update the weights and biases
    w.sub(dw.mul(learningRate));
    b.sub(db.mul(learningRate));
  }
}
```

Finalmente, podemos llamar a la función `train` para entrenar el modelo. Entrenaremos el modelo durante 100 épocas con una tasa de aprendizaje de 0,1.

```javascript
// Train the model
train(x, y, w, b, 100, 0.1);
```

## Probando el modelo

Ahora que hemos entrenado el modelo, veamos cómo se comporta en algunos datos de prueba.

Primero, necesitamos definir los datos de prueba.

```javascript
// Define the test data
const xTest = tf.tensor([
  [5, 6, 7, 8],
  [6, 7, 8, 9],
  [7, 8, 9, 10],
  [8, 9, 10, 11]
]);

// Define the expected output values
const yTest = tf.tensor([
  [10],
  [12],
  [14],
  [16]
]);
```

A continuación, necesitamos calcular los valores predichos.

```javascript
// Calculate the predicted values
const pred = xTest.matMul(w).add(b);
```

Finalmente, podemos comparar los valores pronosticados con los valores de salida esperados.

```javascript
// Compare the predicted values to the expected output values
pred.print();
yTest.print();
```

## Conclusión

En este tutorial, hemos visto cómo usar el descenso de gradiente para entrenar una red neuronal para realizar una regresión lineal. También vimos cómo implementar el descenso de gradiente en TensorFlow.js y cómo usarlo para entrenar una red neuronal.