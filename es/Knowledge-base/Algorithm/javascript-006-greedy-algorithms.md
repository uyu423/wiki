---
title: [JavaScript] 006: Algoritmos codiciosos
description: 
published: true
date: 2023-02-09T08:32:34.803Z
tags: 
editor: markdown
dateCreated: 2023-02-09T08:32:33.202Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 006: Greedy Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/javascript-006-greedy-algorithms)
{.links-list}


# Algoritmos codiciosos

Los algoritmos codiciosos son un tipo de algoritmo que toma la mejor decisión en cada paso para lograr el objetivo general. Por ejemplo, si el objetivo es encontrar la ruta más corta del punto A al punto B, un algoritmo voraz elegiría la ruta más corta en cada paso, sin tener en cuenta la longitud total de la ruta.

Uno de los ejemplos más famosos de un algoritmo codicioso es el problema del viajante de comercio. El objetivo de este problema es encontrar el camino más corto que visite cada ciudad exactamente una vez y regrese al punto de partida. Un enfoque ingenuo de este problema sería probar todos los caminos posibles y comparar las longitudes de cada uno. Sin embargo, esto es muy ineficiente y llevaría mucho tiempo ejecutarlo.

Un algoritmo codicioso, por otro lado, haría los siguientes pasos:

1. Comience en el punto de partida.
2. Encuentra la ciudad más cercana y visítala.
3. Encuentra la ciudad no visitada más cercana a la ciudad actual y visítala.
4. Repita el paso 3 hasta que haya visitado todas las ciudades.
5. Vuelve al punto de partida.

Los pasos anteriores siempre encontrarán un camino, pero puede que no sea el camino más corto posible. En algunos casos, es posible encontrar la solución óptima utilizando un algoritmo codicioso. En otros casos, no lo es.

## Implementación

Digamos que tenemos las siguientes ciudades y las distancias entre ellas:

```
City 1: 0km
City 2: 100km
City 3: 200km
City 4: 300km
City 5: 400km
```

Si usamos el algoritmo voraz descrito anteriormente, el camino tomado sería:

```
City 1 -> City 2 -> City 3 -> City 4 -> City 5 -> City 1
```

Que tiene una distancia total de:

```
0 + 100 + 200 + 300 + 400 + 0 = 1000km
```

Sin embargo, la ruta óptima sería:

```
City 1 -> City 5 -> City 4 -> City 3 -> City 2 -> City 1
```

Que tiene una distancia total de:

```
0 + 400 + 300 + 200 + 100 + 0 = 1000km
```

Como puede ver, el algoritmo codicioso no siempre encuentra la solución óptima. Sin embargo, suele ser mucho más rápido que otros algoritmos, como el enfoque de fuerza bruta, por lo que se suele utilizar en la práctica.

## Ejercicios

1. Implemente el algoritmo codicioso para el problema del viajante de comercio en el lenguaje de programación elegido.
2. Ejecute su algoritmo en el siguiente conjunto de ciudades y distancias:

```
City 1: 0km
City 2: 10km
City 3: 15km
City 4: 20km
City 5: 25km
```

¿Cuál es el camino recorrido y la distancia total? ¿Es este el camino óptimo?

3. Ejecute su algoritmo en el siguiente conjunto de ciudades y distancias:

```
City 1: 0km
City 2: 100km
City 3: 200km
City 4: 300km
City 5: 400km
```

¿Cuál es el camino recorrido y la distancia total? ¿Es este el camino óptimo?

4. Pruebe con otros conjuntos de ciudades y distancias y vea qué camino toma el algoritmo. ¿Puedes encontrar un conjunto en el que el algoritmo no encuentre la ruta óptima?

5. Intenta mejorar el algoritmo para que siempre encuentre la ruta óptima.