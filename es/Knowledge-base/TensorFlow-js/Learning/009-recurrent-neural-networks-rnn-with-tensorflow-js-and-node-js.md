---
title: 009: Redes neuronales recurrentes (RNN) con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T08:44:02.992Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:43:58.501Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [009: Recurrent Neural Networks (RNN) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/009-recurrent-neural-networks-rnn-with-tensorflow-js-and-node-js)
{.links-list}


# Introducción

Las redes neuronales recurrentes (RNN) son un tipo de red neuronal que son muy adecuadas para procesar datos secuenciales, como texto, audio y video. En esta publicación, usaremos TensorFlow.js y Node.js para crear un RNN que pueda generar texto nuevo, carácter por carácter.

# Configurando el proyecto

Antes de comenzar, debemos configurar nuestro proyecto. Usaremos el marco web Express para Node.js, por lo que primero debemos instalarlo.

```
$ npm install express --save
```

A continuación, necesitamos instalar TensorFlow.js. Usaremos la API de Node.js, por lo que debemos instalar el paquete `@tensorflow/tfjs-node`.

```
$ npm install @tensorflow/tfjs-node --save
```

Ahora que tenemos todas las dependencias que necesitamos, podemos crear un archivo llamado `index.js` en el directorio raíz de nuestro proyecto y comenzar a codificar.

# Construyendo la RNN

Lo primero que debemos hacer es cargar los datos que usaremos para entrenar nuestro RNN. Usaremos un corpus de texto de Shakespeare, que puede descargar [aquí] (https://storage.googleapis.com/tfjs-examples/shakespeare.txt).

Una vez que haya descargado el archivo de texto, podemos cargarlo en nuestro programa Node.js usando el módulo `fs`.

```javascript
const fs = require('fs');

const text = fs.readFileSync('shakespeare.txt', 'utf8');
```

Ahora que tenemos el texto cargado, debemos preprocesarlo para que sea adecuado para entrenar nuestro RNN. Comenzaremos convirtiendo todos los caracteres a minúsculas y eliminando todos los caracteres no alfanuméricos.

```javascript
const text = text.toLowerCase();
const text = text.replace(/[^a-zA-Z0-9]/g, '');
```

A continuación, debemos dividir el texto en una matriz de caracteres individuales.

```javascript
const chars = Array.from(text);
```

Ahora que tenemos nuestro texto preprocesado, podemos comenzar a construir nuestro RNN. Usaremos una celda de memoria a corto plazo (LSTM), que es un tipo de celda RNN que es adecuada para procesar datos secuenciales.

Podemos crear una celda LSTM en TensorFlow.js con el siguiente código:

```javascript
const lstmCell = tf.layers.lstmCell({
  units: 512,
  recurrentInputSize: 512,
  inputShape: [1, chars.length],
  kernelInitializer: 'glorotNormal',
  recurrentInitializer: 'orthogonal',
  biasInitializer: 'zeros',
  unitForgetBias: true,
  activation: 'tanh',
  recurrentActivation: 'sigmoid',
  useBias: true,
  kernelRegularizer: null,
  recurrentRegularizer: null,
  biasRegularizer: null,
  activityRegularizer: null,
  kernelConstraint: null,
  recurrentConstraint: null,
  biasConstraint: null,
  dropout: 0.0,
  recurrentDropout: 0.0
});
```

A continuación, necesitamos crear el propio RNN. Esto lo podemos hacer con el siguiente código:

```javascript
const rnn = tf.layers.rnn({
  cell: lstmCell,
  inputShape: [1, chars.length],
  returnSequences: true,
  goBackwards: false,
  stateful: false,
  unroll: false
});
```

Ahora que tenemos nuestro RNN creado, necesitamos compilarlo. Usaremos el optimizador Adam y la entropía cruzada categórica como nuestra función de pérdida.

```javascript
rnn.compile({
  optimizer: 'adam',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});
```

# Entrenando a la RNN

Ahora que nuestro RNN está compilado, podemos comenzar a entrenarlo. Primero necesitaremos crear algunos datos de entrenamiento. Crearemos una matriz de caracteres codificados en caliente, donde cada carácter está representado por un vector de ceros con un uno en el índice correspondiente al carácter.

```javascript
const chars = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'];

const oneHotChars = [];

for (let i = 0; i < chars.length; i++) {
  const char = chars[i];
  const oneHotChar = [];

  for (let j = 0; j < chars.length; j++) {
    if (j === i) {
      oneHotChar.push(1.0);
    } else {
      oneHotChar.push(0.0);
    }
  }

  oneHotChars.push(oneHotChar);
}
```

Ahora que tenemos nuestros caracteres codificados en caliente, necesitamos crear nuestros datos de entrenamiento. Crearemos una matriz de ejemplos de entrenamiento, donde cada ejemplo de entrenamiento es un par de caracteres codificados en caliente. El primer carácter del par será el carácter de entrada y el segundo carácter será el carácter de salida.

```javascript
const trainingData = [];

for (let i = 0; i < text.length - 1; i++) {
  const inputChar = oneHotChars[chars.indexOf(text[i])];
  const outputChar = oneHotChars[chars.indexOf(text[i + 1])];

  trainingData.push([inputChar, outputChar]);
}
```

Ahora que tenemos nuestros datos de entrenamiento, podemos entrenar nuestro RNN. Lo entrenaremos durante 10 épocas y usaremos un tamaño de lote de 32.

```javascript
rnn.fit(trainingData, {
  epochs: 10,
  batchSize: 32
});
```

# Generando texto

Ahora que nuestro RNN está entrenado, podemos usarlo para generar texto nuevo. Comenzaremos creando una función que tome un carácter y devuelva el siguiente carácter.

```javascript
function nextChar(char) {
  const oneHotChar = oneHotChars[chars.indexOf(char)];
  const output = rnn.predict(tf.tensor2d([oneHotChar], [1, oneHotChar.length]));
  const index = output.argMax(1).dataSync()[0];
  const nextChar = chars[index];

  return nextChar;
}
```

Ahora podemos usar nuestra función `nextChar` para generar texto nuevo. Comenzaremos con el carácter 'a' y generaremos 1000 caracteres.

```javascript
let text = 'a';

for (let i = 0; i < 1000; i++) {
  text += nextChar(text[text.length - 1]);
}

console.log(text);
```

¡Y eso es! Ahora tiene un RNN en funcionamiento que puede generar texto nuevo, carácter por carácter.

# Información Adicional

Si está interesado en obtener más información sobre las RNN, le recomiendo los siguientes recursos:

- [Redes neuronales recurrentes en TensorFlow](https://www.tensorflow.org/tutorials/sequences/recurrent)
- [Comprender las redes LSTM](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [Construyendo una red neuronal recurrente con TensorFlow](https://www.oreilly.com/learning/building-a-recurrent-neural-network-with-tensorflow)