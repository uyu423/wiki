---
title: 031: Modelos de entrenamiento y ajuste fino con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T14:17:56.969Z
tags: 
editor: markdown
dateCreated: 2023-02-02T14:17:55.375Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [031: Training and Fine-Tuning Models with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/031-training-and-fine-tuning-models-with-tensorflow-js-and-node-js)
{.links-list}


# 031: Modelos de entrenamiento y ajuste fino con TensorFlow.js y Node.js

TensorFlow.js es una biblioteca de código abierto para el cálculo numérico que le permite crear y entrenar modelos de aprendizaje automático en el navegador. Node.js es un tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript fuera del navegador. En esta publicación, le mostraremos cómo usar TensorFlow.js y Node.js para entrenar y ajustar modelos de aprendizaje automático.

## Instalación de TensorFlow.js

Para instalar TensorFlow.js, deberá tener instalados Node.js y npm (el administrador de paquetes de Node.js). Puede verificar si tiene instalado Node.js ejecutando el siguiente comando en su terminal:

```
node -v
```

Si no tiene instalado Node.js, puede descargarlo [aquí](https://nodejs.org/en/).

Una vez que haya instalado Node.js y npm, puede instalar TensorFlow.js con el siguiente comando:

```
npm install @tensorflow/tfjs
```

## Entrenamiento de un modelo

Ahora que tiene instalado TensorFlow.js, puede comenzar a entrenar sus propios modelos de aprendizaje automático. En esta sección, le mostraremos cómo entrenar un modelo de regresión lineal simple.

Primero, vamos a crear algunos datos de entrenamiento. Usaremos la función tf.tensor2d() integrada para crear un tensor 2D (una matriz de matrices) con 10 filas y 1 columna. Rellenaremos el tensor con números aleatorios de una distribución normal con una media de 0 y una desviación estándar de 1.

```javascript
const xs = tf.tensor2d([-1, 0, 1, 2, 3, 4], [6, 1]);
const ys = tf.tensor2d([-3, -1, 1, 3, 5, 7], [6, 1]);
```

A continuación, definiremos nuestro modelo. Usaremos la función tf.secuencial() para crear un modelo secuencial, que es una pila lineal de capas. Luego, usaremos la función tf.layers.dense() para agregar una capa densa al modelo. Una capa densa es una capa totalmente conectada, lo que significa que todos los nodos de la capa anterior están conectados a todos los nodos de la capa densa. Especificaremos que la capa densa tiene 1 nodo de salida y que la forma de entrada es [1].

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));
```

Ahora que hemos definido nuestro modelo, necesitamos compilarlo. La compilación del modelo configurará el modelo para el entrenamiento. Usaremos la función tf.train.sgd() para crear un optimizador de descenso de gradiente estocástico. El optimizador se utilizará para minimizar la función de pérdida durante el entrenamiento. También especificaremos que queremos optimizar para el error cuadrático medio.

```javascript
model.compile({optimizer: tf.train.sgd(0.1), loss: 'meanSquaredError'});
```

Ahora que nuestro modelo está compilado, podemos comenzar a entrenarlo. Usaremos la función model.fit() para entrenar el modelo. Especificaremos los datos de entrenamiento (xs e ys), el número de épocas (100) y el tamaño del lote (1). Las épocas son el número de veces que el modelo pasará por los datos de entrenamiento. El tamaño del lote es la cantidad de ejemplos de entrenamiento que usará el modelo antes de actualizar los pesos del modelo.

```javascript
model.fit(xs, ys, {epochs: 100, batchSize: 1});
```

## Haciendo predicciones

Ahora que nuestro modelo está entrenado, podemos usarlo para hacer predicciones. Usaremos la función model.predict() para hacer predicciones. Pasaremos un tensor 1D con el valor 3. El modelo generará un tensor 1D con el valor 9.

```javascript
model.predict(tf.tensor2d([3], [1, 1])).print();
```

## Ajuste fino de un modelo

Una vez que tenga un modelo entrenado, es posible que desee ajustarlo para mejorar su rendimiento. En esta sección, le mostraremos cómo ajustar un modelo previamente entrenado.

Comenzaremos cargando un modelo previamente entrenado. Usaremos la función tf.loadLayersModel() para cargar el modelo. Tendremos que especificar la URL del modelo. Puede encontrar una lista de modelos previamente entrenados [aquí](https://github.com/tensorflow/tfjs-models/tree/master/models).

```javascript
const model = tf.loadLayersModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

Ahora que hemos cargado el modelo, necesitamos compilarlo. Usaremos la misma función compile() que antes. Sin embargo, esta vez especificaremos que queremos optimizar la precisión de la clasificación.

```javascript
model.compile({optimizer: tf.train.sgd(0.0001), loss: 'categoricalCrossentropy', metrics: ['accuracy']});
```

Ahora podemos comenzar a entrenar el modelo. Usaremos la función fit() nuevamente. Sin embargo, esta vez especificaremos el número de épocas (5) y los datos de validación (xs e ys). Los datos de validación se utilizan para evaluar el modelo después de cada época.

```javascript
model.fit(xs, ys, {epochs: 5, validationData: [xs, ys]});
```

Después de entrenar el modelo, podemos usarlo para hacer predicciones. Usaremos la función predecir () nuevamente. Esta vez pasaremos una imagen de un perro. El modelo generará una matriz de probabilidades, una para cada clase. La probabilidad más alta será la clase a la que el modelo predice que pertenece la imagen.

```javascript
model.predict(tf.tensor2d([image], [1, 224, 224, 3])).print();
```

## Conclusión

En esta publicación, le mostramos cómo usar TensorFlow.js y Node.js para entrenar y ajustar los modelos de aprendizaje automático.