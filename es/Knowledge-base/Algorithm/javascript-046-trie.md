---
title: [JavaScript] 046: Trio
description: 
published: true
date: 2023-02-11T00:33:08.837Z
tags: 
editor: markdown
dateCreated: 2023-02-11T00:33:07.201Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 046: Trie***English** document is available*](/en/Knowledge-base/Algorithm/javascript-046-trie)
{.links-list}


# JavaScript 046: Prueba

Un trie, también llamado árbol digital o, a veces, árbol radix o árbol de prefijos (ya que se pueden buscar por prefijos), es una estructura de datos de árbol ordenada que se utiliza para almacenar un conjunto dinámico o una matriz asociativa donde las claves suelen ser cadenas. A diferencia de un árbol de búsqueda binario, ningún nodo del árbol almacena la clave asociada con ese nodo; en cambio, su posición en el árbol define la clave con la que está asociado. Todos los descendientes de un nodo tienen un prefijo común de la cadena asociada con ese nodo, y la raíz está asociada con la cadena vacía. Los valores no están necesariamente asociados con todos los nodos. Más bien, los valores tienden a asociarse con hojas y con algunos nodos internos que corresponden a claves de interés.

En aras de la simplicidad, supondremos en este artículo que las claves son caracteres únicos. Una suposición más realista sería que las teclas son cadenas de caracteres, pero incluso este caso más general se puede reducir al caso de un solo carácter si se considera que los caracteres de la cadena son una secuencia de pulsaciones de teclas.

## El árbol

Un trie puede verse como un árbol con una propiedad muy especial, a saber, que todos los caminos desde la raíz hasta las hojas tienen la misma longitud, y en cada nodo del camino, esta longitud es igual a la profundidad del nodo en el árbol. En otras palabras, un trie es un árbol en el que todas las hojas están al mismo nivel.

![Trie](https://i.imgur.com/fgNcuqP.png)

Cada nodo del árbol está etiquetado con una letra. El camino desde la raíz hasta una hoja corresponde a una palabra, y la etiqueta de cada nodo del camino es la letra que forma la palabra. Por ejemplo, en la figura anterior, el camino desde la raíz hasta el nodo marcado con la letra 'c' corresponde a la palabra "coche".

## El Algoritmo

La idea básica detrás del algoritmo trie es almacenar la cadena que se buscará en una estructura de datos trie y luego buscar en trie la cadena deseada.

El algoritmo de búsqueda comienza en la raíz del trie y en cada nodo comprueba si la etiqueta del nodo coincide con la siguiente letra de la cadena que se va a buscar. Si hay una coincidencia, se mueve al siguiente nodo en el trie (es decir, el hijo del nodo actual); si no hay coincidencia, se mueve al siguiente nodo en el árbol (es decir, el hermano del nodo actual). Si la búsqueda llega a un nodo hoja sin encontrar una coincidencia, entonces la cadena no está presente en el trie.

![Búsqueda Trie](https://i.imgur.com/bvU4r4e.png)

Por ejemplo, considere el trie que se muestra en la figura anterior y suponga que queremos buscar la cadena "car". El algoritmo de búsqueda comienza en el nodo raíz, que está etiquetado con la letra 'a'. Dado que esto coincide con la primera letra de la cadena, se mueve al nodo secundario, que está etiquetado con la letra 'c'. Dado que esto también coincide con la segunda letra de la cadena, se mueve al nodo secundario, que está etiquetado con la letra 'a'. Como esto no coincide con la tercera letra de la cadena, se mueve al siguiente nodo, que está etiquetado con la letra 'r'. Como esto tampoco coincide, se mueve al siguiente nodo, que está etiquetado con la letra 'b'. Como no hay más nodos, la búsqueda termina y concluimos que la cadena no está presente en el trie.

## Inserción

El algoritmo de inserción es similar al algoritmo de búsqueda, excepto que cuando llega a un nodo que no coincide con la siguiente letra de la cadena a insertar, crea un nuevo nodo con la etiqueta de la siguiente letra y lo inserta como hijo de el nodo actual.

![Insertar Trie](https://i.imgur.com/TGiukHr.png)

Por ejemplo, considere el trie que se muestra en la figura anterior y suponga que queremos insertar la cadena "gato". El algoritmo de inserción comienza en el nodo raíz, que está etiquetado con la letra 'a'. Dado que esto coincide con la primera letra de la cadena, se mueve al nodo secundario, que está etiquetado con la letra 'c'. Dado que esto también coincide con la segunda letra de la cadena, se mueve al nodo secundario, que está etiquetado con la letra 'a'. Dado que esto no coincide con la tercera letra de la cadena, crea un nuevo nodo con la etiqueta 't' y lo inserta como hijo del nodo actual.

## Eliminación

El algoritmo de eliminación es similar al algoritmo de inserción, excepto que cuando llega a un nodo que no coincide con la siguiente letra de la cadena a eliminar, elimina el nodo y todos sus descendientes.

![Trie-Delete](https://i.imgur.com/vALDKdR.png)

Por ejemplo, considere el trie que se muestra en la figura anterior y suponga que queremos eliminar la cadena "gato". El algoritmo de eliminación comienza en el nodo raíz, que está etiquetado con la letra 'a'. Dado que esto coincide con la primera letra de la cadena, se mueve al nodo secundario, que está etiquetado con la letra 'c'. Dado que esto también coincide con la segunda letra de la cadena, se mueve al nodo secundario, que está etiquetado con la letra 'a'. Como esto no coincide con la tercera letra de la cadena, elimina el nodo y todos sus descendientes.

## Implementación

La estructura de datos trie se puede implementar usando una lista enlazada o una matriz.

### Lista enlazada

Una lista enlazada es una estructura de datos que consta de un conjunto de nodos, cada uno de los cuales contiene una referencia al siguiente nodo de la lista.

![Lista Trie-Linked](https://i.imgur.com/rYUjg9O.png)

Cada nodo de la lista contiene dos campos:

- El primer campo es la etiqueta del nodo, que es un solo carácter.
- El segundo campo es una referencia al siguiente nodo de la lista.

El primer nodo de la lista se denomina nodo principal y el último nodo de la lista se denomina nodo final.

La implementación de la lista enlazada del trie es muy simple. Para buscar una cadena, comenzamos en el nodo principal y, para cada carácter de la cadena, seguimos la referencia al siguiente nodo hasta llegar al nodo final. Si la cadena no está presente en el trie, la búsqueda alcanzará el nodo final antes de llegar al final de la cadena.

Para insertar una cadena, comenzamos en el nodo principal y, para cada carácter de la cadena, seguimos la referencia al siguiente nodo hasta llegar al nodo final. Si la cadena no está presente en el trie, la inserción llegará al nodo final antes de llegar al final de la cadena, y en ese punto insertará un nuevo nodo con la etiqueta del siguiente carácter y actualizará la referencia del nodo de cola para apuntar al nuevo nodo.

Para eliminar una cadena, comenzamos en el nodo principal y, para cada carácter de la cadena, seguimos la referencia al siguiente nodo hasta llegar al nodo final. Si la cadena no está presente en el trie, la eliminación llegará al nodo final antes de llegar al final de la cadena. Si la cadena está presente en el trie, la eliminación llegará al final de la cadena y, en ese punto, eliminará el nodo y todos sus descendientes.

### Matriz

Una matriz es una estructura de datos que consta de un conjunto de elementos, cada uno de los cuales está identificado por un índice.

![Arreglo Trie](https://i.imgur.com/kzKVLCc.png)

En la implementación de matriz del trie, cada nodo en el trie está representado por una matriz de tamaño 26, donde cada elemento de la matriz es una referencia al siguiente nodo en el trie. La matriz está indexada por los caracteres del alfabeto, de modo que el índice del carácter 'a' es 0, el índice del carácter 'b' es 1, y así sucesivamente.

Para buscar una cadena, comenzamos en el nodo raíz y, para cada carácter de la cadena, seguimos la referencia al siguiente nodo. Si la cadena no está presente en el trie, la búsqueda alcanzará un nodo nulo antes de llegar al final de la cadena.

Para insertar una cadena, comenzamos en el nodo raíz y, para cada carácter de la cadena, seguimos la referencia al siguiente nodo. Si la cadena no está presente en el trie, la inserción alcanzará un nodo nulo antes de llegar al final de la cadena, y en ese punto insertará un nuevo nodo y actualizará la referencia del nodo.

Para eliminar una cadena, comenzamos en el nodo raíz y, para cada carácter de la cadena, seguimos la referencia al siguiente nodo. Si la cadena no está presente en el trie, la eliminación alcanzará un nodo nulo antes de llegar al final de la cadena. Si la cadena está presente en el trie, la eliminación llegará al final de la cadena y, en ese punto, eliminará el nodo y todos sus descendientes.

## Aplicaciones

La estructura de datos trie se usa en muchas aplicaciones, como correctores ortográficos, juegos de palabras y compresión de datos.

La aplicación del corrector ortográfico usa un trie para almacenar un diccionario de palabras, y el algoritmo de búsqueda se usa para verificar si una palabra dada está en el diccionario.

La aplicación del juego de palabras usa un trie para almacenar las palabras en el juego, y el algoritmo de búsqueda se usa para encontrar todas las palabras que se pueden formar a partir de un conjunto de letras determinado.

La aplicación de compresión de datos usa un trie para almacenar un diccionario de palabras, y el algoritmo de búsqueda se usa para encontrar la palabra más larga en el diccionario que sea un prefijo de una cadena determinada. A continuación, se utiliza la longitud de la palabra más larga para codificar la cadena.

## Ejercicios

1. Implemente la estructura de datos trie usando una lista enlazada.

2. Implemente la estructura de datos trie utilizando una matriz.

3. Use la estructura de datos trie para almacenar un diccionario de palabras e implemente una aplicación de corrector ortográfico que use el algoritmo de búsqueda para verificar si una palabra dada está en el diccionario.

4. Use la estructura de datos trie para almacenar las palabras en un juego de palabras e implemente el algoritmo de búsqueda para encontrar todas las palabras que se pueden formar a partir de un conjunto dado de letras.

5. Use la estructura de datos trie para almacenar un diccionario de palabras e implemente el algoritmo de búsqueda para encontrar la palabra más larga en el diccionario que sea un prefijo de una cadena determinada.