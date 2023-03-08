---
title: 034: Visualización del entrenamiento de modelos con TensorBoard y Node.js
description: 
published: true
date: 2023-02-02T15:04:26.610Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:04:25.014Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [034: Visualizing Model Training with TensorBoard and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/034-visualizing-model-training-with-tensorboard-and-node-js)
{.links-list}


---

# 034: Visualización del entrenamiento de modelos con TensorBoard y Node.js

TensorBoard es un conjunto de herramientas de visualización para el aprendizaje automático desarrollado por Google. Le permite visualizar el proceso de entrenamiento de sus modelos de aprendizaje automático, lo que puede ser útil para depurar y optimizar sus modelos.

En esta publicación, aprenderemos a usar TensorBoard con Node.js. Comenzaremos instalando TensorBoard y configurando un modelo básico de aprendizaje automático. Luego, aprenderemos a usar TensorBoard para visualizar el proceso de entrenamiento de nuestro modelo.

## Instalación de TensorBoard

TensorBoard está disponible como un paquete de Python. Podemos instalarlo usando el administrador de paquetes pip:

```
pip install tensorboard
```

## Configuración de un modelo básico de aprendizaje automático

Usaremos TensorFlow.js para configurar un modelo básico de aprendizaje automático. TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático en el navegador.

Primero, necesitamos instalar TensorFlow.js:

```
npm install @tensorflow/tfjs
```

A continuación, configuraremos un modelo de regresión lineal simple. Usaremos la API tf.secuencial() para crear un modelo:

```javascript
const model = tf.sequential();
```

Luego, agregaremos una sola capa densa a nuestro modelo. Una capa densa es una capa totalmente conectada, lo que significa que todas las neuronas de la capa están conectadas a todas las neuronas de la capa anterior:

```javascript
model.add(tf.layers.dense({units: 1, inputShape: [1]}));
```

Finalmente, compilaremos nuestro modelo. Necesitamos especificar un optimizador y una función de pérdida cuando compilamos un modelo. El optimizador se utiliza para actualizar los pesos del modelo durante el entrenamiento. La función de pérdida se utiliza para medir el rendimiento del modelo. Usaremos el optimizador tf.train.sgd() y la función de pérdida tf.losses.meanSquaredError():

```javascript
model.compile({optimizer: tf.train.sgd(0.001), loss: tf.losses.meanSquaredError});
```

## Visualización del proceso de capacitación con TensorBoard

Ahora que tenemos configurado nuestro modelo de aprendizaje automático, podemos comenzar a usar TensorBoard para visualizar el proceso de capacitación.

Primero, necesitamos crear una devolución de llamada de TensorBoard. Una devolución de llamada es una función que se llama al final de cada época de entrenamiento. Podemos usar la función tf.tensorBoard() para crear una devolución de llamada:

```javascript
const tensorBoardCallback = tf.tensorBoard('logdir');
```

A continuación, entrenaremos nuestro modelo. Usaremos la función tf.fit() para entrenar nuestro modelo. Necesitamos especificar los datos de entrenamiento, la cantidad de épocas de entrenamiento y la devolución de llamada de TensorBoard que creamos:

```javascript
model.fit(x, y, {epochs: 100, callbacks: [tensorBoardCallback]});
```

Una vez que se completa el entrenamiento, podemos iniciar el servidor TensorBoard. Podemos hacer esto usando el comando tensorboard. Necesitamos especificar el directorio de registro que especificamos cuando creamos la devolución de llamada de TensorBoard:

```
tensorboard --logdir logdir
```

Esto iniciará el servidor TensorBoard y abrirá un navegador web. Luego podemos navegar a la pestaña "Gráficos" para ver una visualización del proceso de entrenamiento:

![Pestaña Gráficos de TensorBoard](https://i.imgur.com/rm3kTGi.png)

Podemos ver que la pérdida va disminuyendo a medida que avanzan las épocas de entrenamiento.

## Conclusión

En esta publicación, aprendimos a usar TensorBoard para visualizar el proceso de capacitación de un modelo de aprendizaje automático. Instalamos TensorBoard y configuramos un modelo básico de aprendizaje automático. Luego, usamos TensorBoard para visualizar el proceso de entrenamiento de nuestro modelo.