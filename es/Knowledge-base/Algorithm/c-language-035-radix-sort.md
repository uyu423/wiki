---
title: [Lenguaje C] 035: Clasificación Radix
description: 
published: true
date: 2023-02-13T15:33:04.743Z
tags: 
editor: markdown
dateCreated: 2023-02-13T15:32:57.191Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 035: Radix Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-035-radix-sort)
{.links-list}


# Clasificación Radix

Radix sort es un algoritmo de clasificación eficiente que clasifica los datos con claves enteras agrupando las claves por los dígitos individuales que comparten la misma posición y valor significativos. Se requiere una notación posicional, pero debido a que los números enteros pueden representar cadenas de caracteres (por ejemplo, en binario, un carácter se puede representar con ocho bits), la ordenación radix no se limita a los números enteros.

Radix sort mejora la eficiencia de las ordenaciones de comparación al crear un depósito para cada clave y colocar todas las claves con el mismo dígito en el mismo depósito. Esto reduce el número de comparaciones necesarias para clasificar los datos.

La complejidad temporal de la ordenación radix es O(n * k), donde n es el número de claves yk es el número de dígitos.

## Ejemplo de código

La siguiente es una implementación simple de radix sort en C.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
 
#define MAX_NUMBER_OF_DIGITS 10
 
void radix_sort(int *array, int n)
{
    int i, j, k, digit, divisor, count[10], temp[n];
 
    divisor = 1;
 
    for (i = 0; i < MAX_NUMBER_OF_DIGITS; i++)
    {
        for (j = 0; j < 10; j++)
        {
            count[j] = 0;
        }
 
        for (j = 0; j < n; j++)
        {
            digit = (array[j] / divisor) % 10;
            count[digit]++;
        }
 
        for (j = 1; j < 10; j++)
        {
            count[j] += count[j - 1];
        }
 
        for (j = n - 1; j >= 0; j--)
        {
            digit = (array[j] / divisor) % 10;
            temp[count[digit] - 1] = array[j];
            count[digit]--;
        }
 
        for (j = 0; j < n; j++)
        {
            array[j] = temp[j];
        }
 
        divisor *= 10;
    }
}
 
int main()
{
    int array[] = {329, 457, 657, 839, 436,720,355};
    int n = sizeof(array) / sizeof(array[0]);
 
    radix_sort(array, n);
 
    for (int i = 0; i < n; i++)
    {
        printf("%d ", array[i]);
    }
 
    return 0;
}
```

## Explicación

Radix sort funciona comenzando con el dígito menos significativo (LSD) y ordenando los datos en función de ese dígito. El LSD es el dígito en la posición de las unidades. El siguiente dígito a la izquierda es el segundo LSD, el dígito en la posición de las decenas. Este proceso se repite hasta que se han considerado todos los dígitos.

Para ordenar los datos, la ordenación radix usa una ordenación de conteo para cada dígito. Una clasificación de conteo realiza un seguimiento del número de claves que tienen un dígito dado en una posición específica. Por ejemplo, si se está considerando el LSD, la ordenación por conteo hará un seguimiento del número de teclas que tienen un 0 en la posición LSD, el número de teclas que tienen un 1 en la posición LSD, etc.

Una vez que se ha realizado la clasificación de conteo para el LSD, los datos se reorganizan para que todas las claves con el mismo LSD estén una al lado de la otra. Luego, las claves se ordenan según el siguiente dígito a la izquierda (es decir, el segundo LSD). Este proceso se repite hasta que se han considerado todos los dígitos.

Radix sort es un algoritmo de clasificación estable porque las claves se ordenan según los dígitos de derecha a izquierda. Esto significa que las teclas con los mismos dígitos en las posiciones más a la izquierda conservarán su orden relativo.

## Complejidad

La complejidad temporal de la ordenación radix es O(n * k), donde n es el número de claves yk es el número de dígitos. La complejidad del espacio es O(n + k).