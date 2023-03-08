---
title: Trabajar con datos binarios en TypeScript y Node.js
description: 
published: true
date: 2023-02-10T09:17:40.961Z
tags: 
editor: markdown
dateCreated: 2023-02-10T09:17:38.475Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Working with Binary Data in TypeScript and Node.js***English** document is available*](/en/Knowledge-base/TypeScript/working-with-binary-data-in-typescript-and-node-js)
{.links-list}


# Trabajar con datos binarios en TypeScript y Node.js

Los desarrolladores de TI a menudo necesitan trabajar con datos binarios. Esto puede deberse a que están trabajando con una API que devuelve datos binarios o porque necesitan leer o escribir datos binarios en un archivo. En TypeScript y Node.js, los desarrolladores tienen diferentes opciones para trabajar con datos binarios.

## La clase de búfer

Una forma de trabajar con datos binarios en Node.js es usar la clase `Buffer`. Esta clase está disponible globalmente, por lo que no es necesario importarla. La clase `Buffer` proporciona varios métodos para leer y escribir datos binarios.

Para crear un `Buffer` a partir de una cadena, los desarrolladores pueden usar el método `Buffer.from()`. Este método toma una cadena y una codificación como argumentos. El argumento de codificación es opcional y por defecto es `utf8`. El siguiente ejemplo crea un `Buffer` a partir de una cadena utilizando la codificación `utf8`:

    const buf = Buffer.from('hola mundo', 'utf8');

Los desarrolladores también pueden escribir datos binarios en un `Buffer` utilizando el método `Buffer.alloc()`. Este método toma un número como argumento, que es el tamaño del 'Búfer' en bytes. El siguiente ejemplo crea un 'Búfer' vacío con un tamaño de 10 bytes:

    const buf = Buffer.alloc(10);

Una vez que se ha creado un `Buffer`, los desarrolladores pueden escribir datos en él usando el método `Buffer.write()`. Este método toma una cadena, un desplazamiento y una codificación como argumentos. El desplazamiento es el índice en el `Buffer` donde se escribirá la cadena. El argumento de codificación es opcional y por defecto es `utf8`. El siguiente ejemplo escribe la cadena ` 'hello world'` en el `Buffer` creado en el ejemplo anterior, comenzando en el índice 0:

    buf.write('hola mundo', 0, 'utf8');

Para leer datos de un `Buffer`, los desarrolladores pueden usar el método `Buffer.toString()`. Este método toma una codificación y, opcionalmente, un índice inicial y final como argumentos. El siguiente ejemplo lee los datos del `Buffer` creado en los ejemplos anteriores y los genera como una cadena:

    consola.log(buf.toString('utf8')); // 'Hola Mundo'

## La clase Uint8Array

Otra forma de trabajar con datos binarios en TypeScript es usar la clase `Uint8Array`. Esta clase está disponible globalmente, por lo que no es necesario importarla. La clase `Uint8Array` proporciona varios métodos para leer y escribir datos binarios.

Para crear un `Uint8Array` a partir de una matriz de números, los desarrolladores pueden usar el método `Uint8Array.from()`. Este método toma una matriz de números como argumento. El siguiente ejemplo crea un `Uint8Array` a partir de una matriz de números:

    const matriz = Uint8Array.from([1, 2, 3, 4, 5]);

Para crear un `Uint8Array` a partir de un `Buffer`, los desarrolladores pueden usar el método `Uint8Array.from()`. Este método toma un `Buffer` como argumento. El siguiente ejemplo crea un `Uint8Array` a partir de un `Buffer`:

    const buf = Buffer.from([1, 2, 3, 4, 5]);
    const matriz = Uint8Array.from(buf);

Una vez que se ha creado un `Uint8Array`, los desarrolladores pueden escribir datos en él utilizando el método `Uint8Array.set()`. Este método toma una matriz de números y, opcionalmente, un índice de inicio como argumentos. El índice de inicio es el índice en `Uint8Array` donde se escribirá la matriz de números. El siguiente ejemplo escribe la matriz de números `[6, 7, 8, 9, 10]` en `Uint8Array` creado en el ejemplo anterior, comenzando en el índice 0:

    arr.set([6, 7, 8, 9, 10], 0);

Para leer datos de un `Uint8Array`, los desarrolladores pueden usar el método `Uint8Array.subarray()`. Este método toma un índice inicial y final como argumentos. El siguiente ejemplo lee los datos de `Uint8Array` creado en los ejemplos anteriores y los genera como una matriz:

    consola.log(arr.subarray(0, 5)); // [1, 2, 3, 4, 5]

## Conversión entre tipos de datos binarios

En algunos casos, los desarrolladores pueden necesitar convertir entre `Buffer` y `Uint8Array`. Esto se puede hacer usando los métodos `Buffer.from()` y `Uint8Array.from()`. El siguiente ejemplo crea un `Buffer` a partir de `Uint8Array`:

    const matriz = Uint8Array.from([1, 2, 3, 4, 5]);
    const buf = Buffer.from(arr);

El siguiente ejemplo crea un `Uint8Array` a partir de un `Buffer`:

    const buf = Buffer.from([1, 2, 3, 4, 5]);
    const matriz = Uint8Array.from(buf);

## Conclusión

Los desarrolladores tienen diferentes opciones para trabajar con datos binarios en TypeScript y Node.js. La clase `Buffer` proporciona varios métodos para trabajar con datos binarios, y la clase `Uint8Array` proporciona una forma alternativa de trabajar con datos binarios. En algunos casos, los desarrolladores pueden necesitar convertir entre `Buffer` y `Uint8Array`.