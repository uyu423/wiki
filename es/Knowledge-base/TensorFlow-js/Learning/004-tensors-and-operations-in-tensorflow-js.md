---
title: 004: Tensores y Operaciones en TensorFlow.js
description: 
published: true
date: 2023-02-02T07:36:26.999Z
tags: 
editor: markdown
dateCreated: 2023-02-02T07:36:25.431Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [004: Tensors and Operations in TensorFlow.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/004-tensors-and-operations-in-tensorflow-js)
{.links-list}


# Introducción

TensorFlow.js es una poderosa biblioteca de JavaScript para el aprendizaje automático y una de sus características clave es la capacidad de trabajar con tensores. En esta publicación, veremos qué son los tensores y cómo trabajar con ellos en TensorFlow.js.

# ¿Qué es un tensor?

Un tensor es una generalización de un vector. Los vectores a menudo se consideran matrices unidimensionales de números, pero los tensores se pueden considerar como matrices de cualquier dimensión. Así como los vectores se pueden sumar y multiplicar por escalares, también los tensores.

Los tensores se usan a menudo en el aprendizaje automático porque se pueden usar para representar datos de varias maneras. Por ejemplo, una imagen se puede representar como un tensor tridimensional, siendo la altura, el ancho y la profundidad de la imagen las tres dimensiones.

# TensorFlow.js

TensorFlow.js es una biblioteca de JavaScript para aprendizaje automático que le permite trabajar con tensores de varias maneras. En esta publicación, veremos algunas de las formas en que puede trabajar con tensores en TensorFlow.js.

# Creando Tensores

Los tensores se pueden crear a partir de matrices de JavaScript utilizando la función tf.tensor. Por ejemplo, el siguiente código crea un tensor bidimensional con los valores 1, 2, 3 y 4:

```javascript
const t = tf.tensor([[1, 2], [3, 4]]);
```

También puede crear tensores con valores específicos utilizando las funciones tf.ones, tf.zeros y tf.fill. Por ejemplo, el siguiente código crea un tensor bidimensional con los valores 1, 0, 1 y 0:

```javascript
const t = tf.ones([2, 2]);
```

# Manipulación de tensores

Los tensores se pueden manipular de varias maneras. La forma más común de manipular un tensor es usar la función tf.transpose. Esta función permuta las dimensiones de un tensor. Por ejemplo, el siguiente código crea un tensor bidimensional con los valores 1, 2, 3 y 4 y luego permuta las dimensiones para crear un nuevo tensor con los valores 1, 3, 2 y 4:

```javascript
const t = tf.tensor([[1, 2], [3, 4]]);
const t2 = t.transpose();
```

Los tensores también se pueden remodelar usando la función tf.reshape. Esta función devuelve un nuevo tensor con los mismos valores que el tensor original pero con una forma diferente. Por ejemplo, el siguiente código crea un tensor bidimensional con los valores 1, 2, 3 y 4 y luego lo transforma en un tensor unidimensional con los valores 1, 2, 3, 4:

```javascript
const t = tf.tensor([[1, 2], [3, 4]]);
const t2 = t.reshape([4]);
```

# Trabajar con tensores en TensorFlow.js

TensorFlow.js proporciona una variedad de funciones para trabajar con tensores. En esta sección, echaremos un vistazo a algunas de las funciones más utilizadas.

La función tf.tensor se puede usar para crear un tensor a partir de una matriz de JavaScript. Las funciones tf.ones y tf.zeros se pueden usar para crear tensores con todos unos o todos ceros, respectivamente. La función tf.fill se puede usar para crear un tensor con un valor dado.

La función tf.transpose se puede utilizar para permutar las dimensiones de un tensor. La función tf.reshape se puede usar para remodelar un tensor.

La función tf.concat se puede utilizar para concatenar dos o más tensores a lo largo de una dimensión determinada. La función tf.split se puede usar para dividir un tensor a lo largo de una dimensión determinada.

Las funciones tf.add, tf.sub, tf.mul y tf.div se pueden usar para realizar sumas, restas, multiplicaciones y divisiones por elementos en dos tensores, respectivamente.

La función tf.matMul se puede utilizar para realizar una multiplicación de matrices en dos tensores bidimensionales.

La función tf.sum se puede utilizar para calcular la suma de todos los elementos de un tensor. La función tf.mean se puede utilizar para calcular la media de todos los elementos de un tensor.

# Conclusión

En esta publicación, analizamos qué son los tensores y cómo trabajar con ellos en TensorFlow.js. Hemos visto cómo crear tensores y cómo manipularlos. También vimos cómo trabajar con tensores en TensorFlow.js usando una variedad de funciones.