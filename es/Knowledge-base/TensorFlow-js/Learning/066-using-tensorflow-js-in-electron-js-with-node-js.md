---
title: 066: Usar TensorFlow.js en Electron.js con Node.js
description: 
published: true
date: 2023-02-02T21:23:20.958Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:23:19.325Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [066: Using TensorFlow.js in Electron.js with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/066-using-tensorflow-js-in-electron-js-with-node-js)
{.links-list}


# TensorFlow.js en Electron.js con Node.js

## Introducción

En esta publicación, exploraremos cómo usar TensorFlow.js en Electron.js con Node.js. Repasaremos los aspectos básicos del uso de TensorFlow.js y luego mostraremos cómo usarlo en Electron.js.

## ¿Qué es TensorFlow.js?

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. Se utiliza para una variedad de tareas, incluida la clasificación de imágenes, la detección de objetos y la clasificación de texto.

## Empezando

Para comenzar, deberá instalar TensorFlow.js. Puedes hacer esto con el siguiente comando:

```
npm install @tensorflow/tfjs
```

Una vez que TensorFlow.js esté instalado, puede importarlo a su código JavaScript con la siguiente línea:

```javascript
import * as tf from '@tensorflow/tfjs';
```

## Uso de TensorFlow.js en Electron.js

Ahora que tenemos instalado TensorFlow.js, echemos un vistazo a cómo usarlo en Electron.js.

Lo primero que debemos hacer es crear un nuevo proyecto Electron.js. Esto lo podemos hacer con el siguiente comando:

```
npm init electron-app my-app
```

Esto creará un nuevo directorio llamado "my-app" con la estructura básica de una aplicación Electron.js.

A continuación, debemos instalar TensorFlow.js en nuestro proyecto. Esto lo podemos hacer con el siguiente comando:

```
cd my-app
npm install @tensorflow/tfjs
```

Una vez instalado TensorFlow.js, podemos importarlo a nuestra aplicación Electron.js con la siguiente línea:

```javascript
import * as tf from '@tensorflow/tfjs';
```

Ahora que tenemos instalado TensorFlow.js, podemos comenzar a usarlo en nuestra aplicación.

## Conclusión

En esta publicación, exploramos cómo usar TensorFlow.js en Electron.js con Node.js. Hemos repasado los conceptos básicos del uso de TensorFlow.js y luego mostramos cómo usarlo en Electron.js.