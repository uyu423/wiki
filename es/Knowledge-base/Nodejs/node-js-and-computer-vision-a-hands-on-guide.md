---
title: Node.js y Computer Vision: una guía práctica
description: 
published: true
date: 2023-02-09T04:18:36.032Z
tags: 
editor: markdown
dateCreated: 2023-02-09T04:18:29.706Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Node.js and Computer Vision: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-computer-vision-a-hands-on-guide)
{.links-list}


# Node.js y Computer Vision: una guía práctica

En el mundo del desarrollo web, Node.js es un popular entorno de tiempo de ejecución de JavaScript del lado del servidor. Es utilizado por grandes empresas como Netflix, Walmart y eBay. Y no es sólo para el desarrollo web. Node.js también es popular para crear aplicaciones de escritorio y para el desarrollo de sistemas integrados.

Un área en la que Node.js está experimentando una gran adopción es la visión artificial. En este artículo, veremos qué es la visión por computadora y cómo puede usar Node.js para crear soluciones prácticas.

## ¿Qué es la visión artificial?

La visión por computadora es un campo de la inteligencia artificial que se ocupa de cómo se pueden hacer las computadoras para comprender las imágenes digitales. Esto implica tareas como reconocimiento de imágenes, detección de objetos y clasificación de imágenes.

La visión artificial es un campo amplio con muchas aplicaciones diferentes. Se utiliza en automóviles autónomos, para el reconocimiento facial y en el análisis de imágenes médicas.

## Node.js y visión artificial

Hay algunas formas diferentes de usar Node.js para la visión por computadora. Los dos más populares son la biblioteca de código abierto OpenCV y la biblioteca comercial Sightengine.

OpenCV es la biblioteca de visión por computadora más popular y tiene enlaces para muchos lenguajes de programación, incluido Node.js. Se utiliza en una amplia gama de aplicaciones, incluidas la seguridad, la robótica y la realidad aumentada.

Sightengine es una biblioteca comercial de visión artificial centrada en el reconocimiento de imágenes. Ofrece una prueba gratuita y tiene una biblioteca de cliente Node.js.

En este artículo, nos centraremos en OpenCV, ya que es la más popular de las dos bibliotecas.

## Primeros pasos con OpenCV

OpenCV es una biblioteca de código abierto, por lo que se puede instalar de forma gratuita. La forma más fácil de instalarlo es usando el administrador de paquetes de Node.js, npm.

```
npm install opencv
```

Esto instalará la última versión de OpenCV.

Una vez que se instala OpenCV, puede solicitarlo en su código Node.js.

```javascript
const cv = require('opencv');
```

## Lectura de una imagen

El primer paso en cualquier proyecto de visión artificial es leer una imagen. OpenCV lo hace fácil con la función `readImage`.

```javascript
cv.readImage('image.jpg', (err, img) => {
  if (err) {
    console.error(err);
  } else {
    // Do something with the image
  }
});
```

Esto leerá la imagen `image.jpg` y la proporcionará como un objeto `img`.

## Convertir una imagen

OpenCV admite una amplia gama de formatos de imagen, incluidos JPEG, PNG y TIFF. Sin embargo, no todos los formatos son compatibles con todas las funciones. Por ejemplo, la función `umbral` solo admite imágenes en escala de grises.

Para convertir una imagen a escala de grises, puede usar la función `cvtColor`.

```javascript
cv.cvtColor(img, cv.COLOR_BGR2GRAY, (err, grayImg) => {
  if (err) {
    console.error(err);
  } else {
    // Do something with the grayscale image
  }
});
```

Esto convertirá la imagen `img` a escala de grises y la proporcionará como `grayImg`.

## Umbral de una imagen

La umbralización es una operación común en la visión artificial. Se utiliza para convertir una imagen en una imagen binaria, donde cada píxel es blanco o negro.

OpenCV proporciona una función de "umbral" que toma una imagen y un valor de umbral. Los píxeles con una intensidad superior al umbral se convierten en blanco y los píxeles con una intensidad inferior al umbral se convierten en negro.

```javascript
cv.threshold(grayImg, 127, 255, cv.THRESH_BINARY, (err, binImg) => {
  if (err) {
    console.error(err);
  } else {
    // Do something with the binary image
  }
});
```

Esto establecerá el umbral de la imagen `grayImg` con un valor de umbral de 127. La imagen resultante se proporcionará como `binImg`.

## Invertir una imagen

En algunos casos, puede ser útil invertir una imagen. Esto se puede hacer con la función `bitwise_not`.

```javascript
cv.bitwise_not(binImg, (err, invImg) => {
  if (err) {
    console.error(err);
  } else {
    // Do something with the inverted image
  }
});
```

Esto invertirá la imagen `binImg` y proporcionará el resultado como `invImg`.

## Guardar una imagen

Una vez que haya procesado una imagen, probablemente querrá guardar los resultados. OpenCV proporciona la función `saveImage` para esto.

```javascript
cv.saveImage('output.jpg', invImg);
```

Esto guardará la imagen `invImg` como `output.jpg`.

## Conclusión

En este artículo, analizamos qué es la visión por computadora y cómo puede usar Node.js para crear soluciones prácticas. Hemos cubierto cómo instalar OpenCV, cómo leer y convertir imágenes, cómo umbralizar imágenes y cómo guardar imágenes.

Esta es solo la punta del iceberg cuando se trata de visión artificial. Si está interesado en obtener más información, le recomiendo que consulte los recursos a continuación.

## Recursos

- [Documentación OpenCV](https://docs.opencv.org/4.1.0/)
- [Documentación de Sightengine](https://sightengine.com/docs/reference/nodejs)
- [Visión por computadora en Wikipedia](https://en.wikipedia.org/wiki/Computer_vision)