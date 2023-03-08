---
title: [Lenguaje C] 029: Clasificación de burbuja
description: 
published: true
date: 2023-02-13T10:33:00.177Z
tags: 
editor: markdown
dateCreated: 2023-02-13T10:32:58.604Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 029: Bubble Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-029-bubble-sort)
{.links-list}


# 029: Clasificación de burbujas

Bubble sort es un algoritmo de clasificación que funciona intercambiando repetidamente los elementos adyacentes si están en el orden incorrecto. El nombre tipo burbuja proviene del hecho de que los elementos más pequeños "burbujean" en la parte superior de la lista, mientras que los elementos más grandes se hunden en la parte inferior.

Bubble sort es uno de los algoritmos de clasificación más simples, pero también es uno de los más ineficientes. Tiene una complejidad media y en el peor de los casos de **O(n^2)** donde **n** es el número de elementos que se ordenan. A pesar de su simplicidad e ineficiencia, la ordenación por burbuja todavía se usa en algunos casos porque es fácil de implementar.

## Algoritmo

La idea básica detrás de la ordenación de burbujas es comparar cada elemento con su elemento adyacente e intercambiarlos si están en el orden incorrecto. Este proceso se repite hasta que se ordena toda la lista.

Considere la siguiente lista de números que deben ordenarse en orden ascendente:

[5, 1, 4, 2, 8]

Comparamos los primeros dos elementos, 5 y 1, y los intercambiamos ya que 5 es mayor que 1. La lista ahora se convierte en:

[1, 5, 4, 2, 8]

Comparamos los siguientes dos elementos, 5 y 4, y los intercambiamos ya que 5 es mayor que 4. La lista ahora se convierte en:

[1, 4, 5, 2, 8]

Comparamos los siguientes dos elementos, 5 y 2, y los intercambiamos ya que 5 es mayor que 2. La lista ahora se convierte en:

[1, 4, 2, 5, 8]

Comparamos los siguientes dos elementos, 5 y 8, y no los intercambiamos ya que 5 no es mayor que 8. La lista ahora se convierte en:

[1, 4, 2, 5, 8]

En este punto, la lista ya está ordenada, por lo que podemos detenernos.

La siguiente animación muestra el proceso completo de clasificación de burbujas para la lista [5, 1, 4, 2, 8]:

![Animación de clasificación de burbujas](https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif)

## Complejidad

Como se mencionó anteriormente, la ordenación de burbujas tiene una complejidad media y en el peor de los casos de **O(n^2)**. Esto se debe a que el algoritmo necesita comparar cada elemento con todos los demás elementos de la lista e intercambiarlos si están en el orden incorrecto.

El mejor de los casos para la ordenación de burbuja ocurre cuando la lista ya está ordenada. En este caso, el algoritmo no necesitará hacer ningún intercambio y la complejidad será **O(n)**.

## Implementación

Aquí hay una implementación simple de la ordenación de burbujas en el lenguaje de programación C:

```C
void bubble_sort(int array[], int n)
{
    int i, j, temp;

    for (i = 0; i < n - 1; i++)
    {
        for (j = 0; j < n - i - 1; j++)
        {
            if (array[j] > array[j + 1])
            {
                temp = array[j];
                array[j] = array[j + 1];
                array[j + 1] = temp;
            }
        }
    }
}
```

## Ejercicio

1. Implemente el algoritmo de clasificación de burbujas en su propio lenguaje de programación.

2. Modifique el algoritmo de clasificación de burbujas para que se detenga antes si la lista ya está ordenada.

## Respuestas

1.

```C
void bubble_sort(int array[], int n)
{
    int i, j, temp;

    for (i = 0; i < n - 1; i++)
    {
        for (j = 0; j < n - i - 1; j++)
        {
            if (array[j] > array[j + 1])
            {
                temp = array[j];
                array[j] = array[j + 1];
                array[j + 1] = temp;
            }
        }
    }
}
```

2.

```C
void bubble_sort(int array[], int n)
{
    int i, j, temp;
    bool swapped;

    for (i = 0; i < n - 1; i++)
    {
        swapped = false;

        for (j = 0; j < n - i - 1; j++)
        {
            if (array[j] > array[j + 1])
            {
                temp = array[j];
                array[j] = array[j + 1];
                array[j + 1] = temp;

                swapped = true;
            }
        }

        if (!swapped)
        {
            break;
        }
    }
}
```