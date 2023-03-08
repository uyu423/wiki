---
title: 036: Uso de modelos previamente entrenados con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T15:36:43.939Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:36:42.354Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [036: Using Pretrained Models with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/036-using-pretrained-models-with-tensorflow-js-and-node-js)
{.links-list}


# Introducción

En esta publicación, aprenderemos a usar modelos previamente entrenados con TensorFlow.js y Node.js. Comenzaremos analizando qué son los modelos preentrenados y por qué son útiles. Luego veremos cómo cargar y usar modelos previamente entrenados en TensorFlow.js. Finalmente, veremos cómo implementar un modelo previamente entrenado con Node.js.

# ¿Qué son los modelos preentrenados?

Los modelos preentrenados son modelos que han sido entrenados en un gran conjunto de datos. Estos modelos se pueden utilizar para realizar diversas tareas, como la clasificación de imágenes, la detección de objetos y la clasificación de textos.

Los modelos previamente entrenados son útiles porque nos permiten usar el conocimiento de un gran conjunto de datos sin tener que entrenar nuestro propio modelo desde cero. Esto puede ahorrarnos mucho tiempo y esfuerzo.

# Cargando modelos preentrenados

TensorFlow.js proporciona una serie de modelos preentrenados que se pueden cargar y usar en sus propias aplicaciones. Para cargar un modelo previamente entrenado, primero deberá instalar TensorFlow.js. Puedes hacer esto usando npm:

```
npm install @tensorflow/tfjs
```

Una vez que se instala TensorFlow.js, puede cargar un modelo previamente entrenado mediante la función tf.loadModel(). Por ejemplo, para cargar el modelo MobileNet, usaría el siguiente código:

```javascript
const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

# Uso de modelos preentrenados

Una vez que haya cargado un modelo previamente entrenado, puede usarlo para realizar varias tareas. Por ejemplo, si usa un modelo de clasificación de imágenes entrenado previamente, puede usar el modelo para clasificar imágenes.

Para usar un modelo previamente entrenado, primero deberá obtener las capas de entrada y salida del modelo. Puede hacer esto usando las propiedades model.inputs y model.outputs. Por ejemplo, para obtener las capas de entrada y salida del modelo MobileNet, usaría el siguiente código:

```javascript
const inputLayer = model.inputs[0];
const outputLayer = model.outputs[0];
```

Una vez que tenga las capas de entrada y salida del modelo, puede usar la función tf.tidy() para ejecutar la inferencia. La función tf.tidy() limpiará cualquier tensor tf.js que se cree durante el proceso de inferencia. Esto es importante porque los tensores tf.js pueden ocupar mucha memoria.

Para usar la función tf.tidy(), deberá pasar una función que contenga el código para ejecutar la inferencia. Esta función se ejecutará dentro de un contexto ordenado. Por ejemplo, para ejecutar la inferencia en el modelo MobileNet, usaría el siguiente código:

```javascript
const results = tf.tidy(() => {
  // inputLayer is a tf.js Tensor with shape [1, 224, 224, 3]
  // outputLayer is a tf.js Tensor with shape [1, 1000]
  const output = model.predict(inputLayer);
  return output.dataSync();
});
```

# Implementación de modelos preentrenados

Una vez que haya entrenado un modelo, deberá implementarlo para que otras aplicaciones puedan usarlo. TensorFlow.js proporciona varias formas de implementar modelos previamente entrenados.

Una forma de implementar un modelo previamente entrenado es usar la función tf.model.save(). Esta función guardará el modelo en un archivo JSON. Por ejemplo, para guardar el modelo de MobileNet, usaría el siguiente código:

```javascript
await model.save('file:///model');
```

A continuación, puede cargar el modelo desde el archivo JSON mediante la función tf.loadModel().

Otra forma de implementar un modelo previamente entrenado es usar la función tf.model.toJSON(). Esta función devolverá el modelo como un objeto JSON. Por ejemplo, para obtener el modelo de MobileNet como un objeto JSON, usaría el siguiente código:

```javascript
const modelAsJSON = model.toJSON();
```

Luego puede guardar el objeto JSON en un archivo o base de datos.

# Conclusión

En esta publicación, aprendimos a usar modelos previamente entrenados con TensorFlow.js y Node.js. Hemos visto cómo cargar y usar modelos preentrenados y cómo implementar modelos preentrenados.