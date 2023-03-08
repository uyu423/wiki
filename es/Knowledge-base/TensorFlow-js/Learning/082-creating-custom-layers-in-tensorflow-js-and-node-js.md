---
title: 082: Creación de capas personalizadas en TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T02:04:26.609Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:04:24.986Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [082: Creating Custom Layers in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/082-creating-custom-layers-in-tensorflow-js-and-node-js)
{.links-list}


# 082: Creación de capas personalizadas en TensorFlow.js y Node.js

En esta publicación, aprenderemos cómo crear capas personalizadas en TensorFlow.js y Node.js.

TensorFlow.js es una poderosa herramienta que nos permite crear modelos de aprendizaje automático personalizados e implementarlos en el navegador o en Node.js. En esta publicación, nos centraremos en crear capas personalizadas en TensorFlow.js.

La creación de capas personalizadas es una excelente manera de ampliar la funcionalidad de TensorFlow.js y Node.js. Al crear una capa personalizada, podemos agregar una nueva funcionalidad a TensorFlow.js y Node.js que no está disponible en la biblioteca principal.

Crear una capa personalizada no es una tarea difícil, pero hay algunas cosas que debemos tener en cuenta. En esta publicación, repasaremos los conceptos básicos para crear una capa personalizada y discutiremos algunas de las cosas que debemos tener en cuenta.

## ¿Qué es una capa?

Antes de sumergirnos en la creación de una capa personalizada, primero demos un paso atrás y entendamos qué es una capa.

Una capa es una colección de neuronas que están conectadas entre sí. Las capas a menudo se apilan una encima de la otra para formar una red neuronal profunda.

Las capas son las encargadas de transformar los datos de entrada en datos de salida. Los datos de entrada se alimentan a la primera capa, y la salida de la primera capa se alimenta a la segunda capa, y así sucesivamente.

Las capas pueden tener diferentes tipos de neuronas. El tipo más común de neurona es la neurona totalmente conectada. Las neuronas completamente conectadas están conectadas a todas las neuronas en la capa anterior.

Otros tipos de neuronas incluyen neuronas convolucionales y neuronas de agrupación. Las neuronas convolucionales se utilizan en redes neuronales convolucionales, y las neuronas de agrupación se utilizan en capas de agrupación.

## Crear una capa personalizada

Ahora que sabemos qué es una capa, aprendamos cómo crear una capa personalizada.

Crear una capa personalizada no es una tarea difícil, pero hay algunas cosas que debemos tener en cuenta. En esta sección, repasaremos los conceptos básicos para crear una capa personalizada.

Al crear una capa personalizada, debemos especificar la forma de entrada y la forma de salida. La forma de entrada es la forma de los datos que se introducirán en la capa, y la forma de salida es la forma de los datos que generará la capa.

También necesitamos especificar el tipo de neuronas que se utilizarán en la capa. El tipo más común de neurona es la neurona totalmente conectada. Sin embargo, también podemos usar neuronas convolucionales o neuronas de agrupación.

Una vez que hemos especificado la forma de entrada, la forma de salida y el tipo de neuronas, podemos implementar el pase hacia adelante y el pase hacia atrás. El pase hacia adelante es responsable de transformar los datos de entrada en datos de salida, y el pase hacia atrás es responsable de propagar hacia atrás los gradientes.

## Implementando el pase hacia adelante

El pase hacia adelante es responsable de transformar los datos de entrada en datos de salida. En esta sección, aprenderemos cómo implementar el pase hacia adelante.

El pase hacia adelante se implementa mediante la función ```forward```. Esta función toma los datos de entrada y los transforma en datos de salida.

Los datos de entrada se alimentan a la primera capa, y la salida de la primera capa se alimenta a la segunda capa, y así sucesivamente. La salida de la capa final son los datos de salida.

## Implementando el pase hacia atrás

El pase hacia atrás es responsable de propagar hacia atrás los gradientes. En esta sección, aprenderemos cómo implementar el pase hacia atrás.

El pase hacia atrás se implementa mediante la función ```backward```. Esta función toma los gradientes y los propaga hacia atrás.

Los gradientes se propagan hacia atrás a través de las capas. Los gradientes de la capa final se propagan a la capa anterior, y los gradientes de la capa anterior se propagan a la capa anterior, y así sucesivamente.

## Conclusión

En esta publicación, aprendimos cómo crear capas personalizadas en TensorFlow.js y Node.js. La creación de capas personalizadas es una excelente manera de ampliar la funcionalidad de TensorFlow.js y Node.js.

Al crear una capa personalizada, podemos agregar una nueva funcionalidad a TensorFlow.js y Node.js que no está disponible en la biblioteca principal. Crear una capa personalizada no es una tarea difícil, pero hay algunas cosas que debemos tener en cuenta.

En esta publicación, hemos repasado los conceptos básicos para crear una capa personalizada. Hemos aprendido a especificar la forma de entrada, la forma de salida y el tipo de neuronas. También hemos aprendido cómo implementar el pase hacia adelante y el pase hacia atrás.