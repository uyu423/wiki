---
title: 095: Creación de redes de memoria a corto plazo (LSTM) en TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T05:17:55.675Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:17:53.922Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [095: Building Long Short-Term Memory (LSTM) Networks in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/095-building-long-short-term-memory-lstm-networks-in-tensorflow-js-and-node-js)
{.links-list}


# 095: Creación de redes de memoria a largo plazo (LSTM) en TensorFlow.js y Node.js

En esta publicación, veremos cómo crear redes de memoria a corto plazo (LSTM) en TensorFlow.js y Node.js.

Los LSTM son un tipo de red neuronal recurrente que se adapta bien para trabajar con datos secuenciales. Los datos secuenciales son datos en los que cada elemento depende del elemento anterior, como los datos de series temporales.

Los LSTM pueden aprender dependencias a largo plazo mediante el uso de una celda de "memoria" que puede recordar información durante largos períodos de tiempo. Los LSTM también pueden manejar elementos de entrada que no están en el mismo orden que los elementos de salida, lo cual es importante para trabajar con datos de series temporales.

## Construyendo una red LSTM en TensorFlow.js

Comenzaremos analizando cómo crear una red LSTM en TensorFlow.js.

Primero, necesitamos instalar TensorFlow.js. Podemos hacer esto usando el administrador de paquetes de Node.js, npm:

```
npm install @tensorflow/tfjs
```

A continuación, debemos crear un nuevo archivo llamado `lstm.js` e importar TensorFlow.js:

```javascript
const tf = require('@tensorflow/tfjs');
```

Ahora estamos listos para comenzar a construir nuestra red LSTM.

Comenzaremos definiendo el modelo:

```javascript
const model = tf.sequential();
```

A continuación, agregaremos una capa LSTM al modelo. El primer argumento de la función `tf.layers.lstm` es el número de unidades, que es el número de celdas de memoria en la capa LSTM. Usaremos 16 unidades:

```javascript
model.add(tf.layers.lstm({units: 16, inputShape: [1, 1]}));
```

El argumento `inputShape` es la forma de los datos de entrada. El primer elemento es el número de pasos de tiempo y el segundo elemento es el número de características. En nuestro caso, tenemos un paso de tiempo y una característica.

A continuación, agregaremos una capa densa al modelo. Esta es una capa estándar completamente conectada que generará un solo valor:

```javascript
model.add(tf.layers.dense({units: 1}));
```

Ahora necesitamos compilar el modelo. Necesitamos especificar la función de pérdida y el optimizador. Usaremos la función de pérdida de error cuadrático medio y el optimizador de Adam:

```javascript
model.compile({loss: 'meanSquaredError', optimizer: 'adam'});
```

Ahora estamos listos para entrenar el modelo. Usaremos un `tf.tensor2d` para especificar los datos de entrenamiento. El primer argumento son los datos, y el segundo argumento es la forma de los datos. En nuestro caso, tenemos dos ejemplos de entrenamiento, cada uno con un paso de tiempo y una función:

```javascript
const xs = tf.tensor2d([[1], [2]]);
const ys = tf.tensor2d([[1], [2]]);
```

Entrenaremos el modelo durante 10 épocas, que es la cantidad de veces que el modelo verá los datos de entrenamiento:

```javascript
model.fit(xs, ys, {epochs: 10});
```

Una vez que el modelo ha sido entrenado, podemos usarlo para hacer predicciones. Usaremos un `tf.tensor2d` para especificar los datos de entrada. En nuestro caso, tenemos un paso de tiempo y una característica:

```javascript
const xs = tf.tensor2d([[3]]);
```

Entonces podemos llamar al método `model.predict` para hacer una predicción:

```javascript
model.predict(xs).print();
```

Esto generará la predicción, que es un valor único.

## Construyendo una red LSTM en Node.js

Ahora veremos cómo construir una red LSTM en Node.js.

Primero, necesitamos instalar TensorFlow.js. Podemos hacer esto usando el administrador de paquetes de Node.js, npm:

```
npm install @tensorflow/tfjs
```

A continuación, debemos crear un nuevo archivo llamado `lstm.js` e importar TensorFlow.js:

```javascript
const tf = require('@tensorflow/tfjs');
```

Ahora estamos listos para comenzar a construir nuestra red LSTM.

Comenzaremos definiendo el modelo:

```javascript
const model = tf.sequential();
```

A continuación, agregaremos una capa LSTM al modelo. El primer argumento de la función `tf.layers.lstmLayer` es el número de unidades, que es el número de celdas de memoria en la capa LSTM. Usaremos 16 unidades:

```javascript
model.add(tf.layers.lstmLayer({units: 16, inputShape: [1, 1]}));
```

El argumento `inputShape` es la forma de los datos de entrada. El primer elemento es el número de pasos de tiempo y el segundo elemento es el número de características. En nuestro caso, tenemos un paso de tiempo y una característica.

A continuación, agregaremos una capa densa al modelo. Esta es una capa estándar completamente conectada que generará un solo valor:

```javascript
model.add(tf.layers.denseLayer({units: 1}));
```

Ahora necesitamos compilar el modelo. Necesitamos especificar la función de pérdida y el optimizador. Usaremos la función de pérdida de error cuadrático medio y el optimizador de Adam:

```javascript
model.compile({loss: 'meanSquaredError', optimizer: 'adam'});
```

Ahora estamos listos para entrenar el modelo. Usaremos un `tf.tensor2d` para especificar los datos de entrenamiento. El primer argumento son los datos, y el segundo argumento es la forma de los datos. En nuestro caso, tenemos dos ejemplos de entrenamiento, cada uno con un paso de tiempo y una característica:

```javascript
const xs = tf.tensor2d([[1], [2]]);
const ys = tf.tensor2d([[1], [2]]);
```

Entrenaremos el modelo durante 10 épocas, que es la cantidad de veces que el modelo verá los datos de entrenamiento:

```javascript
model.fit(xs, ys, {epochs: 10});
```

Una vez que el modelo ha sido entrenado, podemos usarlo para hacer predicciones. Usaremos un `tf.tensor2d` para especificar los datos de entrada. En nuestro caso, tenemos un paso de tiempo y una característica:

```javascript
const xs = tf.tensor2d([[3]]);
```

Entonces podemos llamar al método `model.predict` para hacer una predicción:

```javascript
model.predict(xs).print();
```

Esto generará la predicción, que es un valor único.

## Conclusión

En esta publicación, hemos visto cómo crear redes de memoria a corto plazo (LSTM) en TensorFlow.js y Node.js. Los LSTM son un tipo de red neuronal recurrente que se adapta bien para trabajar con datos secuenciales.

Si está interesado en obtener más información sobre los LSTM, le recomiendo los siguientes recursos:

- [La eficacia irrazonable de las redes neuronales recurrentes] (https://karpathy.github.io/2015/05/21/rnn-efectividad/)
- [Comprender las redes LSTM](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [Memoria a largo plazo](https://en.wikipedia.org/wiki/Long_short-term_memory)