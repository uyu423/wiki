---
title: 016: Detección de objetos con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T10:36:34.031Z
tags: 
editor: markdown
dateCreated: 2023-02-02T10:36:32.423Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [016: Object Detection with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/016-object-detection-with-tensorflow-js-and-node-js)
{.links-list}


# Detección de objetos con TensorFlow.js y Node.js

En esta publicación, aprenderemos a usar TensorFlow.js y Node.js para realizar la detección de objetos en tiempo real en las imágenes.

Comenzaremos configurando un entorno de desarrollo, luego instalaremos TensorFlow.js y sus dependencias. A continuación, escribiremos un script de Node.js para cargar una imagen, ejecutar la detección de objetos en ella y dibujar los resultados en la pantalla. Por último, echaremos un vistazo a algunos de los recursos disponibles para seguir aprendiendo.

## Configuración del entorno de desarrollo

Antes de comenzar, debemos configurar un entorno de desarrollo. Para esta publicación, usaremos Node.js.

Si aún no tiene instalado Node.js, puede descargarlo del [sitio web de Node.js] (https://nodejs.org/en/). Una vez que haya instalado Node.js, puede crear un nuevo directorio de proyecto e inicializarlo con los siguientes comandos:

```
mkdir object-detection
cd object-detection
npm init -y
```

## Instalación de TensorFlow.js y sus dependencias

Ahora que tenemos un directorio de proyecto configurado, podemos instalar TensorFlow.js y sus dependencias. Usaremos el paquete [tfjs-node](https://www.npmjs.com/package/@tensorflow/tfjs-node), que proporciona una implementación de TensorFlow.js que se puede usar en Node.js.

Para instalar tfjs-node y sus dependencias, ejecute el siguiente comando:

```
npm install @tensorflow/tfjs-node
```

## Escribir el script de detección de objetos

Con TensorFlow.js instalado, ahora podemos escribir un script para realizar la detección de objetos en las imágenes. Comenzaremos cargando una imagen, luego usaremos el método [tf.data.detectObjects](https://js.tensorflow.org/api/latest/# tf.data.detectObjects) para ejecutar la detección de objetos en la imagen. Finalmente, dibujaremos los resultados en la pantalla.

El script completo está disponible [aquí](https://github.com/tensorflow/tfjs-models/blob/master/tfjs-models/src/object_detection/index.js), pero veremos las partes clave a continuación. .

Primero, necesitamos cargar el paquete tfjs-node:

```javascript
const tf = require('@tensorflow/tfjs-node');
```

A continuación, cargaremos el [modelo coco-ssd](https://github.com/tensorflow/tfjs-models/tree/master/tfjs-models/detection), que usaremos para la detección de objetos. El modelo coco-ssd es un modelo de detección de disparo único que se entrena en el [conjunto de datos de objetos comunes en contexto (COCO)] (http://cocodataset.org/# home).

```javascript
const cocoSSD = require('@tensorflow-models/coco-ssd');
```

Con el modelo cargado, ahora podemos escribir el código para cargar una imagen y ejecutar la detección de objetos en ella. Comenzaremos cargando la imagen usando el método [tf.node.decodeImage](https://js.tensorflow.org/api/latest/# tf.node.decodeImage). Este método devuelve una promesa que se resuelve en un tensor que contiene los datos de la imagen.

```javascript
const image = tf.node.decodeImage(
  fs.readFileSync('./test-image.jpg')
);
```

Una vez que se carga la imagen, podemos usar el método [tf.data.detectObjects](https://js.tensorflow.org/api/latest/# tf.data.detectObjects) para ejecutar la detección de objetos en ella. Este método devuelve una promesa que se resuelve en una matriz de objetos, cada uno de los cuales contiene información sobre un objeto detectado, incluida la clase del objeto y su ubicación dentro de la imagen.

```javascript
const predictions = await cocoSSD.detectObjects(image);
```

Finalmente, dibujaremos los resultados en la pantalla. Usaremos el método [tf.node.drawBoxes](https://js.tensorflow.org/api/latest/# tf.node.drawBoxes) para dibujar cuadros alrededor de los objetos detectados, y el método [tf.node. writeFile](https://js.tensorflow.org/api/latest/#tf.node.writeFile) para escribir los resultados en un nuevo archivo de imagen.

```javascript
const drawnImage = tf.node.drawBoxes(
  image,
  predictions.map(prediction => prediction.bbox)
);
tf.node.writeFile('./test-image-output.jpg', drawnImage.toBuffer());
```

## Ejecutar el script de detección de objetos

Con el script escrito, ahora podemos ejecutarlo para realizar la detección de objetos en una imagen. Para ejecutar el script, use el siguiente comando:

```
node index.js
```

Esto ejecutará el script de detección de objetos en la imagen `test-image.jpg` y escribirá los resultados en `test-image-output.jpg`.

## Recursos para seguir aprendiendo

- [Detección de objetos TensorFlow.js](https://js.tensorflow.org/tutorials/object-detection.html)
- [Detección de objetos en tiempo real con TensorFlow.js y Node.js](https://www.twilio.com/blog/real-time-object-detection-tensorflow-js-node-js)
- [Detectar objetos usando su cámara web] (https://codelabs.developers.google.com/codelabs/tensorflowjs-object-detection/index.html)