---
title: 022: Reconocimiento de voz con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T12:04:36.284Z
tags: 
editor: markdown
dateCreated: 2023-02-02T12:04:34.681Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [022: Speech Recognition with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/022-speech-recognition-with-tensorflow-js-and-node-js)
{.links-list}


# 022: Reconocimiento de voz con TensorFlow.js y Node.js

En esta publicación, veremos cómo usar TensorFlow.js y Node.js para crear un sistema de reconocimiento de voz.

Comenzaremos viendo cómo configurar el entorno, luego entraremos en el código.

## Configuración del entorno

Lo primero que debemos hacer es instalar TensorFlow.js. Podemos hacerlo con el siguiente comando:

```
npm install @tensorflow/tfjs
```

Una vez hecho esto, debemos instalar los enlaces de Node.js para TensorFlow.js. Podemos hacerlo con el siguiente comando:

```
npm install @tensorflow/tfjs-node
```

Con eso fuera del camino, ahora podemos pasar al código.

## El código

Comenzaremos cargando la biblioteca TensorFlow.js y los enlaces de Node.js. Podemos hacerlo con el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs');
require('@tensorflow/tfjs-node');
```

A continuación, necesitaremos cargar la biblioteca de reconocimiento de voz. Podemos hacerlo con el siguiente código:

```javascript
const speech = require('@tensorflow-models/speech-commands');
```

Con eso fuera del camino, ahora podemos pasar a la parte divertida: el código.

Comenzaremos creando un nuevo modelo de reconocimiento de voz. Podemos hacerlo con el siguiente código:

```javascript
const model = speech.createModel();
```

A continuación, necesitaremos entrenar el modelo. Podemos hacerlo con el siguiente código:

```javascript
model.train({
  fileNames: [
    'file1.wav',
    'file2.wav',
    'file3.wav',
  ],
  labels: [
    'label1',
    'label2',
    'label3',
  ]
});
```

Una vez que el modelo está entrenado, ahora podemos usarlo para reconocer el habla. Podemos hacerlo con el siguiente código:

```javascript
model.recognize(audio, (err, result) => {
  if (err) {
    console.error(err);
  } else {
    console.log(result);
  }
});
```

¡Y eso es! Ahora tiene un sistema de reconocimiento de voz en funcionamiento.

## Conclusión

En esta publicación, hemos visto cómo usar TensorFlow.js y Node.js para construir un sistema de reconocimiento de voz. Comenzamos viendo cómo configurar el entorno, luego nos metimos en el código.

Si está interesado en obtener más información, le recomiendo consultar los siguientes recursos:

- La documentación oficial de TensorFlow.js: https://js.tensorflow.org/
- Los enlaces oficiales de Node.js para la documentación de TensorFlow.js: https://js.tensorflow.org/tfjs-node/
- La documentación oficial de la biblioteca de reconocimiento de voz: https://js.tensorflow.org/speech-commands/