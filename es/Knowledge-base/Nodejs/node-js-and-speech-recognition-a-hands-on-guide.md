---
title: Node.js y el reconocimiento de voz: una guía práctica
description: 
published: true
date: 2023-02-02T06:36:44.637Z
tags: 
editor: markdown
dateCreated: 2023-02-02T06:36:43.018Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Node.js and Speech Recognition: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-speech-recognition-a-hands-on-guide)
{.links-list}


# Node.js y reconocimiento de voz: una guía práctica

### Introducción

En este artículo, exploraremos cómo usar Node.js para el reconocimiento de voz. Veremos cómo configurar un proyecto básico de Node.js, cómo usar la popular biblioteca `recognize-speech` para reconocer el habla y cómo usar Google Cloud Speech-to-Text para reconocer el habla.

También veremos cómo usar estas herramientas para crear una aplicación de reconocimiento de voz simple que se puede usar para controlar una computadora.

### Configuración de un proyecto Node.js

Antes de que podamos comenzar a usar el reconocimiento de voz, debemos configurar un proyecto de Node.js. Si nunca ha usado Node.js antes, no se preocupe, es muy fácil comenzar.

Primero, necesitamos instalar Node.js. Puede hacerlo yendo al sitio web de Node.js y descargando el instalador para su sistema operativo.

Una vez instalado Node.js, podemos crear un nuevo proyecto. Cree un nuevo directorio para su proyecto y luego inicialice el proyecto con npm:

```
$ mkdir my-project
$ cd my-project
$ npm init
```

Esto creará un archivo `package.json` en su proyecto. Este archivo contiene metadatos sobre su proyecto, incluidas las dependencias que su proyecto necesita.

A continuación, necesitamos instalar la biblioteca `recognize-speech`. Esto lo podemos hacer con el siguiente comando:

```
$ npm install --save recognize-speech
```

Esto instalará la biblioteca `recognize-speech` y la agregará a la sección `dependencies` de su archivo `package.json`.

### Reconocimiento del habla con la biblioteca `recognize-speech`

Ahora que tenemos un proyecto básico de Node.js configurado, podemos comenzar a usar la biblioteca `recognize-speech` para reconocer el habla.

La biblioteca `recognize-speech` proporciona una API simple para reconocer el habla. Para usarlo, primero necesitamos crear un objeto `recognizer`:

```javascript
var Recognizer = require('recognize-speech');

var recognizer = new Recognizer();
```

A continuación, debemos registrar un controlador de eventos para el evento `habla`:

```javascript
recognizer.on('speech', function(data) {
  // The data object contains the recognized text
  console.log(data.text);
});
```

Por último, tenemos que iniciar el proceso de reconocimiento. Podemos hacer esto llamando al método `recognize`:

```javascript
recognizer.recognize('speech.wav');
```

Esto iniciará el proceso de reconocimiento e imprimirá el texto reconocido en la consola.

### Uso de Google Cloud Speech-to-Text

Google Cloud Speech-to-Text es un servicio de reconocimiento de voz basado en la nube que se puede usar para reconocer el habla. Para usarlo, primero necesitamos crear un objeto `habla`:

```javascript
var Speech = require('@google-cloud/speech');

var speech = new Speech();
```

A continuación, debemos registrar un controlador de eventos para el evento `data`:

```javascript
speech.on('data', function(data) {
  // The data object contains the recognized text
  console.log(data.text);
});
```

Por último, tenemos que iniciar el proceso de reconocimiento. Podemos hacer esto llamando al método `recognize`:

```javascript
speech.recognize('speech.wav');
```

Esto iniciará el proceso de reconocimiento e imprimirá el texto reconocido en la consola.

### Creación de una aplicación de reconocimiento de voz

Ahora que hemos visto cómo usar Node.js para el reconocimiento de voz, construyamos una aplicación de reconocimiento de voz simple que se puede usar para controlar una computadora.

La aplicación utilizará la biblioteca `recognize-speech` para reconocer el habla y la biblioteca `osascript` para controlar la computadora.

Primero, necesitamos instalar la biblioteca `osascript`:

```
$ npm install --save osascript
```

A continuación, necesitamos solicitar la biblioteca `osascript` en nuestro código:

```javascript
var osascript = require('osascript');
```

Ahora, podemos escribir la función `recognize`:

```javascript
function recognize(speech, callback) {
  // ...
}
```

Esta función tomará una grabación de voz como entrada y llamará al método `recognize` de la biblioteca `recognize-speech`. Si el reconocimiento es exitoso, llamará a la función de devolución de llamada con el texto reconocido.

Finalmente, necesitamos escribir la función `principal`:

```javascript
function main() {
  // ...
}
```

Esta función se llamará cuando se inicie la aplicación. Creará un objeto `recognizer` y registrará un controlador de eventos para el evento `speech`.

Cuando se activa el evento `habla`, llamará a la función `reconocer` con la grabación de voz. Si el reconocimiento es exitoso, utilizará la biblioteca `osascript` para controlar la computadora.

Para ejecutar la aplicación, podemos usar el siguiente comando:

```
$ node app.js
```

### Conclusión

En este artículo, hemos visto cómo usar Node.js para el reconocimiento de voz. Hemos visto cómo configurar un proyecto básico de Node.js, cómo usar la biblioteca `recognize-speech` para reconocer el habla y cómo usar Google Cloud Speech-to-Text.

También hemos visto cómo usar estas herramientas para crear una aplicación de reconocimiento de voz simple que se puede usar para controlar una computadora.