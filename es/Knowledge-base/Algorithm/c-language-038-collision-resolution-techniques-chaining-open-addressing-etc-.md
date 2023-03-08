---
title: [Lenguaje C] 038: Técnicas de resolución de colisiones (encadenamiento, direccionamiento abierto, etc.)
description: 
published: true
date: 2023-02-13T18:32:31.697Z
tags: 
editor: markdown
dateCreated: 2023-02-13T18:32:30.159Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 038: Collision Resolution Techniques (Chaining, Open Addressing, etc.)***English** document is available*](/en/Knowledge-base/Algorithm/c-language-038-collision-resolution-techniques-chaining-open-addressing-etc-)
{.links-list}


# Técnicas de Resolución de Colisiones

## Introducción

En informática, una colisión es cuando dos o más elementos chocan en una tabla hash. Una tabla hash es una estructura de datos que se utiliza para almacenar claves y valores. Cuando se aplica un hash a una clave, la función hash devolverá un índice que se utiliza para almacenar el par clave-valor en la tabla hash. Sin embargo, si dos claves se cifran en el mismo índice, se produce una colisión.

Existen tres técnicas principales de resolución de colisiones: encadenamiento, direccionamiento abierto y doble hashing. En este post, discutiremos cada una de estas técnicas en detalle.

## Encadenamiento

El encadenamiento es una técnica de resolución de colisiones que utiliza listas enlazadas para almacenar pares clave-valor que han colisionado. Cuando se aplica hash a una clave, la función hash devolverá un índice. Si el índice está vacío, el par clave-valor simplemente se almacena en ese índice. Sin embargo, si el índice ya está ocupado, el par clave-valor se agrega a la lista vinculada en ese índice.

La ventaja del encadenamiento es que es fácil de implementar. La desventaja del encadenamiento es que puede conducir a un rendimiento deficiente si la tabla hash se llena demasiado. Esto se debe a que las listas vinculadas serán muy largas y llevará más tiempo encontrar un par clave-valor específico.

Aquí hay un ejemplo de encadenamiento en pseudocódigo:

```
function insert(key, value)
  index = hash(key)

  if table[index] is empty
    table[index] = key-value pair
  else
    add key-value pair to the linked list at table[index]
```

## Direccionamiento abierto

El direccionamiento abierto es una técnica de resolución de colisiones que utiliza el sondeo para encontrar un índice vacío para almacenar un par clave-valor. Cuando se aplica hash a una clave, la función hash devolverá un índice. Si el índice está vacío, el par clave-valor simplemente se almacena en ese índice. Sin embargo, si el índice ya está ocupado, el par clave-valor se almacena en el siguiente índice vacío.

La ventaja del direccionamiento abierto es que puede ser más rápido que el encadenamiento si la tabla hash no está demasiado llena. La desventaja del direccionamiento abierto es que puede provocar un rendimiento deficiente si la tabla hash se llena demasiado. Esto se debe a que el sondeo puede volverse muy lento a medida que la tabla hash se llena.

Aquí hay un ejemplo de direccionamiento abierto en pseudocódigo:

```
function insert(key, value)
  index = hash(key)

  while table[index] is occupied
    index = (index + 1) mod table.size

  table[index] = key-value pair
```

## Hashing doble

El hash doble es una técnica de resolución de colisiones que utiliza dos funciones hash para encontrar un índice vacío para almacenar un par clave-valor. Cuando se aplica un hash a una clave, la primera función hash devolverá un índice. Si el índice está vacío, el par clave-valor simplemente se almacena en ese índice. Sin embargo, si el índice ya está ocupado, el par clave-valor se vuelve a codificar con la segunda función hash. La segunda función hash devolverá otro índice y el par clave-valor se almacena en ese índice.

La ventaja del hash doble es que puede ser más rápido que el direccionamiento abierto si la tabla hash no está demasiado llena. La desventaja del hash doble es que puede provocar un rendimiento deficiente si la tabla hash se llena demasiado. Esto se debe a que la segunda función hash puede devolver el mismo índice que la primera función hash, lo que puede generar un bucle infinito.

Aquí hay un ejemplo de hash doble en pseudocódigo:

```
function insert(key, value)
  index = hash(key)
  index2 = hash2(key)

  while table[index] is occupied
    index = (index + index2) mod table.size

  table[index] = key-value pair
```

## Conclusión

En esta publicación, hemos discutido tres técnicas de resolución de colisiones: encadenamiento, direccionamiento abierto y doble hashing. Cada una de estas técnicas tiene sus propias ventajas y desventajas. Elija la técnica adecuada para su aplicación.