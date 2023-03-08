---
title: 058: Prueba de las aplicaciones TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T20:36:35.197Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:36:33.576Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [058: Testing TensorFlow.js and Node.js Applications***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/058-testing-tensorflow-js-and-node-js-applications)
{.links-list}


# 058: Prueba de aplicaciones TensorFlow.js y Node.js

## Introducción

En esta publicación, veremos cómo probar las aplicaciones TensorFlow.js y Node.js. Cubriremos los diferentes tipos de pruebas, cómo configurar un entorno de prueba y cómo ejecutar las pruebas.

## Tipos de Pruebas

Hay dos tipos principales de pruebas: pruebas unitarias y pruebas de extremo a extremo.

Las pruebas unitarias se utilizan para probar piezas individuales de código, como una función o una clase. Por lo general, los escriben los desarrolladores que escribieron el código.

Las pruebas de extremo a extremo se utilizan para probar toda la aplicación, de principio a fin. Por lo general, los escribe un equipo separado de evaluadores.

## Configuración de un entorno de prueba

Antes de que pueda comenzar a escribir pruebas, debe configurar un entorno de prueba.

Hay muchas maneras diferentes de hacer esto, pero cubriremos el método más común: usar un marco de prueba.

Un marco de prueba es una pieza de software que proporciona un conjunto de herramientas para escribir y ejecutar pruebas. El marco de prueba más popular para JavaScript es Jest.

Para usar Jest, primero debe instalarlo. Puede hacer esto usando la línea de comando o un administrador de paquetes como npm:

```
npm install --save-dev jest
```

Una vez que Jest está instalado, debe crear un archivo de configuración. Este archivo le dice a Jest cómo ejecutar sus pruebas.

La forma más sencilla de hacer esto es crear un archivo llamado jest.config.js en la raíz de su proyecto:

```js
module.exports = {
  // your config here
};
```

También puede usar un archivo JSON o un archivo XML.

Una vez que tenga un archivo de configuración, debe decirle a Jest dónde se encuentran sus pruebas. Puede hacer esto configurando la propiedad "testMatch":

```js
module.exports = {
  testMatch: ['**/__tests__/**/*.js?(x)']
};
```

Esto le dice a Jest que busque todos los archivos en el directorio __tests__ que terminen en .js o .jsx.

## Pruebas de escritura

Ahora que tiene configurado un entorno de prueba, puede comenzar a escribir pruebas.

Las pruebas están escritas en JavaScript. Por lo general, se colocan en el directorio __tests__, pero puede colocarlos en cualquier lugar que desee.

Una prueba se compone de dos partes: un "caso de prueba" y un "resultado esperado".

Un caso de prueba es una pieza de código que ejercita el código bajo prueba. Por ejemplo, si está probando una función que suma dos números, su caso de prueba podría verse así:

```js
// test case
const result = add(1, 2);

// expected outcome
expect(result).toBe(3);
```

El "resultado esperado" es lo que espera que haga el código. En este caso, esperamos que el resultado sea 3.

Si el código bajo prueba no produce el resultado esperado, la prueba fallará.

## Ejecución de pruebas

Una vez que haya escrito sus pruebas, puede ejecutarlas usando la línea de comando o un administrador de paquetes como npm:

```
npm test
```

Esto ejecutará todas las pruebas en su proyecto.

También puede ejecutar una prueba específica o un grupo de pruebas pasando el nombre de la prueba o el grupo:

```
npm test my-test
```

```
npm test my-test-group
```

## Conclusión

En esta publicación, cubrimos cómo probar las aplicaciones TensorFlow.js y Node.js. Cubrimos los diferentes tipos de pruebas, cómo configurar un entorno de prueba y cómo escribir y ejecutar pruebas.