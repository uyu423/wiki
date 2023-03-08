---
title: [Lenguaje C] 013: Deque
description: 
published: true
date: 2023-02-12T22:32:42.949Z
tags: 
editor: markdown
dateCreated: 2023-02-12T22:32:36.057Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 013: Deque***English** document is available*](/en/Knowledge-base/Algorithm/c-language-013-deque)
{.links-list}


# deque

Una deque, también conocida como cola de dos extremos, es una colección ordenada de elementos similar a una pila o una cola. Los deques son una generalización de pilas y colas (el nombre se pronuncia "mazo" y es la abreviatura de "cola de dos extremos").

Deques admite agregar y eliminar elementos de cualquier extremo de la estructura de datos en tiempo constante. Por el contrario, las colas y las pilas requieren un tiempo lineal para agregar o eliminar elementos.

## Implementación

Una deque se puede implementar como una matriz dinámica o una lista enlazada.

### Matriz dinámica

Una matriz dinámica es una buena opción para un deque si se conoce de antemano el número máximo de elementos. La matriz se puede cambiar de tamaño según sea necesario.

Para implementar una deque con una matriz dinámica, podemos usar una matriz circular. Esto nos permite evitar la necesidad de cambiar elementos cuando se agregan o eliminan elementos del deque.

![Matriz circular](https://i.imgur.com/zk0Fgdq.png)

Los índices delantero y trasero se pueden controlar con dos variables. El índice delantero representa el índice del primer elemento del deque y el índice trasero representa el índice del último elemento del deque.

Para agregar un elemento al frente del deque, disminuimos el índice frontal e insertamos el elemento en ese índice. Si el índice frontal es menor que 0, nos desplazamos hasta el final de la matriz.

Para agregar un elemento en la parte posterior del deque, incrementamos el índice posterior e insertamos el elemento en ese índice. Si el índice posterior es igual al tamaño de la matriz, nos desplazamos hasta el comienzo de la matriz.

Para eliminar un elemento del frente del deque, simplemente eliminamos el elemento en el índice frontal. Para eliminar un elemento de la parte posterior del deque, eliminamos el elemento en el índice posterior.

### Lista enlazada

Una lista enlazada es una buena opción para un deque si no se conoce de antemano el número máximo de elementos.

Para implementar una deque con una lista enlazada, podemos usar una lista doblemente enlazada. Esto nos permite agregar y eliminar elementos de cualquier extremo de la deque en tiempo constante.

![Lista de enlaces dobles](https://i.imgur.com/7W5rNcu.png)

Los punteros delantero y trasero se pueden controlar con dos variables. El puntero frontal representa el primer nodo de la deque y el puntero posterior representa el último nodo de la deque.

Para agregar un elemento al frente del deque, simplemente insertamos el elemento al frente de la lista. Para agregar un elemento al final del deque, insertamos el elemento al final de la lista.

Para eliminar un elemento del frente de la deque, simplemente eliminamos el elemento del frente de la lista. Para eliminar un elemento de la parte posterior del deque, eliminamos el elemento de la parte posterior de la lista.

## Aplicaciones

Los deques tienen muchas aplicaciones. Algunas de las aplicaciones más comunes se describen a continuación.

### Cola

Una cola es una estructura de datos que permite agregar elementos en un extremo y eliminarlos en el otro extremo. Una cola a menudo se denomina estructura de datos primero en entrar, primero en salir (FIFO).

Una cola se puede implementar con un deque. Para agregar un elemento a la cola, lo agregamos al final del deque. Para eliminar un elemento de la cola, lo eliminamos del frente del deque.

### Pila

Una pila es una estructura de datos que permite agregar y eliminar elementos de un solo extremo. Una pila a menudo se denomina estructura de datos de último en entrar, primero en salir (LIFO).

Una pila se puede implementar con un deque. Para agregar un elemento a la pila, lo agregamos al frente del deque. Para eliminar un elemento de la pila, lo eliminamos del frente del deque.

### palíndromo

Un palíndromo es una palabra, frase o número que es igual hacia adelante y hacia atrás. Por ejemplo, "carro de carreras" y "1001" son palíndromos.

Para comprobar si una palabra es un palíndromo, podemos usar un deque. Agregamos cada carácter de la palabra en la parte posterior del deque. Luego eliminamos cada carácter del deque y lo comparamos con el carácter correspondiente del frente del deque. Si todos los caracteres coinciden, entonces la palabra es un palíndromo.

## Análisis de complejidad

Los deques tienen las siguientes complejidades temporales:

- Acceso: O(1)
- Busca en)
- Inserción: O(1)
- Supresión: O(1)

donde n es el número de elementos en el deque.

Los deques tienen las siguientes complejidades espaciales:

- Matriz estática: O(n)
- Matriz dinámica: O(n)
- Lista enlazada: O(n)

donde n es el número máximo de elementos que se pueden almacenar en el deque.