---
title: [JavaScript] 007: Algoritmos de retroceso
description: 
published: true
date: 2023-02-09T09:32:33.667Z
tags: 
editor: markdown
dateCreated: 2023-02-09T09:32:32.092Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 007: Backtracking Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/javascript-007-backtracking-algorithms)
{.links-list}


# JavaScript 007: Algoritmos de retroceso

El backtracking es un algoritmo general para encontrar todas (o algunas) soluciones a algunos problemas computacionales, que crea candidatos para las soluciones de manera incremental y abandona cada candidato parcial c ("retrocede") tan pronto como determina que c no puede completarse hasta un solución válida.

## Los basicos

Backtracking es una técnica algorítmica para resolver problemas recursivamente al intentar construir una solución de forma incremental, una pieza a la vez, eliminando aquellas soluciones que no satisfacen todos los requisitos tan pronto como se reconocen. Los requisitos para la pieza actual están representados por restricciones, y el algoritmo de seguimiento verifica si se cumplen las restricciones para la siguiente pieza antes de continuar. Si no, "hace una copia de seguridad" deshaciendo los cambios a la pieza anterior y probando un enfoque diferente.

El ejemplo clásico del algoritmo de retroceso es el rompecabezas de las ocho reinas, que solicita todas las formas posibles de colocar ocho reinas en un tablero de ajedrez de modo que ninguna de ellas pueda atacarse entre sí.

## Ejemplo de código

```javascript
function solveNQueens(n) {
  const board = new Array(n).fill(null).map(() => new Array(n).fill('.'));

  const solutions = [];
  const helper = (row) => {
    if (row === n) {
      solutions.push([...board.map(r => r.join(''))]);
      return;
    }

    for (let col = 0; col < n; col++) {
      if (isValid(board, row, col)) {
        board[row][col] = 'Q';
        helper(row + 1);
        board[row][col] = '.';
      }
    }
  }
  helper(0);
  return solutions;
}

function isValid(board, row, col) {
  const n = board.length;

  // check column
  for (let i = 0; i < n; i++) {
    if (board[i][col] === 'Q') {
      return false;
    }
  }

  // check row
  for (let j = 0; j < n; j++) {
    if (board[row][j] === 'Q') {
      return false;
    }
  }

  // check diagonal
  for (let i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
    if (board[i][j] === 'Q') {
      return false;
    }
  }
  for (let i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++) {
    if (board[i][j] === 'Q') {
      return false;
    }
  }

  return true;
}
```

## Explicación

El algoritmo de retroceso comienza colocando una reina en la primera fila del tablero de ajedrez y luego procede a colocar reinas en las filas siguientes. En cada fila, primero busca una columna en la que sea seguro colocar una reina y, si la encuentra, coloca una reina en esa columna y pasa a la siguiente fila. Si no encuentra una columna segura en la fila actual, elimina la reina de la fila anterior y retrocede a la fila anterior.

La función isValid se usa para verificar si es seguro colocar una reina en una fila y columna determinada. Comprueba si hay reinas colocadas en la misma columna, en la misma fila o en alguna de las diagonales.

## Análisis de complejidad

La complejidad temporal del algoritmo de seguimiento inverso es O(N^N), donde N es el número de reinas. Esto se debe a que en cada fila tenemos N opciones para que la columna coloque la reina y hay N filas.

La complejidad espacial del algoritmo es O(N^2), que es el tamaño del tablero de ajedrez.