---
title: 094: Creación de redes neuronales recurrentes (RNN) en TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T05:05:04.319Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:05:02.678Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [094: Building Recurrent Neural Networks (RNNs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/094-building-recurrent-neural-networks-rnns-in-tensorflow-js-and-node-js)
{.links-list}


# Introducción

Las redes neuronales recurrentes (RNN) son un tipo de red neuronal artificial donde las conexiones entre nodos forman un gráfico dirigido a lo largo de una secuencia temporal o espacial. Esto le permite exhibir un comportamiento dinámico temporal para una serie de tiempo o secuencia de eventos.

En esta publicación, crearemos RNN en TensorFlow.js y Node.js. TensorFlow.js es una biblioteca de aprendizaje automático acelerado por hardware de código abierto para la web y JavaScript. Node.js es un entorno de tiempo de ejecución multiplataforma que le permite escribir código JavaScript del lado del servidor.

Usaremos un conjunto de datos de los precios diarios de las acciones de Apple, Inc. (AAPL) desde el 1 de enero de 2013 hasta el 31 de diciembre de 2016. El objetivo es predecir el precio de apertura de las acciones para el 1 de enero de 2017.

# requisitos previos

Antes de comenzar, hay algunas cosas que necesitará:

- Conocimientos básicos de redes neuronales artificiales
- Familiaridad con JavaScript
- Un editor de texto
- Un navegador web

# Empezando

## Instalación de TensorFlow.js

Para instalar TensorFlow.js, puede usar un administrador de paquetes como npm o yarn.

```
npm install @tensorflow/tfjs
```

```
yarn add @tensorflow/tfjs
```

Como alternativa, puede incluir la biblioteca TensorFlow.js en su archivo HTML con una etiqueta de secuencia de comandos.

```html
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.3/dist/tf.min.js"></script>
```

## Instalación de Node.js

Para instalar Node.js, puede descargar el instalador desde el [sitio web de Node.js] (https://nodejs.org/en/).

## Descarga del conjunto de datos

El conjunto de datos que usaremos está disponible [aquí](https://www.kaggle.com/camnugent/sandp500). Descargue el archivo CSV y guárdelo en el mismo directorio que su archivo JavaScript.

# Construyendo la RNN

## Cargando el conjunto de datos

Comenzaremos cargando el conjunto de datos en TensorFlow.js.

```javascript
const tf = require('@tensorflow/tfjs');

const data = tf.loadCSV('AAPL.csv');
```

## Preprocesamiento de los datos

A continuación, dividiremos los datos en conjuntos de entrenamiento y prueba. También escalaremos los datos para que estén entre 0 y 1. Este es un paso de preprocesamiento común para las redes neuronales.

```javascript
const train_data = data.slice(0, data.length - 7);
const test_data = data.slice(data.length - 7);

const train_x = train_data.map(row => row.slice(1, row.length - 1));
const train_y = train_data.map(row => row[row.length - 1]);

const test_x = test_data.map(row => row.slice(1, row.length - 1));
const test_y = test_data.map(row => row[row.length - 1]);

const x_min = Math.min(...train_x.map(row => Math.min(...row)));
const x_max = Math.max(...train_x.map(row => Math.max(...row)));

const y_min = Math.min(...train_y);
const y_max = Math.max(...train_y);

const train_x_scaled = train_x.map(row => row.map(col => (col - x_min) / (x_max - x_min)));
const test_x_scaled = test_x.map(row => row.map(col => (col - x_min) / (x_max - x_min)));

const train_y_scaled = train_y.map(val => (val - y_min) / (y_max - y_min));
const test_y_scaled = test_y.map(val => (val - y_min) / (y_max - y_min));
```

## Construyendo el modelo

Ahora podemos construir el RNN. Comenzaremos creando un modelo secuencial.

```javascript
const model = tf.sequential();
```

A continuación, agregaremos una capa recurrente al modelo. Esta capa tendrá 10 unidades y una forma de entrada de 1.

```javascript
model.add(tf.layers.simpleRNN({units: 10, inputShape: [1]}));
```

Finalmente, agregaremos una capa densa con una sola unidad y una forma de salida de 1. Esta es la capa que generará el precio de las acciones pronosticado.

```javascript
model.add(tf.layers.dense({units: 1, inputShape: [10]}));
```

## Compilando el modelo

Ahora que hemos construido el modelo, necesitamos compilarlo antes de poder entrenarlo. Usaremos el error cuadrático medio (MSE) como nuestra función de pérdida y el optimizador de Adam.

```javascript
model.compile({loss: 'meanSquaredError', optimizer: 'adam'});
```

## Entrenamiento del modelo

Ahora estamos listos para entrenar el modelo. Lo entrenaremos durante 10 épocas y usaremos un tamaño de lote de 1.

```javascript
model.fit(tf.tensor2d(train_x_scaled, [train_x_scaled.length, 1]), tf.tensor2d(train_y_scaled, [train_y_scaled.length, 1]), {
  epochs: 10,
  batchSize: 1
});
```

## Predicción de precios de acciones

Ahora que el modelo está entrenado, podemos usarlo para hacer predicciones en el conjunto de prueba.

```javascript
const test_predictions = model.predict(tf.tensor2d(test_x_scaled, [test_x_scaled.length, 1]));
```

## Evaluación del modelo

Finalmente, podemos evaluar el rendimiento del modelo en el conjunto de prueba.

```javascript
const test_loss = tf.losses.meanSquaredError(test_predictions, tf.tensor2d(test_y_scaled, [test_y_scaled.length, 1]));

console.log(test_loss.dataSync());
```

# Conclusión

En esta publicación, hemos visto cómo construir una red neuronal recurrente en TensorFlow.js y Node.js. También hemos visto cómo preprocesar los datos y entrenar el modelo.

Si bien el modelo que hemos construido es bastante simple, se puede extender a modelos más complejos. Por ejemplo, podría agregar más capas o unidades al modelo, o podría usar un optimizador diferente.

# Recursos

- [Documentación de TensorFlow.js](https://js.tensorflow.org/)
- [Documentación de Node.js](https://nodejs.org/en/docs/)
- [Red neuronal recurrente](https://en.wikipedia.org/wiki/Recurrent_neural_network)
- [Predicción del mercado de valores usando redes neuronales recurrentes](https://t.co/GbU6XfjlbO?amp=1)