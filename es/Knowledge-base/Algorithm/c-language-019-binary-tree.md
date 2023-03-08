---
title: [Lenguaje C] 019: árbol binario
description: 
published: true
date: 2023-02-13T03:32:19.970Z
tags: 
editor: markdown
dateCreated: 2023-02-13T03:32:17.830Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 019: Binary Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-019-binary-tree)
{.links-list}


# Árbol binario

Un árbol binario es una estructura de datos que permite unir dos nodos mediante una ruta desde la raíz hasta el hijo más a la izquierda y desde el hijo más a la izquierda hasta el hijo más a la derecha. El camino se llama camino desde la raíz hasta el hijo más a la izquierda, y desde el hijo más a la izquierda hasta el hijo más a la derecha.

Un árbol binario es una estructura de datos recursiva, lo que significa que se puede definir en términos de sí mismo. Un árbol binario es un árbol en el que cada nodo tiene dos hijos. El nodo raíz es el nodo superior del árbol. El hijo izquierdo es un nodo que está conectado al nodo raíz por una ruta desde el nodo raíz hasta el hijo más a la izquierda. El hijo derecho es un nodo que está conectado al nodo raíz por una ruta desde el nodo raíz hasta el hijo más a la derecha.

Los hijos de un nodo a veces se denominan hijo izquierdo y hijo derecho, respectivamente. Los términos padre e hijo también se utilizan para describir la relación entre los nodos en un árbol binario. Un nodo es el padre de otro nodo si el primer nodo está conectado al segundo nodo por una ruta desde el nodo raíz hasta el primer nodo. Un nodo es hijo de otro nodo si el primer nodo está conectado al segundo nodo por un camino del primer nodo al segundo nodo.

La altura de un nodo es la longitud del camino más largo desde el nodo raíz hasta el nodo. La altura de un árbol es la altura del nodo raíz.

La profundidad de un nodo es la longitud del camino más corto desde el nodo raíz hasta el nodo. La profundidad de un árbol es la profundidad del nodo raíz.

Se dice que un árbol binario está lleno si cada nodo tiene dos hijos o ninguno. Se dice que un árbol binario está completo si cada nodo tiene dos hijos o ningún hijo y todas las hojas están a la misma profundidad.

Se dice que un árbol binario está equilibrado si la altura del subárbol izquierdo y la altura del subárbol derecho difieren como máximo en 1.

Aquí hay un ejemplo de un árbol binario:


        1
       / \
      2 3
     / \
    4 5

El nodo raíz es 1. El hijo izquierdo de 1 es 2. El hijo derecho de 1 es 3. El hijo izquierdo de 2 es 4. El hijo derecho de 2 es 5.

La profundidad del nodo raíz es 0. La profundidad del nodo 2 es 1. La profundidad del nodo 3 es 1. La profundidad del nodo 4 es 2. La profundidad del nodo 5 es 2.

La altura del nodo raíz es 2. La altura del nodo 2 es 1. La altura del nodo 3 es 1. La altura del nodo 4 es 0. La altura del nodo 5 es 0.

El árbol está lleno. El árbol está completo. El árbol está equilibrado.