---
title: [Lenguaje C] 006: Algoritmos codiciosos
description: 
published: true
date: 2023-02-12T17:32:26.780Z
tags: 
editor: markdown
dateCreated: 2023-02-12T17:32:25.153Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 006: Greedy Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/c-language-006-greedy-algorithms)
{.links-list}


# Algoritmos codiciosos

En informática, un algoritmo codicioso es un algoritmo que sigue la heurística de resolución de problemas de hacer la elección óptima localmente en cada etapa con la esperanza de encontrar un óptimo global. En muchos problemas, una estrategia voraz no suele producir una solución óptima, sin embargo, una heurística voraz puede ser la mejor estrategia para algunos problemas, produciendo una aproximación a una solución correcta en un tiempo razonable.

## ¿Qué es un algoritmo codicioso?

Un algoritmo codicioso es un algoritmo que hace la elección localmente óptima en cada etapa con la esperanza de encontrar el óptimo global.

La principal diferencia entre un algoritmo codicioso y otros algoritmos es que un algoritmo codicioso nunca reconsidera sus elecciones, incluso si eso llevaría a una mejor solución general.

## ¿Cómo funcionan los algoritmos codiciosos?

Los algoritmos codiciosos funcionan haciendo la elección localmente óptima en cada etapa con la esperanza de encontrar el óptimo global.

La clave para comprender cómo funcionan los algoritmos voraces es darse cuenta de que no siempre buscan la mejor solución general, sino la mejor solución en cada etapa individual.

## ¿Cuándo usar algoritmos codiciosos?

Los algoritmos codiciosos se utilizan mejor cuando es probable que la opción óptima localmente conduzca a la óptima global.

Un ejemplo común de esto es el problema del camino más corto. En el problema del camino más corto, tenemos un conjunto de nodos y un conjunto de aristas que los conectan. También tenemos un nodo inicial y un nodo objetivo. El objetivo del problema es encontrar el camino más corto desde el nodo inicial hasta el nodo objetivo.

Un algoritmo codicioso resolvería este problema eligiendo siempre el camino más corto desde el nodo actual hasta el nodo objetivo. Si bien es posible que esto no siempre encuentre la ruta más corta en general, es probable que encuentre una ruta que esté cerca de la ruta más corta.

## Ejemplos de código

Aquí hay un ejemplo simple de un algoritmo codicioso en acción. Considere el siguiente problema:

Se le da un conjunto de monedas con diferentes valores y se le pide que encuentre la cantidad mínima de monedas necesarias para hacer una cierta cantidad de dinero.

Un algoritmo codicioso resolvería este problema eligiendo siempre primero la moneda con el valor más alto. Por ejemplo, si las monedas disponibles son 1, 5, 10 y 25, y la cantidad de dinero que desea ganar es 30, entonces el algoritmo codicioso elegiría primero la moneda con valor 25, seguida de la moneda con valor 5. Esto daría un total de 2 monedas, que es la cantidad mínima de monedas necesarias para hacer 30.

## Ejercicios

1. Implementar el algoritmo voraz para el problema de cambio de moneda.

2. Considere el siguiente problema: se le asigna un conjunto de tareas que deben completarse, cada una con una duración determinada. También tienes un conjunto de máquinas, cada una con un cierto número de horas de tiempo disponible. El objetivo del problema es encontrar el número mínimo de máquinas necesarias para completar todas las tareas.

3. Usa el algoritmo codicioso para resolver el problema.

4. Considere el siguiente problema: se le asigna un conjunto de n tareas, cada una con una duración determinada. También tienes un conjunto de m máquinas, cada una con un cierto número de horas de tiempo disponible. El objetivo del problema es encontrar el número mínimo de máquinas necesarias para completar todas las tareas.

5. Usa el algoritmo codicioso para resolver el problema.