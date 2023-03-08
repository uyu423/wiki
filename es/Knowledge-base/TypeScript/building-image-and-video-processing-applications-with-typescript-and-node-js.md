---
title: Creación de aplicaciones de procesamiento de imágenes y videos con TypeScript y Node.js
description: 
published: true
date: 2023-02-08T20:17:42.107Z
tags: 
editor: markdown
dateCreated: 2023-02-08T20:17:40.461Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building Image and Video Processing Applications with TypeScript and Node.js***English** document is available*](/en/Knowledge-base/TypeScript/building-image-and-video-processing-applications-with-typescript-and-node-js)
{.links-list}


# Creación de aplicaciones de procesamiento de imágenes y videos con TypeScript y Node.js

Los desarrolladores que buscan crear aplicaciones escalables de procesamiento de imágenes y videos tienen muchas opciones cuando se trata de lenguajes de programación. Una opción que a menudo se pasa por alto es TypeScript. TypeScript es un superconjunto escrito de JavaScript que se compila en JavaScript simple. Es un lenguaje que es fácil de aprender para los principiantes y también tiene funciones avanzadas que los desarrolladores experimentados pueden aprovechar.

Node.js es un tiempo de ejecución de JavaScript basado en el motor de JavaScript V8 de Chrome. Se utiliza para desarrollar aplicaciones del lado del servidor. Las aplicaciones de Node.js están escritas en JavaScript y se pueden ejecutar en una variedad de plataformas, incluidas Windows, macOS y Linux.

En este artículo, mostraremos cómo usar TypeScript y Node.js para crear una aplicación de procesamiento de imágenes. Usaremos la biblioteca TypeScript, gm, que es un contenedor de la biblioteca GraphicsMagick. GraphicsMagick es un conjunto de herramientas de procesamiento de imágenes multiplataforma que se puede utilizar para crear, editar y convertir imágenes.

La biblioteca gm proporciona una API simple para realizar tareas comunes de procesamiento de imágenes, como cambiar el tamaño, recortar y convertir imágenes. Se puede utilizar para crear aplicaciones web y de línea de comandos. En este artículo, crearemos una aplicación de línea de comandos que cambiará el tamaño de una imagen.

## Instalación de TypeScript y Node.js

Antes de que podamos comenzar a escribir nuestra aplicación, debemos instalar TypeScript y Node.js. TypeScript se puede instalar usando npm, el administrador de paquetes de Node.js. Para instalar TypeScript, abra una terminal y ejecute el siguiente comando:

```
npm install -g typescript
```

Esto instalará el compilador de TypeScript, tsc, y el servidor de lenguaje de TypeScript, tsserver. El compilador TypeScript se utiliza para compilar código TypeScript en código JavaScript. El servidor de lenguaje TypeScript proporciona servicios de lenguaje, como finalización de código y verificación de tipos, para código TypeScript.

Node.js se puede descargar desde el sitio web de Node.js. Una vez que se haya instalado Node.js, la interfaz de línea de comandos de npm estará disponible.

## Creación de un proyecto TypeScript

Ahora que tenemos TypeScript y Node.js instalados, podemos crear un proyecto de TypeScript. Para hacer esto, usaremos el comando npm init. Este comando creará un archivo package.json, que se usa para administrar las dependencias de un proyecto de Node.js.

Para crear un proyecto de TypeScript, abra una terminal y navegue hasta el directorio donde desea crear el proyecto. Luego, ejecuta el siguiente comando:

```
npm init
```

Esto le pedirá una serie de preguntas, como el nombre y la versión del proyecto. Para nuestro proyecto, estableceremos el nombre en "aplicación de procesamiento de imágenes" y la versión en "1.0.0".

Una vez que se ha creado el archivo package.json, podemos instalar las dependencias para nuestro proyecto. Para nuestro proyecto, necesitaremos instalar las definiciones gm TypeScript y la biblioteca gm. Para hacer esto, ejecute el siguiente comando:

```
npm install --save @types/gm gm
```

Esto instalará las definiciones gm TypeScript y la biblioteca gm en el directorio node_modules. Las definiciones gm TypeScript proporcionan enlaces TypeScript para la biblioteca gm.

## Cambiar el tamaño de una imagen

Ahora que tenemos nuestro proyecto configurado, podemos comenzar a escribir nuestra aplicación. Lo primero que debemos hacer es importar la biblioteca gm. Podemos hacer esto agregando la siguiente línea en la parte superior de nuestro archivo main.ts:

```typescript
import * as gm from "gm";
```

Esto importará el espacio de nombres gm a nuestro archivo. Ahora podemos usar el espacio de nombres gm para acceder a la funcionalidad de la biblioteca gm.

Lo siguiente que debemos hacer es abrir nuestra imagen. Podemos hacer esto usando la función gm.open(). Esta función toma la ruta a la imagen como primer argumento y una función de devolución de llamada como segundo argumento. La función de devolución de llamada se llama con un objeto de error y un objeto gm. El objeto gm se puede utilizar para realizar operaciones en la imagen.

Podemos abrir nuestra imagen y pasar el objeto gm a una función de cambio de tamaño () de la siguiente manera:

```typescript
gm.open("input.jpg", (err, image) => {
  if (err) {
    console.log(err);
  } else {
    resize(image);
  }
});
```

La función resize() tomará el objeto gm y cambiará el tamaño de la imagen. Podemos definir la función resize() de la siguiente manera:

```typescript
function resize(image: gm.Image): void {
  image
    .resize(100, 100)
    .write("output.jpg", (err) => {
      if (err) {
        console.log(err);
      }
    });
}
```

Esta función cambiará el tamaño de la imagen a 100x100 píxeles y escribirá la salida en el archivo output.jpg.

Para ejecutar nuestra aplicación, podemos usar el compilador de TypeScript, tsc. Podemos compilar nuestro código ejecutando el siguiente comando:

```
tsc main.ts
```

Esto generará un archivo main.js en el directorio actual. Podemos ejecutar nuestra aplicación ejecutando el siguiente comando:

```
node main.js
```

Esto cambiará el tamaño de la imagen input.jpg y guardará la salida en el archivo output.jpg.

## Conclusión

En este artículo, mostramos cómo usar TypeScript y Node.js para crear una aplicación de procesamiento de imágenes. Hemos visto cómo usar la biblioteca gm para cambiar el tamaño de una imagen. Esta aplicación se puede ampliar fácilmente para realizar otras tareas de procesamiento de imágenes, como recortar y convertir imágenes.