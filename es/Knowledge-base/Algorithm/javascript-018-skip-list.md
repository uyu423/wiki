---
title: [JavaScript] 018: Lista de omisión
description: 
published: true
date: 2023-02-09T20:32:40.041Z
tags: 
editor: markdown
dateCreated: 2023-02-09T20:32:38.420Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 018: Skip List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-018-skip-list)
{.links-list}


# Omitir lista

Una lista de saltos es una estructura de datos que permite una búsqueda eficiente dentro de una secuencia ordenada de elementos. Es un tipo de lista enlazada que emplea una estructura jerárquica de nodos, en la que cada nodo tiene múltiples "enlaces" a otros nodos en diferentes niveles dentro de la jerarquía. Esta lista de exclusión fue descrita por primera vez por Pugh en su artículo de 1990 "Listas de exclusión: una alternativa probabilística a los árboles equilibrados".

La lista de omisión es una estructura de datos aleatoria, lo que significa que el orden en el que se vinculan los nodos está determinado por un generador de números aleatorios. La ventaja de este enfoque es que permite que la lista de saltos se construya en tiempo O(n), donde n es el número de elementos que se insertarán en la lista.

La lista de omisión tiene una serie de aplicaciones, incluso en bases de datos y sistemas de archivos. También se utiliza en la estructura de datos del árbol radix del kernel de Linux.

## Cómo funcionan las listas de exclusión

Una lista de omisión se compone de una serie de niveles, y cada nivel tiene un conjunto de nodos. El primer nivel es el nivel más bajo, y el último nivel es el nivel más alto. El número de niveles está determinado por un generador de números aleatorios.

Los nodos de cada nivel están vinculados entre sí en un orden ordenado. Los nodos del nivel más bajo están vinculados entre sí en orden de valor creciente, y los nodos de los niveles superiores están vinculados entre sí en orden de valor decreciente.

La lista de omisión también tiene un nodo "principal", que es el primer nodo en el nivel más bajo. El nodo principal tiene un puntero al primer nodo del siguiente nivel. Si no hay ningún nodo en el siguiente nivel, el puntero del nodo principal será nulo.

Cada nodo en la lista de omisión tiene un campo de "valor" y un campo de "nivel". El campo de valor almacena el valor del nodo y el campo de nivel almacena el nivel del nodo.

El nivel de un nodo está determinado por el generador de números aleatorios. La probabilidad de que a un nodo se le asigne un nivel i es 1/(2^i). Esto significa que la posibilidad de que un nodo se asigne al nivel más alto es 1/2, la posibilidad de que un nodo se asigne al segundo nivel más alto es 1/4, y así sucesivamente.

La lista de saltos se busca comenzando en el nodo principal y siguiendo los punteros hasta el siguiente nodo en el mismo nivel. Si el valor del siguiente nodo es menor que el valor que se busca, el puntero se sigue hasta el siguiente nodo en el mismo nivel. Este proceso se repite hasta llegar a un nodo con un valor mayor o igual al valor buscado. En este punto, la búsqueda sigue el puntero hasta el siguiente nodo en el nivel inferior y repite el proceso.

Si el valor que se busca no se encuentra en la lista de omisión, la búsqueda devuelve nulo.

## Ejemplo de código

Aquí hay una implementación Java simple de una lista de omisión. La clase "SkipList" representa una lista de saltos y la clase "Nodo" representa un nodo en la lista de saltos.

```java
public class SkipList {
    
    private Node head;
    private int size;
    private Random random;
    
    public SkipList() {
        head = new Node(Integer.MIN_VALUE);
        size = 0;
        random = new Random();
    }
    
    public void insert(int value) {
        Node node = new Node(value);
        Node current = head;
        while (current.value < value) {
            current = current.next;
        }
        node.next = current.next;
        current.next = node;
        size++;
    }
    
    public boolean contains(int value) {
        Node current = head;
        while (current.value < value) {
            current = current.next;
        }
        return current.value == value;
    }
    
    public int size() {
        return size;
    }
    
    private class Node {
        int value;
        Node next;
        
        public Node(int value) {
            this.value = value;
        }
    }
    
}
```

## Ejercicios

1. Implemente los métodos "insertar" y "contiene" para la clase SkipList.

2. Modifique la clase SkipList para usar una lista con enlaces dobles en lugar de una lista con enlaces simples.

3. Modifique la clase SkipList para realizar un seguimiento del número de nodos en cada nivel.

4. Modifique la clase SkipList para permitir el uso de comparadores personalizados para ordenar los elementos de la lista.

5. Modifique la clase SkipList para permitir que se utilicen funciones hash personalizadas para aplicar hash a los elementos de la lista.