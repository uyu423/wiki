---
title: 037: Métricas de modelos personalizados con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T13:57:27.532Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:57:25.914Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [037: Custom Model Metrics with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/037-custom-model-metrics-with-tensorflow-js-and-node-js)
{.links-list}


# 037: Métricas de modelos personalizados con TensorFlow.js y Node.js

En esta publicación, aprenderemos a definir métricas de modelos personalizadas en TensorFlow.js y Node.js.

## ¿Qué son las métricas del modelo personalizado?

Las métricas del modelo personalizado son funciones que aceptan dos argumentos:

- `yTrue`: Los valores de verdad básicos.
- `yPred`: Los valores pronosticados.

Y devuelva un valor único que represente la métrica.

Por ejemplo, es posible que queramos definir una métrica personalizada que calcule el error cuadrático medio (MSE) entre los valores reales y los valores predichos. Podemos hacer esto definiendo la siguiente función:

```javascript
function mse(yTrue, yPred) {
  // ...
}
```

## Definición de métricas de modelos personalizados en TensorFlow.js

En TensorFlow.js, podemos definir métricas de modelos personalizadas creando un `CustomCallback` y pasándolo al método `fit`.

```javascript
const model = tf.sequential();
// ...

model.compile({
  // ...
  metrics: ['mse']
});

model.fit(x, y, {
  epochs: 10,
  callbacks: tf.callbacks.customCallback(['mse'], (logs) => {
    console.log(logs.mse);
  })
});
```

En el código anterior, hemos definido un `CustomCallback` que calcula la métrica `mse`. Luego pasamos esta devolución de llamada al método `fit`, que le dice al modelo que calcule la métrica `mse` durante el entrenamiento.

## Definición de métricas de modelos personalizados en Node.js

En Node.js, podemos definir métricas de modelo personalizadas creando una instancia `tf.Metrics` y pasándola al método `fit`.

```javascript
const model = tf.sequential();
// ...

model.compile({
  // ...
  metrics: ['mse']
});

const metrics = new tf.Metrics(['mse']);

model.fit(x, y, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      metrics.update(logs);
    }
  }
});

metrics.print();
```

En el código anterior, hemos creado una instancia `tf.Metrics` que calcula la métrica `mse`. Luego pasamos esta instancia al método `fit`, que le dice al modelo que calcule la métrica `mse` durante el entrenamiento.

## Conclusión

En esta publicación, aprendimos cómo definir métricas de modelos personalizadas en TensorFlow.js y Node.js.