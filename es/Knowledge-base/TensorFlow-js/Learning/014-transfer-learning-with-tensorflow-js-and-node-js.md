---
title: 014: Transferencia de aprendizaje con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T10:04:41.399Z
tags: 
editor: markdown
dateCreated: 2023-02-02T10:04:39.811Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [014: Transfer Learning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/014-transfer-learning-with-tensorflow-js-and-node-js)
{.links-list}


# Introducción

En esta publicación, veremos cómo usar el aprendizaje de transferencia con TensorFlow.js y Node.js. El aprendizaje por transferencia es una técnica poderosa que puede ayudarlo a acelerar el proceso de capacitación para sus propios modelos de aprendizaje automático. Al comenzar con un modelo previamente entrenado, puede ahorrar mucho tiempo y esfuerzo que, de lo contrario, se gastaría en entrenar un modelo desde cero.

En esta publicación, cubriremos los siguientes temas:

- ¿Qué es el aprendizaje por transferencia?
- Cómo usar el aprendizaje por transferencia con TensorFlow.js
- Cómo usar el aprendizaje por transferencia con Node.js

# ¿Qué es el aprendizaje por transferencia?

El aprendizaje por transferencia es una técnica de aprendizaje automático que le permite reutilizar un modelo previamente entrenado en un nuevo conjunto de datos. Esto es especialmente útil cuando no tiene suficientes datos para entrenar un modelo desde cero.

Hay dos tipos principales de transferencia de aprendizaje:

- **Ajuste fino:** Aquí es donde toma un modelo previamente entrenado y luego lo entrena en su propio conjunto de datos. Esto generalmente se usa cuando su conjunto de datos es similar al que se usó para entrenar el modelo previamente entrenado.
- **Extracción de características:** Aquí es donde toma un modelo previamente entrenado y lo usa para extraer características de su propio conjunto de datos. Por lo general, esto se usa cuando su conjunto de datos es diferente del que se usó para entrenar el modelo previamente entrenado.

# Cómo usar Transfer Learning con TensorFlow.js

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. Le permite usar el aprendizaje de transferencia con modelos de TensorFlow.js al proporcionar un conjunto de modelos previamente entrenados.

Los modelos preentrenados son modelos que han sido entrenados en un gran conjunto de datos y luego están disponibles para que otros los usen. Puede utilizar estos modelos como punto de partida para entrenar sus propios modelos.

Para usar un modelo previamente entrenado con TensorFlow.js, primero debe instalar la biblioteca TensorFlow.js. Puedes hacer esto usando el siguiente comando:

```
npm install @tensorflow/tfjs
```

Una vez que se instala la biblioteca TensorFlow.js, puede cargar un modelo previamente entrenado usando la función `loadModel()`. Por ejemplo, para cargar el modelo preentrenado de MobileNet, usaría el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MobileNet model.
const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

Una vez que se carga el modelo, puede usarlo para transferir el aprendizaje. Por ejemplo, puede usarlo para ajustar un modelo en su propio conjunto de datos.

# Cómo usar Transfer Learning con Node.js

Node.js es un tiempo de ejecución de JavaScript que le permite usar JavaScript para crear aplicaciones de red escalables.

Puede usar Node.js con TensorFlow.js para crear aplicaciones que utilicen el aprendizaje por transferencia. Para usar Node.js con TensorFlow.js, primero debe instalar la biblioteca TensorFlow.js. Puedes hacer esto usando el siguiente comando:

```
npm install @tensorflow/tfjs
```

Una vez que se instala la biblioteca TensorFlow.js, puede cargar un modelo previamente entrenado usando la función `loadModel()`. Por ejemplo, para cargar el modelo preentrenado de MobileNet, usaría el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MobileNet model.
const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

Una vez que se carga el modelo, puede usarlo para transferir el aprendizaje. Por ejemplo, puede usarlo para ajustar un modelo en su propio conjunto de datos.

# Conclusión

En esta publicación, analizamos cómo usar el aprendizaje por transferencia con TensorFlow.js y Node.js. El aprendizaje por transferencia es una técnica poderosa que puede ayudarlo a acelerar el proceso de capacitación para sus propios modelos de aprendizaje automático. Al comenzar con un modelo previamente entrenado, puede ahorrar mucho tiempo y esfuerzo que, de lo contrario, se gastaría en entrenar un modelo desde cero.