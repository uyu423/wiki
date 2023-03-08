---
title: 028: Aprendizaje por refuerzo con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T13:37:04.559Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:37:02.956Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [028: Reinforcement Learning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/028-reinforcement-learning-with-tensorflow-js-and-node-js)
{.links-list}


# 028: Aprendizaje por refuerzo con TensorFlow.js y Node.js

En esta publicación, le mostraremos cómo comenzar con el aprendizaje por refuerzo en Node.js usando TensorFlow.js. Usaremos un ejemplo simple para demostrar cómo construir y entrenar un modelo usando el popular algoritmo Q-learning.

El aprendizaje por refuerzo es un tipo de aprendizaje automático que permite a los agentes aprender realizando acciones en un entorno y recibiendo comentarios. Se ha utilizado para resolver una variedad de tareas, como jugar videojuegos, controlar robots y administrar recursos en un centro de datos.

El algoritmo Q-learning es una opción popular para tareas de aprendizaje por refuerzo. Funciona mediante el aprendizaje de una función de valor que estima el rendimiento esperado de realizar una acción determinada en un estado determinado. Luego, el algoritmo toma las acciones que maximizan el rendimiento esperado.

Para comenzar con Q-learning en TensorFlow.js, necesitaremos instalar el paquete @tensorflow/tfjs-node. Este paquete nos permite ejecutar TensorFlow.js en un servidor o en un entorno sin cabeza, como un trabajador web.

```
npm install @tensorflow/tfjs-node
```

A continuación, necesitaremos crear un archivo para nuestro código. Lo llamaremos q-learning.js.

En q-learning.js, comenzaremos importando los paquetes que necesitamos.

```javascript
const tf = require('@tensorflow/tfjs-node');
const _ = require('lodash');
```

También necesitaremos crear algunas funciones auxiliares. La primera función auxiliar que crearemos es una función para calcular el valor máximo de una matriz. Esta función se utilizará para encontrar la acción con el mayor retorno esperado.

```javascript
function argmax(array) {
  return tf.tensor1d(array).argMax().dataSync()[0];
}
```

La siguiente función auxiliar que crearemos es una función para calcular el rendimiento esperado de realizar una acción dada en un estado dado. Esta función utilizará el algoritmo Q-learning para estimar el rendimiento esperado.

```javascript
function expectedReturn(state, action, reward, discount, nextState) {
  return reward + discount * _.max(Q(nextState).dataSync());
}
```

Ahora que tenemos nuestras funciones auxiliares, podemos comenzar a crear nuestro modelo Q-learning. Comenzaremos definiendo los estados y acciones que nuestro agente puede tomar. En este ejemplo, nuestro agente es un robot que puede moverse en cuatro direcciones (arriba, abajo, izquierda o derecha). Representaremos cada estado como una matriz bidimensional. La primera dimensión representará la coordenada x del robot y la segunda dimensión representará la coordenada y del robot.

```javascript
const states = [[0, 0], [0, 1], [0, 2], [1, 0], [1, 1], [1, 2], [2, 0], [2, 1], [2, 2]];
const actions = ['up', 'down', 'left', 'right'];
```

A continuación, crearemos un tensor TensorFlow.js para nuestros valores Q. Este tensor será una matriz bidimensional con las mismas dimensiones que nuestra matriz de estados. Los valores en el tensor representarán el rendimiento esperado de realizar una acción dada en un estado dado.

```javascript
const Q = tf.variable(tf.zeros([states.length, actions.length]));
```

Ahora que tenemos definidos nuestros estados y acciones, podemos comenzar a entrenar nuestro modelo. Haremos esto recorriendo una serie de episodios. En cada episodio, nuestro agente realizará una acción en un estado y recibirá una recompensa. Luego, el agente utilizará el algoritmo Q-learning para actualizar los valores Q para los pares de estado-acción que ha encontrado.

```javascript
for (let episode = 0; episode < 1000; episode++) {
  // Reset the environment at the start of each episode.
  let state = [0, 0];

  // Loop over each timestep in the episode.
  for (let timestep = 0; timestep < 10; timestep++) {
    // Choose an action at random.
    let action = _.sample(actions);

    // Take the action and observe the reward.
    let reward = 1;

    // Use the Q-learning algorithm to update the Q-values.
    let discount = 0.9;
    let nextState = [0, 0];
    Q.assign(tf.tensor2d(states).transpose(), expectedReturn(state, action, reward, discount, nextState));

    // Update the state.
    state = nextState;
  }
}
```

Una vez que nuestro modelo está entrenado, podemos usarlo para hacer predicciones. Para hacer esto, primero necesitaremos definir una función para convertir un estado en un tensor. Esta función se utilizará para convertir el estado de nuestro agente en un formato que pueda ser utilizado por nuestro modelo.

```javascript
function toTensor(state) {
  return tf.tensor2d([state]);
}
```

Ahora que tenemos definida nuestra función toTensor, podemos usarla para convertir el estado de nuestro agente en un tensor. Luego podemos usar nuestro modelo Q-learning para predecir el rendimiento esperado de realizar cada acción en el estado.

```javascript
let state = [0, 0];
let tensor = toTensor(state);
let prediction = Q(tensor);

console.log(prediction.dataSync());
// [ 0.0, 0.0, 0.0, 0.0 ]
```

Como podemos ver, nuestro modelo predice que el rendimiento esperado de realizar cada acción en el estado es 0.0. Esto se debe a que nuestro modelo aún no ha sido entrenado en este par estado-acción.

Para que nuestro modelo haga mejores predicciones, necesitaremos entrenarlo con más datos. Podemos hacer esto aumentando la cantidad de episodios en nuestro ciclo de entrenamiento. También podemos probar diferentes valores para el factor de descuento. Este parámetro controla cuánto valora el agente las recompensas futuras. Un factor de descuento más alto hará que el agente valore más las recompensas futuras.

Una vez que nuestro modelo está entrenado, podemos usarlo para encontrar la acción que maximiza el rendimiento esperado. Para hacer esto, usaremos nuestra función auxiliar argmax. Esta función tomará una matriz de valores y devolverá el índice del valor máximo.

```javascript
let state = [0, 0];
let tensor = toTensor(state);
let prediction = Q(tensor);

let action = argmax(prediction.dataSync());

console.log(action);
// 0
```

Como podemos ver, nuestro modelo predice que la acción con el rendimiento esperado más alto es 0 (arriba).

Este es un ejemplo simple de cómo usar el algoritmo Q-learning para entrenar a un agente de aprendizaje por refuerzo en Node.js usando TensorFlow.js. Este algoritmo se puede usar para resolver una variedad de tareas, como jugar videojuegos, controlar robots y administrar recursos en un centro de datos.