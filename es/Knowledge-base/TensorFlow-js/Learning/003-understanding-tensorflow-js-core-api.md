---
title: 003: comprensión de la API principal de TensorFlow.js
description: 
published: true
date: 2023-02-02T07:23:28.201Z
tags: 
editor: markdown
dateCreated: 2023-02-02T07:23:26.578Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [003: Understanding TensorFlow.js Core API***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/003-understanding-tensorflow-js-core-api)
{.links-list}


# Comprender la API principal de TensorFlow.js

TensorFlow.js es un marco web de código abierto que permite a los desarrolladores entrenar e implementar modelos de aprendizaje automático en el navegador. La API principal de TensorFlow.js es una API de bajo nivel que permite a los desarrolladores crear, manipular y optimizar cálculos numéricos en JavaScript.

## ¿Qué es un tensor?

Un tensor es una estructura de datos que representa una transformación lineal. En términos simples, un tensor es una matriz de números. En TensorFlow.js, un tensor tiene una forma y un tipo de datos. La forma de un tensor es el tamaño y la dimensionalidad de la matriz, y el tipo de datos es el tipo de datos que contiene el tensor (por ejemplo, `float32`, `int32`, `string`).

## Creando tensores

Hay algunas formas de crear tensores en TensorFlow.js. La forma más sencilla es crear un tensor a partir de una matriz de JavaScript utilizando la función `tf.tensor`:

```javascript
const a = tf.tensor([1, 2, 3, 4]);
```

La función `tf.tensor` también te permite especificar la forma y el tipo de datos del tensor:

```javascript
const b = tf.tensor([1, 2, 3, 4], [2, 2], 'int32');
```

También puedes crear un tensor a partir de un escalar (un solo número):

```javascript
const c = tf.scalar(5);
```

## Manipulación de tensores

Los tensores se pueden manipular mediante una variedad de funciones en la API de TensorFlow.js. Por ejemplo, puede agregar dos tensores usando la función `tf.add`:

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = tf.tensor([5, 6, 7, 8]);
const c = tf.add(a, b);
```

También puede realizar operaciones por elementos en tensores. Las operaciones elementales son operaciones que se aplican a cada elemento del tensor de forma independiente. Por ejemplo, puedes multiplicar dos tensores por elementos usando la función `tf.mul`:

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = tf.tensor([5, 6, 7, 8]);
const c = tf.mul(a, b);
```

## Conversión de tensores

Los tensores se pueden convertir a otras estructuras de datos usando los métodos `.toXXX`. Por ejemplo, puedes convertir un tensor en una matriz de JavaScript utilizando el método `.toArray`:

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = a.toArray(); // [1, 2, 3, 4]
```

También puedes convertir un tensor en una cadena usando el método `.toString`:

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = a.toString(); // "1 2 3 4"
```

## Optimización de cálculos

TensorFlow.js proporciona una variedad de funciones de optimización que se pueden usar para optimizar los cálculos numéricos. Por ejemplo, puede usar la función `tf.clipByValue` para recortar valores de tensor a un rango específico:

```javascript
const a = tf.tensor([-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]);
const b = tf.clipByValue(a, -2, 2);
```

También puede usar la función `tf.addN` para realizar sumas por elementos en una lista de tensores:

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = tf.tensor([5, 6, 7, 8]);
const c = tf.tensor([9, 10, 11, 12]);
const d = tf.addN([a, b, c]);
```

## Aprendiendo más

TensorFlow.js es una poderosa herramienta que permite a los desarrolladores crear, manipular y optimizar cálculos numéricos en JavaScript. La API principal de TensorFlow.js es una API de bajo nivel que proporciona los componentes básicos para crear, manipular y optimizar cálculos numéricos en JavaScript.

Si desea obtener más información sobre TensorFlow.js, le recomendamos que consulte los siguientes recursos:

- La documentación de TensorFlow.js: https://js.tensorflow.org/
- El repositorio TensorFlow.js GitHub: https://github.com/tensorflow/tfjs
- La referencia de la API principal de TensorFlow.js: https://js.tensorflow.org/api/core.html