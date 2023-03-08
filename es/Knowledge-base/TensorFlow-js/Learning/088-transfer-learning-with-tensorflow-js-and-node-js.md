---
title: 088: Transferencia de aprendizaje con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T03:36:19.528Z
tags: 
editor: markdown
dateCreated: 2023-02-03T03:36:17.928Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [088: Transfer Learning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/088-transfer-learning-with-tensorflow-js-and-node-js)
{.links-list}


# 088: Transferencia de aprendizaje con TensorFlow.js y Node.js

En esta publicación, aprenderemos a usar el aprendizaje por transferencia para volver a entrenar un modelo creado con TensorFlow.js y Node.js.

Transfer learning es una técnica que nos permite utilizar un modelo previamente entrenado y adaptarlo a nuestros propios datos y tareas. Esto es útil cuando no tenemos suficientes datos para entrenar un modelo desde cero o cuando queremos usar un modelo que ya ha sido entrenado en una tarea similar.

Usaremos un modelo preentrenado de TensorFlow.js Model Zoo. El modelo que usaremos es un modelo MobileNetV2 que se entrenó en el conjunto de datos de ImageNet.

## ¿Qué es TensorFlow.js?

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático en el navegador y en Node.js.

## ¿Qué es Node.js?

Node.js es un tiempo de ejecución de JavaScript para ejecutar código del lado del servidor.

## ¿Qué es un modelo preentrenado?

Un modelo preentrenado es un modelo que ha sido entrenado en un conjunto de datos.

## ¿Qué es el conjunto de datos de ImageNet?

ImageNet es un gran conjunto de datos de imágenes que a menudo se usa para entrenar modelos de clasificación de imágenes.

## ¿Qué es el aprendizaje por transferencia?

Transfer learning es una técnica que nos permite utilizar un modelo previamente entrenado y adaptarlo a nuestros propios datos y tareas.

## ¿Cómo uso el aprendizaje por transferencia con TensorFlow.js?

Hay dos formas de usar el aprendizaje por transferencia con TensorFlow.js:

1. Puede usar un modelo preentrenado de TensorFlow.js Model Zoo.
2. Puede usar un modelo previamente entrenado de otro marco, como TensorFlow, Keras o PyTorch.

## ¿Cómo uso un modelo previamente entrenado del Zoológico de modelos de TensorFlow.js?

Para usar un modelo preentrenado de TensorFlow.js Model Zoo, deberá hacer lo siguiente:

1. Elija un modelo previamente entrenado.
2. Cargue el modelo.
3. Vuelva a entrenar el modelo con sus propios datos.

## ¿Cómo elijo un modelo pre-entrenado?

Al elegir un modelo preentrenado, deberá tener en cuenta lo siguiente:

1. El tamaño del modelo.
2. La precisión del modelo.
3. El costo computacional del modelo.

## ¿Cómo cargo el modelo?

Para cargar el modelo, deberá usar la función `tf.loadModel`. Esta función toma una URL o una instancia `tf.Model`.

## ¿Cómo vuelvo a entrenar al modelo?

Para volver a entrenar el modelo, deberá usar la función `tf.train`. Esta función toma una instancia `tf.Model` y una instancia `tf.Tensor`. La instancia `tf.Tensor` contiene los datos de entrenamiento.

## ¿Cuáles son los beneficios de usar el aprendizaje por transferencia?

Hay varios beneficios de usar el aprendizaje por transferencia:

1. Es más rápido que entrenar un modelo desde cero.
2. Requiere menos datos.
3. Se puede usar para entrenar a un modelo en una nueva tarea.
4. Se puede utilizar para mejorar el rendimiento de un modelo.

## ¿Cuáles son los inconvenientes de utilizar el aprendizaje por transferencia?

Hay varios inconvenientes de usar el aprendizaje por transferencia:

1. Puede ser difícil entender cómo funciona el modelo preentrenado.
2. Puede ser difícil depurar el modelo previamente entrenado.
3. El modelo previamente capacitado puede no ser adecuado para la nueva tarea.

## Conclusión

En esta publicación, aprendimos a usar el aprendizaje por transferencia para volver a entrenar un modelo creado con TensorFlow.js y Node.js.