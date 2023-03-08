---
title: [Lenguaje C] 036: tabla hash
description: 
published: true
date: 2023-02-13T16:32:48.975Z
tags: 
editor: markdown
dateCreated: 2023-02-13T16:32:41.729Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 036: Hash Table***English** document is available*](/en/Knowledge-base/Algorithm/c-language-036-hash-table)
{.links-list}


# Tabla de picadillo

Una tabla hash es una estructura de datos que almacena datos en un formato de matriz asociativa, donde las claves se utilizan para acceder a los valores de los datos. Una tabla hash utiliza una función hash para generar un valor hash para cada clave, que se utiliza como índice para almacenar el valor de los datos en la tabla.

Las tablas hash se utilizan para implementar matrices asociativas, que son estructuras de datos que almacenan datos en pares clave-valor. En una matriz asociativa, la clave se usa para acceder al valor de los datos, al igual que se usa un nombre de variable para acceder a un valor de variable.

Las tablas hash se utilizan en muchas aplicaciones, como la indexación de bases de datos, cachés y estructuras de datos basadas en hash.

## Descripción general

Una tabla hash es una estructura de datos que almacena datos en un formato de matriz asociativa, donde las claves se utilizan para acceder a los valores de los datos.

Una tabla hash utiliza una función hash para generar un valor hash para cada clave, que se utiliza como índice para almacenar el valor de los datos en la tabla.

Las tablas hash se utilizan para implementar matrices asociativas, que son estructuras de datos que almacenan datos en pares clave-valor. En una matriz asociativa, la clave se usa para acceder al valor de los datos, al igual que se usa un nombre de variable para acceder a un valor de variable.

Las tablas hash se utilizan en muchas aplicaciones, como la indexación de bases de datos, cachés y estructuras de datos basadas en hash.

## Hashing

Una función hash es una función que toma un valor de datos y genera un valor hash, que es un valor numérico utilizado para indexar el valor de los datos en una tabla hash.

Una buena función hash debe tener las siguientes propiedades:

- La función hash debe ser determinista, lo que significa que dado el mismo valor de datos, la función hash siempre debe generar el mismo valor hash.

- La función hash debe distribuirse uniformemente, lo que significa que debe generar valores hash distribuidos uniformemente en el rango de valores posibles.

- La función hash debe ser resistente a colisiones, lo que significa que debería ser difícil encontrar dos valores de datos que se asignen al mismo valor hash.

Hay muchos algoritmos hash diferentes, pero algunos de los más comunes son:

- Sondeo lineal: este algoritmo sondea la tabla hash en busca de la siguiente ranura disponible para almacenar el valor de los datos.

- Sondeo cuadrático: este algoritmo sondea la tabla hash mediante una función cuadrática para encontrar el siguiente espacio disponible para almacenar el valor de los datos.

- Hashing doble: este algoritmo utiliza dos funciones hash para sondear la tabla hash en busca de la siguiente ranura disponible para almacenar el valor de los datos.

## Operaciones de tablas hash

Las tablas hash admiten las siguientes operaciones:

- Insertar: esta operación inserta un valor de datos en la tabla hash.

- Eliminar: esta operación elimina un valor de datos de la tabla hash.

- Buscar: Esta operación busca un valor de datos en la tabla hash.

- Actualizar: esta operación actualiza un valor de datos en la tabla hash.

## Implementación de tablas hash

Las tablas hash se pueden implementar mediante matrices o listas enlazadas.

Las tablas hash basadas en matrices almacenan los valores de datos en una matriz y las claves se utilizan para indexar en la matriz.

Las tablas hash basadas en listas vinculadas almacenan los valores de datos en una lista vinculada y las claves se utilizan para indexar en la lista vinculada.

## Aplicaciones de tablas hash

Las tablas hash se utilizan en muchas aplicaciones, como la indexación de bases de datos, cachés y estructuras de datos basadas en hash.

La indexación de bases de datos es un proceso de almacenamiento de datos en una base de datos de tal manera que se puedan recuperar rápidamente. Las tablas hash a menudo se usan para indexar datos en bases de datos.

Los cachés son estructuras de datos que almacenan datos en la memoria para que se pueda acceder a ellos rápidamente. Las tablas hash a menudo se usan para implementar cachés.

Las estructuras de datos basadas en hash son estructuras de datos que utilizan funciones hash para almacenar datos. Algunos ejemplos de estructuras de datos basadas en hash son mapas hash y conjuntos hash.