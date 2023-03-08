---
title: [JavaScript] 038: Técnicas de resolución de colisiones (encadenamiento, direccionamiento abierto, etc.)
description: 
published: true
date: 2023-02-10T16:32:32.347Z
tags: 
editor: markdown
dateCreated: 2023-02-10T16:32:30.723Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 038: Collision Resolution Techniques (Chaining, Open Addressing, etc.)***English** document is available*](/en/Knowledge-base/Algorithm/javascript-038-collision-resolution-techniques-chaining-open-addressing-etc-)
{.links-list}


# JavaScript 038: Técnicas de resolución de colisiones (encadenamiento, direccionamiento abierto, etc.)

En esta publicación, discutiremos las técnicas de resolución de colisiones en tablas hash. Cuando dos claves se asignan al mismo valor hash, se produce una colisión. Hay algunas formas de resolver las colisiones, que veremos en esta publicación.

## Encadenamiento

El encadenamiento es una técnica de resolución de colisiones en la que cada ranura de la tabla hash es una lista enlazada. Cuando ocurre una colisión, la clave se agrega a la lista vinculada en esa ranura.

![Encadenamiento](https://upload.wikimedia.org/wikipedia/commons/6/6d/Hash_table_3_1_1_0_1_0_0_LL.svg)

Para buscar una clave, hacemos hash de la clave y vamos a la ranura correspondiente. Luego, buscamos la clave en la lista vinculada en esa ranura. La complejidad de tiempo tanto para la inserción como para la búsqueda es O(n), donde n es el número de claves en la tabla hash.

Una ventaja del encadenamiento es que es fácil de implementar. Otra ventaja es que la tabla hash se puede cambiar de tamaño fácilmente. Para cambiar el tamaño de la tabla hash, simplemente creamos una nueva tabla hash e insertamos todas las claves de la tabla hash anterior en la nueva tabla hash.

## Direccionamiento abierto

El direccionamiento abierto es una técnica de resolución de colisiones en la que las claves se almacenan en la propia tabla hash. Hay algunos métodos diferentes para el direccionamiento abierto, que repasaremos.

### Sondeo lineal

El sondeo lineal es un método de direccionamiento abierto en el que buscamos el siguiente espacio vacío en la tabla hash hasta que encontramos un espacio vacío. Si llegamos al final de la tabla hash, damos la vuelta y continuamos desde el principio de la tabla hash.

![Sonda lineal](https://upload.wikimedia.org/wikipedia/commons/d/d5/Hash_table_4_1_1_1_1_1_1_LP.svg)

Para buscar una clave, hacemos hash de la clave y vamos a la ranura correspondiente. Si esa ranura está vacía, sabemos que la clave no está en la tabla hash. Si la ranura no está vacía, comparamos la clave en esa ranura con la clave que estamos buscando. Si no son iguales, seguimos buscando la siguiente ranura. La complejidad de tiempo para la inserción es O(1), pero la complejidad de tiempo para la búsqueda es O(n), donde n es el número de claves en la tabla hash.

Una ventaja del sondeo lineal es que es fácil de implementar. Otra ventaja es que las claves se distribuyen uniformemente en la tabla hash, por lo que no hay ranuras vacías.

### Sondeo cuadrático

El sondeo cuadrático es un método de direccionamiento abierto en el que buscamos la siguiente ranura vacía agregando 1, 4, 9, 16, 25, etc. al valor hash.

![Sondeo cuadrático](https://upload.wikimedia.org/wikipedia/commons/5/5f/Hash_table_5_1_1_1_1_1_1_QP.svg)

Para buscar una clave, hacemos hash de la clave y vamos a la ranura correspondiente. Si esa ranura está vacía, sabemos que la clave no está en la tabla hash. Si la ranura no está vacía, comparamos la clave en esa ranura con la clave que estamos buscando. Si no son iguales, seguimos buscando la siguiente ranura. La complejidad de tiempo para la inserción es O(1), pero la complejidad de tiempo para la búsqueda es O(n), donde n es el número de claves en la tabla hash.

Una ventaja del sondeo cuadrático es que es fácil de implementar. Otra ventaja es que las claves se distribuyen uniformemente en la tabla hash, por lo que no hay ranuras vacías.

### Hashing doble

El hash doble es un método de direccionamiento abierto en el que usamos dos funciones hash para calcular la siguiente ranura.

![Hashing doble](https://upload.wikimedia.org/wikipedia/commons/4/4a/Hash_table_5_1_1_1_1_1_1_DH.svg)

Para buscar una clave, hacemos hash de la clave y vamos a la ranura correspondiente. Si esa ranura está vacía, sabemos que la clave no está en la tabla hash. Si la ranura no está vacía, comparamos la clave en esa ranura con la clave que estamos buscando. Si no son iguales, seguimos buscando la siguiente ranura. La complejidad de tiempo para la inserción es O(1), pero la complejidad de tiempo para la búsqueda es O(n), donde n es el número de claves en la tabla hash.

Una ventaja del hash doble es que es fácil de implementar. Otra ventaja es que las claves se distribuyen uniformemente en la tabla hash, por lo que no hay ranuras vacías.

## Conclusión

En esta publicación, discutimos las técnicas de resolución de colisiones en tablas hash. Repasamos el encadenamiento, el sondeo lineal, el sondeo cuadrático y el hash doble. El encadenamiento es una técnica en la que cada ranura de la tabla hash es una lista enlazada. El direccionamiento abierto es una técnica en la que las claves se almacenan en la propia tabla hash. El sondeo lineal, el sondeo cuadrático y el hash doble son todos métodos de direccionamiento abierto.