---
title: 010: memoria a largo plazo (LSTM) con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T09:04:29.074Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:04:24.714Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [010: Long Short-Term Memory (LSTM) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/010-long-short-term-memory-lstm-with-tensorflow-js-and-node-js)
{.links-list}


# Memoria a corto plazo (LSTM) con TensorFlow.js y Node.js

En esta publicación, aprenderemos sobre las redes de memoria a corto plazo (LSTM) con TensorFlow.js y Node.js. Repasaremos qué son las redes LSTM, cómo funcionan y cómo capacitarlas. Al final de esta publicación, debe tener una buena comprensión de cómo usar las redes LSTM y cómo se pueden aplicar a diferentes problemas.

## ¿Qué son las redes LSTM?

Las redes LSTM son un tipo de red neuronal recurrente (RNN). Las RNN son redes neuronales que pueden procesar datos secuenciales, como datos de series temporales o texto. Las redes LSTM son un tipo especial de RNN que pueden aprender dependencias a largo plazo. Esto significa que pueden recordar información durante largos períodos de tiempo, lo cual es útil para tareas como la predicción y la clasificación.

## ¿Cómo funcionan las redes LSTM?

Las redes LSTM están compuestas por celdas LSTM. Cada celda LSTM tiene un estado de celda y una puerta de entrada, una puerta de salida y una puerta de olvido. El estado de la celda es como una memoria que puede almacenar información durante largos períodos de tiempo. La puerta de entrada controla cuánta información de la entrada actual se almacena en el estado de la celda. La puerta de salida controla la cantidad de información del estado de la celda que se emite. La puerta de olvido controla cuánta información del estado de celda anterior se olvida.

![Celda LSTM](https://raw.githubusercontent.com/tensorflow/tfjs-layers/master/resources/lstm_cell.png)

Las redes LSTM utilizan estas puertas para controlar el flujo de información en la red. Esto les permite aprender dependencias a largo plazo.

## ¿Cómo entrenar redes LSTM?

Las redes LSTM se pueden entrenar usando una variedad de métodos. El método más común es usar retropropagación a través del tiempo (BPTT). BPTT es un método de entrenamiento de RNN donde los gradientes se propagan hacia atrás en el tiempo. Esto permite que la red aprenda de largas secuencias de datos.

## Conclusión

En esta publicación, aprendimos sobre las redes de memoria a corto plazo. Discutimos qué son, cómo funcionan y cómo entrenarlos. Las redes LSTM son una poderosa herramienta para aprender a partir de datos secuenciales.