---
title: 017: Segmentación de imágenes con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T10:44:35.950Z
tags: 
editor: markdown
dateCreated: 2023-02-02T10:44:34.207Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [017: Image Segmentation with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/017-image-segmentation-with-tensorflow-js-and-node-js)
{.links-list}


# Introducción

En esta publicación, veremos cómo realizar la segmentación de imágenes con TensorFlow.js y Node.js. La segmentación de imágenes es el proceso de dividir una imagen en distintas regiones. Esto se usa a menudo en aplicaciones de visión por computadora para identificar objetos en una imagen.

Usaremos la biblioteca [TensorFlow.js](https://js.tensorflow.org/) para la segmentación de imágenes. TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. Se usa tanto para el aprendizaje profundo en el navegador como para Node.js.

Usaremos el tiempo de ejecución [Node.js](https://nodejs.org/) para nuestro ejemplo. Node.js es un tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript fuera del navegador. A menudo se usa para la programación del lado del servidor.

## Empezando

Antes de comenzar, debemos instalar las dependencias de TensorFlow.js y Node.js. Podemos hacer esto usando el administrador de paquetes [npm](https://www.npmjs.com/).

Primero, crea un nuevo directorio para nuestro proyecto:

```
mkdir image-segmentation
```

A continuación, debemos inicializar un nuevo proyecto npm. Esto lo podemos hacer ejecutando el siguiente comando:

```
npm init -y
```

Esto creará un nuevo archivo llamado `package.json` en nuestro directorio de proyectos. Este archivo contiene información sobre nuestro proyecto, como las dependencias que necesitamos instalar.

Ahora, podemos instalar las dependencias de TensorFlow.js y Node.js. Usaremos el paquete [tfjs-node](https://www.npmjs.com/package/@tensorflow/tfjs-node), que nos permite ejecutar TensorFlow.js en Node.js.

Para instalar las dependencias, ejecute el siguiente comando:

```
npm install @tensorflow/tfjs-node
```

Esto instalará las dependencias de TensorFlow.js y Node.js en nuestro proyecto.

## Cargando una imagen

Ahora que tenemos nuestras dependencias instaladas, podemos comenzar a escribir nuestro programa de segmentación de imágenes.

Primero, necesitamos cargar una imagen. Usaremos la función [tf.node.decodeImage](https://js.tensorflow.org/api/latest/# node.decodeImage) para cargar nuestra imagen. Esta función toma un "búfer" que contiene los datos de la imagen y devuelve un "tf.Tensor3D" que contiene los datos de la imagen.

Podemos leer nuestros datos de imagen usando el módulo [fs](https://nodejs.org/api/fs.html), que es parte de la biblioteca estándar de Node.js. La función [fs.readFile](https://nodejs.org/api/fs.html# fs_fs_readfile_path_options_callback) toma una ruta a la imagen y devuelve los datos de la imagen como un "búfer".

Para usar el módulo `fs`, necesitamos importarlo a nuestro programa. Podemos hacer esto usando la función [require](https://nodejs.org/api/modules.html# modules_require_id).

```javascript
const fs = require('fs');
```

Ahora que hemos importado el módulo `fs`, podemos usar la función `fs.readFile` para leer nuestros datos de imagen.

```javascript
const imageData = fs.readFileSync('image.jpg');
```

La variable `imageData` ahora contiene nuestros datos de imagen como `buffer`.

A continuación, necesitamos decodificar los datos de nuestra imagen. Podemos hacer esto usando la función `tf.node.decodeImage`.

```javascript
const imageTensor = tf.node.decodeImage(imageData);
```

La variable `imageTensor` ahora contiene nuestros datos de imagen como `tf.Tensor3D`.

## Preprocesamiento de la imagen

Antes de que podamos realizar la segmentación de imágenes, necesitamos preprocesar nuestra imagen. Esto implica realizar algunas operaciones en nuestros datos de imagen para prepararlos para la segmentación.

Primero, necesitamos cambiar el tamaño de nuestra imagen. Usaremos la función [tf.image.resizeBilinear](https://js.tensorflow.org/api/latest/# tf.image.resizeBilinear) para cambiar el tamaño de nuestra imagen. Esta función toma una imagen `tf.Tensor` y un tamaño (`[alto, ancho]`) y devuelve una imagen redimensionada `tf.Tensor`.

Cambiaremos el tamaño de nuestra imagen a un tamaño de `[128, 128]`.

```javascript
const imageSize = [128, 128];
const imageTensor = tf.image.resizeBilinear(imageTensor, imageSize);
```

La variable `imageTensor` ahora contiene nuestros datos de imagen redimensionados como `tf.Tensor3D`.

A continuación, necesitamos normalizar los datos de nuestra imagen. Usaremos la función [tf.image.normalize](https://js.tensorflow.org/api/latest/# tf.image.normalize) para normalizar nuestra imagen. Esta función toma una imagen `tf.Tensor` y devuelve una imagen normalizada `tf.Tensor`.

Normalizaremos nuestra imagen restando la media y dividiendo por la desviación estándar.

```javascript
const imageTensor = tf.image.normalize(imageTensor, [0, 255], -1, 1);
```

La variable `imageTensor` ahora contiene nuestros datos de imagen normalizados como `tf.Tensor3D`.

## Realización de segmentación de imágenes

Ahora que hemos preprocesado nuestra imagen, podemos realizar la segmentación de la imagen. Usaremos la función [tf.image.segmentation.segmentationKMeans](https://js.tensorflow.org/api/latest/# tf.image.segmentation.segmentationKMeans) para realizar la segmentación de imágenes. Esta función toma una imagen `tf.Tensor` y devuelve un mapa de segmentación `tf.Tensor`.

Segmentaremos nuestra imagen en `4` regiones.

```javascript
const numSegments = 4;
const segmentationMap = tf.image.segmentation.segmentationKMeans(imageTensor, numSegments);
```

La variable `segmentationMap` ahora contiene nuestro mapa de segmentación como `tf.Tensor3D`.

## Visualización del mapa de segmentación

Ahora que hemos segmentado nuestra imagen, necesitamos visualizar el mapa de segmentación. Podemos hacer esto usando la función [tf.tensor3d](https://js.tensorflow.org/api/latest/# tf.tensor3d). Esta función toma una matriz de números y devuelve un `tf.Tensor3D`.

Primero, necesitamos convertir nuestro mapa de segmentación `tf.Tensor` en una matriz. Podemos hacer esto usando la función [tf.tensor3d](https://js.tensorflow.org/api/latest/# tf.tensor3d).

```javascript
const segmentationMapArray = segmentationMap.arraySync();
```

La variable `segmentationMapArray` ahora contiene nuestro mapa de segmentación como una matriz.

A continuación, debemos convertir nuestra matriz de mapas de segmentación en `tf.Tensor3D`. Podemos hacer esto usando la función [tf.tensor3d](https://js.tensorflow.org/api/latest/# tf.tensor3d).

```javascript
const segmentationMapTensor = tf.tensor3d(segmentationMapArray);
```

La variable `segmentationMapTensor` ahora contiene nuestro mapa de segmentación como `tf.Tensor3D`.

Finalmente, podemos visualizar nuestro mapa de segmentación usando la función [tf.image.resizeBilinear](https://js.tensorflow.org/api/latest/# tf.image.resizeBilinear). Esta función toma una imagen `tf.Tensor` y un tamaño (`[alto, ancho]`) y devuelve una imagen redimensionada `tf.Tensor`.

Cambiaremos el tamaño de nuestro mapa de segmentación al tamaño original de nuestra imagen.

```javascript
const segmentationMapImage = tf.image.resizeBilinear(segmentationMapTensor, [imageHeight, imageWidth]);
```

La variable `segmentationMapImage` ahora contiene nuestro mapa de segmentación como `tf.Tensor3D`.

## Guardar el mapa de segmentación

Ahora que hemos visualizado nuestro mapa de segmentación, debemos guardarlo. Podemos hacer esto usando la función [tf.node.encodePng](https://js.tensorflow.org/api/latest/# node.encodePng). Esta función toma una imagen `tf.Tensor` y devuelve un `buffer` que contiene los datos PNG.

Podemos escribir estos datos en un archivo usando el módulo [fs](https://nodejs.org/api/fs.html). La función [fs.writeFile](https://nodejs.org/api/fs.html# fs_fs_writefile_file_data_options_callback) toma una ruta al archivo, los datos para escribir y una función de devolución de llamada.

Para usar el módulo `fs`, necesitamos importarlo a nuestro programa. Podemos hacer esto usando la función [require](https://nodejs.org/api/modules.html# modules_require_id).

```javascript
const fs = require('fs');
```

Ahora que hemos importado el módulo `fs`, podemos usar la función `fs.writeFile` para escribir nuestros datos del mapa de segmentación en un archivo.

```javascript
const segmentationMapData = tf.node.encodePng(segmentationMapImage);
fs.writeFileSync('segmentation-map.png', segmentationMapData);
```

Esto escribirá los datos de nuestro mapa de segmentación en un archivo llamado `segmentation-map.png`.

## Conclusión

En esta publicación, hemos visto cómo realizar la segmentación de imágenes usando TensorFlow.js y Node.js. También hemos visto cómo visualizar el mapa de segmentación y guardarlo en un archivo.

La segmentación de imágenes es una poderosa herramienta para aplicaciones de visión artificial. TensorFlow.js facilita la segmentación de imágenes en el navegador y en Node.js.