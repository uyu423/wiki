---
title: 069: Escalado de aplicaciones TensorFlow.js con Node.js
description: 
published: true
date: 2023-02-02T23:04:23.382Z
tags: 
editor: markdown
dateCreated: 2023-02-02T23:04:21.726Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [069: Scaling TensorFlow.js Applications with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/069-scaling-tensorflow-js-applications-with-node-js)
{.links-list}


# 069: Escalado de aplicaciones TensorFlow.js con Node.js

TensorFlow.js es una poderosa herramienta para el aprendizaje automático en JavaScript, pero ¿qué haces cuando tu aplicación TensorFlow.js supera al navegador? En esta publicación, exploraremos cómo escalar las aplicaciones de TensorFlow.js con Node.js.

## ¿Qué es TensorFlow.js?

TensorFlow.js es una biblioteca de código abierto para el aprendizaje automático en JavaScript. Los desarrolladores lo utilizan para crear modelos sofisticados de aprendizaje automático que se ejecutan en el navegador o en Node.js.

## ¿Por qué usar Node.js para TensorFlow.js?

Node.js es una excelente opción para escalar aplicaciones de TensorFlow.js. Es rápido, eficiente y tiene un gran ecosistema de bibliotecas y herramientas.

## Cómo escalar TensorFlow.js con Node.js

Hay dos formas principales de escalar las aplicaciones de TensorFlow.js con Node.js:

1. Utilice el módulo `tensorflow.js` de Node.js.
2. Use una biblioteca compatible con TensorFlow.js como `tfjs-node`.

Exploraremos cada uno de estos métodos con más detalle a continuación.

### Usando el módulo `tensorflow.js` de Node.js

El módulo `tensorflow.js` de Node.js es la forma oficial de ejecutar TensorFlow.js en Node.js. Es fácil de instalar y usar.

Para instalar el módulo `tensorflow.js` Node.js, ejecute el siguiente comando:

```
npm install @tensorflow/tfjs
```

Para usar el módulo Node.js `tensorflow.js`, pídelo en tu código:

```javascript
const tf = require('@tensorflow/tfjs');
```

Ahora puede usar todas las API de TensorFlow.js en su aplicación Node.js.

### Uso de una biblioteca compatible con TensorFlow.js

Si desea utilizar una biblioteca compatible con TensorFlow.js como `tfjs-node`, primero deberá instalarla.

Para instalar `tfjs-node`, ejecute el siguiente comando:

```
npm install tfjs-node
```

Para usar `tfjs-node`, exíjalo en su código:

```javascript
const tf = require('tfjs-node');
```

Ahora puede usar todas las API de TensorFlow.js en su aplicación Node.js.

## Recursos para leer más

- [Documentación de TensorFlow.js](https://js.tensorflow.org/)
- [documentación de tfjs-node](https://github.com/tensorflow/tfjs-node)
- [Documentación de Node.js](https://nodejs.org/en/docs/)