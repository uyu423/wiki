---
title: [JavaScript] 045: R-Árbol
description: 
published: true
date: 2023-02-10T23:32:34.256Z
tags: 
editor: markdown
dateCreated: 2023-02-10T23:32:27.554Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 045: R-Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-045-r-tree)
{.links-list}


# R-Árbol

R-Tree es una estructura de datos que se utiliza para almacenar datos espaciales, como puntos, rectángulos y polígonos. Es un tipo de árbol de partición de espacio en el que cada nodo representa un área rectangular. El árbol está diseñado de tal manera que todos los rectángulos de un nodo dado están contenidos dentro del rectángulo de ese nodo.

Los R-Trees se utilizan a menudo en sistemas de información geográfica (GIS), diseño asistido por computadora (CAD) y procesamiento de imágenes.

## Cómo funciona

La idea básica detrás de un R-Tree es dividir un espacio bidimensional en un conjunto de rectángulos que no se superponen. Cada rectángulo está asociado con un objeto, como un punto, una línea o un polígono. Luego, los rectángulos se organizan en una estructura de árbol, con el nodo raíz que representa todo el espacio bidimensional. Los nodos secundarios del nodo raíz representan rectángulos más pequeños dentro del espacio, y así sucesivamente.

![RTree](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree.png)

La ventaja de usar un R-Tree es que se puede usar para encontrar rápidamente objetos que están cerca de un punto determinado. Por ejemplo, si queremos encontrar todos los puntos dentro de un radio dado de un punto dado, simplemente podemos consultar el R-Tree para todos los rectángulos que se cruzan con el radio. Esto es mucho más rápido que buscar en todo el espacio los puntos que caen dentro del radio.

## Inserción

La inserción en un R-Tree es un proceso de dos pasos. Primero, encontramos el nodo hoja donde se debe insertar el nuevo rectángulo. Para hacer esto, comenzamos en el nodo raíz y comparamos el nuevo rectángulo con cada uno de los rectángulos en el nodo raíz. A continuación, seleccionamos el rectángulo que coincida más con el nuevo rectángulo y repetimos el proceso con el nodo secundario asociado a ese rectángulo. Continuamos este proceso hasta llegar a un nodo hoja.

Una vez que hayamos encontrado el nodo hoja donde se debe insertar el nuevo rectángulo, simplemente agregamos el nuevo rectángulo a ese nodo.

![RTreeInsert](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree-insert.png)

## Eliminación

La eliminación de un R-Tree es un proceso de dos pasos. Primero, buscamos el nodo hoja donde se encuentra el rectángulo a eliminar. Para hacer esto, comenzamos en el nodo raíz y comparamos el rectángulo que se eliminará con cada uno de los rectángulos en el nodo raíz. A continuación, seleccionamos el rectángulo que es la coincidencia más cercana al rectángulo que se eliminará y repetimos el proceso con el nodo secundario asociado con ese rectángulo. Continuamos este proceso hasta llegar a un nodo hoja.

Una vez que hayamos encontrado el nodo hoja donde se encuentra el rectángulo, simplemente eliminamos el rectángulo de ese nodo.

![RTreeDelete](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree-delete.png)

## Consultando

Consultar un R-Tree es un proceso de dos pasos. Primero, encontramos los nodos hoja que intersecan con el rectángulo de consulta. Para hacer esto, comenzamos en el nodo raíz y comparamos el rectángulo de consulta con cada uno de los rectángulos en el nodo raíz. Luego, seleccionamos los rectángulos que se cruzan con el rectángulo de consulta y repetimos el proceso con los nodos secundarios asociados con esos rectángulos. Continuamos este proceso hasta llegar a un nodo hoja.

Una vez que hemos encontrado los nodos hoja que intersecan con el rectángulo de consulta, simplemente devolvemos los objetos asociados con esos rectángulos.

![RTreeQuery](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree-query.png)

## Implementación

Hay muchas formas de implementar un R-Tree. Un método popular es utilizar un quadtree, que es un tipo de árbol de partición de espacio en el que cada nodo tiene hasta cuatro nodos secundarios.

Otro método popular es utilizar un árbol k-d, que es un tipo de árbol de partición de espacio en el que cada nodo tiene hasta dos nodos secundarios.

## Conclusión

R-Trees son una poderosa estructura de datos para almacenar y consultar datos espaciales. Son eficientes y fáciles de implementar.