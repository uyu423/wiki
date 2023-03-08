---
title: [Lenguaje C] 008: Lista vinculada
description: 
published: true
date: 2023-02-12T19:32:47.136Z
tags: 
editor: markdown
dateCreated: 2023-02-12T19:32:40.200Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 008: Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-008-linked-list)
{.links-list}


# C Language 008: Lista enlazada

Una lista enlazada es una estructura de datos lineal, en la que los elementos no se almacenan en ubicaciones de memoria contiguas. Los elementos de una lista enlazada se enlazan mediante punteros.

## ¿Qué es una lista enlazada?

Una lista enlazada es una estructura de datos que consta de un grupo de nodos que juntos representan una secuencia. Cada nodo contiene dos campos:

1. **Campo de datos**: contiene los datos reales.
2. **Campo de enlace**: contiene la dirección del siguiente nodo en la secuencia.

![Lista vinculada](https://i.imgur.com/eua0oE7.png)

El ejemplo anterior muestra una lista enlazada con cuatro nodos. El primer nodo se llama nodo **cabeza** y el último nodo se llama nodo **cola**. El nodo principal es el primer nodo de la secuencia y el nodo final es el último nodo de la secuencia.

Los nodos de una lista enlazada no se almacenan en ubicaciones de memoria contiguas. El campo de enlace de un nodo contiene la dirección del siguiente nodo en la secuencia. El puntero de cabeza apunta al primer nodo y el puntero de cola apunta al último nodo.

## Ventajas de las listas enlazadas

1. **Las listas enlazadas son estructuras de datos dinámicas.** Es decir, pueden crecer y reducirse durante la ejecución de un programa.
2. **Las operaciones de inserción y eliminación se pueden implementar fácilmente en listas vinculadas.**
3. **Las listas enlazadas se pueden implementar fácilmente de diferentes maneras.** Por ejemplo, se pueden implementar como **listas enlazadas individualmente** o **listas enlazadas doblemente**.
4. **Las listas enlazadas circulares** se pueden implementar fácilmente en listas enlazadas.

## Desventajas de las listas enlazadas

1. **El acceso aleatorio no es posible en listas enlazadas.** Necesitamos acceder a los nodos secuencialmente desde el principio.
2. **Se requiere espacio de memoria adicional para almacenar los punteros.**
3. **Las matrices tienen una mejor localidad de caché que puede hacerlas un poco más rápidas.**

## Implementación de Listas Enlazadas

Hay dos formas de implementar listas enlazadas:

1. **Listas enlazadas individualmente**: en este tipo de lista enlazada, cada nodo contiene un campo de datos y un campo de enlace, que contiene la dirección del siguiente nodo en la secuencia.
2. **Listas doblemente enlazadas**: En este tipo de lista enlazada, cada nodo contiene dos campos de enlace, que contienen las direcciones de los nodos anterior y siguiente en la secuencia.

![Lista de enlaces individuales](https://i.imgur.com/FwASDVv.png)
![Lista doblemente enlazada](https://i.imgur.com/KzZ4gcD.png)

## Operaciones en listas enlazadas

Las siguientes operaciones se pueden realizar en una lista enlazada:

1. **Inserción**: agrega un nuevo nodo a la lista.
2. **Eliminación**: elimina un nodo de la lista.
3. **Transversal**: Muestra los datos almacenados en los nodos de la lista.
4. **Buscar**: busca un elemento de datos determinado en la lista.
5. **Reverse**: Invierte el orden de los nodos en la lista.

## Inserción en Listas Enlazadas

Hay tres formas de insertar un nodo en una lista enlazada:

1. **Inserción al principio de la lista**: En este tipo de inserción, el nuevo nodo se inserta al principio de la lista.

![Inserción al principio de la lista](https://i.imgur.com/w4VDm7q.png)

2. **Inserción al final de la lista**: En este tipo de inserción, el nuevo nodo se inserta al final de la lista.

![Inserción al final de la lista](https://i.imgur.com/VkzMVqY.png)

3. **Inserción en medio de la lista**: En este tipo de inserción, el nuevo nodo se inserta en medio de la lista.

![Inserción en medio de la lista](https://i.imgur.com/U4VxK5D.png)

## Eliminación en listas enlazadas

Hay tres formas de eliminar un nodo en una lista enlazada:

1. **Eliminación al principio de la lista**: En este tipo de eliminación, el nodo a eliminar es el primer nodo de la lista.

![Eliminación al principio de la lista](https://i.imgur.com/FgxL0b4.png)

2. **Eliminación al final de la lista**: En este tipo de eliminación, el nodo a eliminar es el último nodo de la lista.

![Eliminación al final de la lista](https://i.imgur.com/w4VDm7q.png)

3. **Eliminación en medio de la lista**: En este tipo de eliminación, el nodo a eliminar se encuentra en la mitad de la lista.

![Borrado en medio de la lista](https://i.imgur.com/U4VxK5D.png)

## Recorrido en listas enlazadas

Hay dos formas de recorrer una lista enlazada:

1. **Recorrido iterativo**: En este tipo de recorrido, usamos un bucle para visitar cada nodo de la lista.

2. **Recorrido recursivo**: En este tipo de recorrido, usamos una función recursiva para visitar cada nodo de la lista.

## Buscar en listas enlazadas

Hay dos formas de buscar un elemento de datos determinado en una lista vinculada:

1. **Búsqueda iterativa**: En este tipo de búsqueda, usamos un bucle para visitar cada nodo de la lista hasta encontrar el elemento de datos deseado.

2. **Búsqueda recursiva**: En este tipo de búsqueda, utilizamos una función recursiva para visitar cada nodo de la lista hasta encontrar el elemento de datos deseado.

## Invertir una lista enlazada

Hay dos formas de invertir una lista enlazada:

1. **Método iterativo**: en este método, usamos un ciclo para invertir los punteros de los nodos en la lista.

2. **Método recursivo**: En este método, usamos una función recursiva para invertir los punteros de los nodos en la lista.