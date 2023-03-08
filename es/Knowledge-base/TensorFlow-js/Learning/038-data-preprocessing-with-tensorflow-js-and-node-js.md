---
title: 038: Preprocesamiento de datos con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T15:43:30.905Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:43:29.358Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [038: Data Preprocessing with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/038-data-preprocessing-with-tensorflow-js-and-node-js)
{.links-list}


# 038: Preprocesamiento de datos con TensorFlow.js y Node.js

En esta publicación, aprenderemos cómo preprocesar datos para usarlos con TensorFlow.js y Node.js.

El preprocesamiento de datos es un paso crítico en el aprendizaje automático. A menudo se dice que el preprocesamiento de datos es el 80 % del trabajo en el aprendizaje automático. La razón de esto es que la calidad de los datos tiene un gran impacto en el rendimiento del algoritmo de aprendizaje automático.

Hay muchas maneras diferentes de preprocesar datos. Los métodos que use dependerán del tipo de datos que tenga y del algoritmo de aprendizaje automático que esté usando.

En esta publicación, nos centraremos en dos métodos de preprocesamiento de datos:

- Normalización
- Aumento de datos

## Normalización

La normalización es una técnica que se utiliza para cambiar la escala de los datos para que estén dentro de un rango específico. Hay muchas formas diferentes de normalizar los datos, pero el método más común es volver a escalar los datos al rango [0, 1].

Esto se puede hacer usando el método min-max, que vuelve a escalar los datos para que el valor mínimo sea 0 y el valor máximo sea 1.

Para hacer esto, primero necesitamos encontrar los valores mínimo y máximo de los datos. Luego podemos usar la siguiente fórmula para cambiar la escala de los datos:

```
x' = (x - min) / (max - min)
```

donde x son los datos originales, x' son los datos reescalados, min es el valor mínimo y max es el valor máximo.

Podemos usar el método min-max para cambiar la escala de los datos en nuestro conjunto de entrenamiento. Luego podemos usar los datos reescalados para entrenar nuestro algoritmo de aprendizaje automático.

## Aumento de datos

El aumento de datos es una técnica que se utiliza para aumentar artificialmente el tamaño de los datos de entrenamiento. Esto se hace creando nuevos puntos de datos a partir de los datos existentes.

Hay muchas formas diferentes de aumentar los datos. El método más común es usar transformaciones aleatorias para crear nuevos puntos de datos.

Por ejemplo, podríamos rotar aleatoriamente una imagen una pequeña cantidad para crear un nuevo punto de datos. También podríamos recortar aleatoriamente una imagen para crear un nuevo punto de datos.

El aumento de datos es una técnica poderosa que se puede utilizar para mejorar el rendimiento de los algoritmos de aprendizaje automático.

## Conclusión

En esta publicación, aprendimos sobre dos métodos de preprocesamiento de datos: normalización y aumento de datos. También aprendimos cómo implementar estos métodos en TensorFlow.js y Node.js.