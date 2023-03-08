---
title: 008: Redes neuronales convolucionales (CNN) con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T08:37:03.777Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:36:59.260Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [008: Convolutional Neural Networks (CNN) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/008-convolutional-neural-networks-cnn-with-tensorflow-js-and-node-js)
{.links-list}


# Introducción

En esta publicación, veremos cómo crear redes neuronales convolucionales (CNN) en TensorFlow.js y Node.js. Usaremos un conjunto de datos bien conocido para el reconocimiento de imágenes, el conjunto de datos MNIST, para entrenar nuestra CNN.

Las redes neuronales convolucionales son un tipo de red neuronal particularmente adecuada para tareas de reconocimiento de imágenes. Esto se debe a que pueden aprovechar la estructura espacial de las imágenes.

# Construyendo una CNN en TensorFlow.js

Comenzaremos viendo cómo construir una CNN en TensorFlow.js. Si no está familiarizado con TensorFlow.js, es una biblioteca de JavaScript para el aprendizaje automático que se ejecuta en el navegador.

Primero, necesitamos cargar el conjunto de datos MNIST. El conjunto de datos MNIST es una colección de imágenes de dígitos escritos a mano, cada uno de los cuales tiene 28x28 píxeles.

Podemos cargar el conjunto de datos MNIST usando la función `tf.data.mnist` de TensorFlow.js. Esta función devuelve un objeto `Dataset`, que luego podemos usar para entrenar nuestra CNN.

```javascript
const mnistData = tf.data.mnist({
  train: true,
  testData: false
});
```

A continuación, necesitamos definir la red neuronal convolucional. Usaremos un modelo secuencial, que es un tipo de red neuronal que se compone de una pila lineal de capas.

Comenzaremos agregando una capa `Flatten`, que toma nuestras imágenes de 28x28 y las aplana en un solo vector de 784 elementos.

```javascript
const model = tf.sequential();

model.add(tf.layers.flatten({
  inputShape: [28, 28]
}));
```

A continuación, agregaremos una capa `Densa`. Esta es una capa totalmente conectada, lo que significa que cada neurona de la capa está conectada a cada neurona de la capa anterior.

Configuraremos la capa `Dense` para que tenga 128 neuronas y use la función de activación `relu`. La función de activación `relu` es una opción común para las redes neuronales. Da salida a 0 para cualquier entrada menor que 0 y da salida a la entrada para cualquier entrada mayor o igual a 0.

```javascript
model.add(tf.layers.dense({
  units: 128,
  activation: 'relu',
  inputShape: [784]
}));
```

Finalmente, agregaremos una capa `Densa` con 10 neuronas y la función de activación `softmax`. La función de activación `softmax` es una opción común para la capa de salida de una red neuronal. Produce una distribución de probabilidad sobre los 10 dígitos posibles.

```javascript
model.add(tf.layers.dense({
  units: 10,
  activation: 'softmax',
  inputShape: [128]
}));
```

Ahora que hemos definido nuestro modelo, necesitamos compilarlo. Cuando compilamos un modelo, especificamos la función de pérdida y el optimizador.

La función de pérdida es una medida de qué tan bien está funcionando el modelo. Queremos minimizar la función de pérdida, lo que significa que queremos que el modelo haga predicciones lo más cercanas posible a las etiquetas verdaderas.

El optimizador es un algoritmo que se utiliza para actualizar el modelo con el fin de minimizar la función de pérdida. Hay muchos optimizadores diferentes disponibles, pero usaremos el optimizador `sgd`.

```javascript
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'sgd'
});
```

Ahora que nuestro modelo está compilado, podemos entrenarlo. Lo entrenaremos durante 10 épocas, lo que significa que el modelo verá el conjunto de datos MNIST completo 10 veces.

```javascript
model.fit(mnistData, {
  epochs: 10
});
```

# Construyendo una CNN en Node.js

Ahora que hemos visto cómo crear una CNN en TensorFlow.js, echemos un vistazo a cómo hacerlo en Node.js.

Primero, necesitamos cargar el conjunto de datos MNIST. El conjunto de datos MNIST es una colección de imágenes de dígitos escritos a mano, cada uno de los cuales tiene 28x28 píxeles.

Podemos cargar el conjunto de datos MNIST usando el paquete `mnist`. Este paquete devuelve un objeto `Dataset`, que luego podemos usar para entrenar nuestra CNN.

```javascript
const mnist = require('mnist');

const mnistData = mnist.training(0, 60000);
```

A continuación, necesitamos definir la red neuronal convolucional. Usaremos un modelo secuencial, que es un tipo de red neuronal que se compone de una pila lineal de capas.

Comenzaremos agregando una capa `Flatten`, que toma nuestras imágenes de 28x28 y las aplana en un solo vector de 784 elementos.

```javascript
const model = tf.sequential();

model.add(tf.layers.flatten({
  inputShape: [28, 28]
}));
```

A continuación, agregaremos una capa `Densa`. Esta es una capa totalmente conectada, lo que significa que cada neurona de la capa está conectada a cada neurona de la capa anterior.

Configuraremos la capa `Dense` para que tenga 128 neuronas y use la función de activación `relu`. La función de activación `relu` es una opción común para las redes neuronales. Da salida a 0 para cualquier entrada menor que 0 y da salida a la entrada para cualquier entrada mayor o igual a 0.

```javascript
model.add(tf.layers.dense({
  units: 128,
  activation: 'relu',
  inputShape: [784]
}));
```

Finalmente, agregaremos una capa `Densa` con 10 neuronas y la función de activación `softmax`. La función de activación `softmax` es una opción común para la capa de salida de una red neuronal. Produce una distribución de probabilidad sobre los 10 dígitos posibles.

```javascript
model.add(tf.layers.dense({
  units: 10,
  activation: 'softmax',
  inputShape: [128]
}));
```

Ahora que hemos definido nuestro modelo, necesitamos compilarlo. Cuando compilamos un modelo, especificamos la función de pérdida y el optimizador.

La función de pérdida es una medida de qué tan bien está funcionando el modelo. Queremos minimizar la función de pérdida, lo que significa que queremos que el modelo haga predicciones lo más cercanas posible a las etiquetas verdaderas.

El optimizador es un algoritmo que se utiliza para actualizar el modelo con el fin de minimizar la función de pérdida. Hay muchos optimizadores diferentes disponibles, pero usaremos el optimizador `sgd`.

```javascript
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'sgd'
});
```

Ahora que nuestro modelo está compilado, podemos entrenarlo. Lo entrenaremos durante 10 épocas, lo que significa que el modelo verá el conjunto de datos MNIST completo 10 veces.

```javascript
model.fit(mnistData, {
  epochs: 10
});
```

# Conclusión

En esta publicación, hemos visto cómo construir redes neuronales convolucionales en TensorFlow.js y Node.js. También hemos visto cómo entrenar estas redes en el conjunto de datos MNIST.