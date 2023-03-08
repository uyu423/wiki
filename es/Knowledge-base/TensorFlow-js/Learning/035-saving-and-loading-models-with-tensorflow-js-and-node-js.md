---
title: 035: Guardar y cargar modelos con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T15:17:20.363Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:17:18.814Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [035: Saving and Loading Models with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/035-saving-and-loading-models-with-tensorflow-js-and-node-js)
{.links-list}


## Guardar y cargar modelos con TensorFlow.js y Node.js

En esta publicación, aprenderemos cómo guardar y cargar modelos con TensorFlow.js y Node.js. Cubriremos los siguientes temas:

- Guardar un modelo con TensorFlow.js
- Cargando un modelo con TensorFlow.js
- Usando un modelo con Node.js

### Guardar un modelo con TensorFlow.js

El primer paso es guardar nuestro modelo. Podemos hacer esto con el método `tf.Model.save`. Este método toma dos argumentos:

- `ruta`: La ruta para guardar el modelo.
- `overwrite`: un valor booleano que indica si se sobrescribe o no el modelo existente en la ruta especificada.

Aquí hay un ejemplo de cómo guardar un modelo:

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

model.save('/tmp/model/1/model.json', true);
```

En este ejemplo, hemos guardado nuestro modelo en el directorio `/tmp/model/1`. El parámetro `overwrite` se establece en `true`, por lo que si ya hubiera un modelo en ese directorio, se sobrescribiría.

### Cargando un modelo con TensorFlow.js

Ahora que hemos guardado nuestro modelo, aprendamos cómo cargarlo. Podemos hacer esto con el método `tf.loadModel`. Este método toma un argumento:

- `ruta`: La ruta al modelo guardado.

Aquí hay un ejemplo de cómo cargar un modelo:

```javascript
const model = await tf.loadModel('/tmp/model/1/model.json');
```

En este ejemplo, hemos cargado nuestro modelo desde el directorio `/tmp/model/1`.

### Usando un modelo con Node.js

Una vez que hayamos cargado nuestro modelo, podemos usarlo para hacer predicciones. Podemos hacer esto con el método `model.predict`. Este método toma un argumento:

- `entradas`: Los datos de entrada para hacer predicciones. Puede ser un solo `tf.Tensor` o un `Array` de `tf.Tensor`s.

Este es un ejemplo del uso de un modelo para hacer predicciones:

```javascript
const input = tf.tensor2d([[1.0]]);
const output = model.predict(input);

output.print();
```

En este ejemplo, hemos creado un `tf.Tensor` con el valor `[[1.0]]`. Hemos pasado este tensor al método `model.predict`, que devuelve una predicción. Luego imprimimos la predicción en la consola.