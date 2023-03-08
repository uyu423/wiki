---
title: [Lenguaje C] 007: Algoritmos de retroceso
description: 
published: true
date: 2023-02-12T18:34:01.767Z
tags: 
editor: markdown
dateCreated: 2023-02-12T18:34:00.121Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 007: Backtracking Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/c-language-007-backtracking-algorithms)
{.links-list}


# Lenguaje C 007: Algoritmos de retroceso

## ¿Qué es el retroceso?

Backtracking es un algoritmo general para encontrar todas (o algunas) soluciones a algunos problemas computacionales, en particular problemas de satisfacción de restricciones, que crea candidatos para las soluciones de manera incremental y abandona cada candidato parcial ("retrocesos") tan pronto como determina que el candidato no puede posiblemente se complete a una solución válida.

## La idea básica

La idea básica es construir soluciones parciales un elemento a la vez. Cuando nos atascamos y no podemos agregar más elementos a las soluciones parciales, "retrocedemos" eliminando el último elemento que agregamos y probamos otra posibilidad. Seguimos haciendo esto hasta que hayamos encontrado todas las soluciones o hayamos agotado todas las posibilidades.

## Ejemplo de código

Aquí hay un algoritmo de retroceso simple escrito en C que resuelve el problema de las 8 reinas. El problema de las 8 reinas consiste en colocar 8 reinas en un tablero de ajedrez de modo que dos reinas no puedan atacarse entre sí.

```c
#include <stdio.h>
#define N 8
 
/* A utility function to print solution */
void printSolution(int board[N][N])
{
    static int k = 1;
    printf("%d-\n\n",k++);
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
            printf(" %d ", board[i][j]);
        printf("\n");
    }
    printf("\n");
}
 
/* A utility function to check if a queen can
   be placed on board[row][col] safely or not */
bool isSafe(int board[N][N], int row, int col)
{
    int i, j;
 
    /* Check this row on left side */
    for (i = 0; i < col; i++)
        if (board[row][i])
            return false;
 
    /* Check upper diagonal on left side */
    for (i=row, j=col; i>=0 && j>=0; i--, j--)
        if (board[i][j])
            return false;
 
    /* Check lower diagonal on left side */
    for (i=row, j=col; j>=0 && i<N; i++, j--)
        if (board[i][j])
            return false;
 
    return true;
}
 
/* A recursive utility function to solve N
   Queen problem */
bool solveNQUtil(int board[N][N], int col)
{
    /* base case: If all queens are placed
       then return true */
    if (col == N)
    {
        printSolution(board);
        return true;
    }
 
    /* Consider this column and try placing
       this queen in all rows one by one */
    bool res = false;
    for (int i = 0; i < N; i++)
    {
        /* Check if queen can be placed on
           board[i][col] */
        if ( isSafe(board, i, col) )
        {
            /* Place this queen in board[i][col] */
            board[i][col] = 1;
 
            // Make result true if any placement
            // is possible
            res = solveNQUtil(board, col + 1) || res;
 
            /* If placing queen in board[i][col]
               doesn't lead to a solution, then
               remove queen from board[i][col] */
            board[i][col] = 0; // BACKTRACK
        }
    }
 
    /* If queen can not be place in any row in
       this column col then return false */
    return res;
}
 
/* This function solves the N Queen problem using
   Backtracking. It mainly uses solveNQUtil() to
   solve the problem. It returns false if queens
   cannot be placed, otherwise return true and
   placement of queens in the form of 1s.
   Please note that there may be more than one
   solutions, this function prints one  of the
   feasible solutions.*/
bool solveNQ()
{
    int board[N][N] = { {0, 0, 0, 0},
        {0, 0, 0, 0},
        {0, 0, 0, 0},
        {0, 0, 0, 0}
    };
 
    if (solveNQUtil(board, 0) == false)
    {
      printf("Solution does not exist");
      return false;
    }
 
    return true;
}
 
// driver program to test above function
int main()
{
    solveNQ();
    return 0;
}
```

## Ejercicio

1. Modifique el código anterior para resolver el problema de N-reinas para N = 4, 6, 8, 10.

2. Intenta resolver el problema de N-reinas para N = 12. ¿Cuántas soluciones hay?

## Respuestas

1.

```c
#include <stdio.h>
#define N 4
 
/* A utility function to print solution */
void printSolution(int board[N][N])
{
    static int k = 1;
    printf("%d-\n\n",k++);
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
            printf(" %d ", board[i][j]);
        printf("\n");
    }
    printf("\n");
}
 
/* A utility function to check if a queen can
   be placed on board[row][col] safely or not */
bool isSafe(int board[N][N], int row, int col)
{
    int i, j;
 
    /* Check this row on left side */
    for (i = 0; i < col; i++)
        if (board[row][i])
            return false;
 
    /* Check upper diagonal on left side */
    for (i=row, j=col; i>=0 && j>=0; i--, j--)
        if (board[i][j])
            return false;
 
    /* Check lower diagonal on left side */
    for (i=row, j=col; j>=0 && i<N; i++, j--)
        if (board[i][j])
            return false;
 
    return true;
}
 
/* A recursive utility function to solve N
   Queen problem */
bool solveNQUtil(int board[N][N], int col)
{
    /* base case: If all queens are placed
       then return true */
    if (col == N)
    {
        printSolution(board);
        return true;
    }
 
    /* Consider this column and try placing
       this queen in all rows one by one */
    bool res = false;
    for (int i = 0; i < N; i++)
    {
        /* Check if queen can be placed on
           board[i][col] */
        if ( isSafe(board, i, col) )
        {
            /* Place this queen in board[i][col] */
            board[i][col] = 1;
 
            // Make result true if any placement
            // is possible
            res = solveNQUtil(board, col + 1) || res;
 
            /* If placing queen in board[i][col]
               doesn't lead to a solution, then
               remove queen from board[i][col] */
            board[i][col] = 0; // BACKTRACK
        }
    }
 
    /* If queen can not be place in any row in
       this column col then return false */
    return res;
}
 
/* This function solves the N Queen problem using
   Backtracking. It mainly uses solveNQUtil() to
   solve the problem. It returns false if queens
   cannot be placed, otherwise return true and
   placement of queens in the form of 1s.
   Please note that there may be more than one
   solutions, this function prints one  of the
   feasible solutions.*/
bool solveNQ()
{
    int board[N][N] = { {0, 0, 0, 0},
        {0, 0, 0, 0},
        {0, 0, 0, 0},
        {0, 0, 0, 0}
    };
 
    if (solveNQUtil(board, 0) == false)
    {
      printf("Solution does not exist");
      return false;
    }
 
    return true;
}
 
// driver program to test above function
int main()
{
    solveNQ();
    return 0;
}
```

```c
#include <stdio.h>
#define N 6
 
/* A utility function to print solution */
void printSolution(int board[N][N])
{
    static int k = 1;
    printf("%d-\n\n",k++);
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
            printf(" %d ", board[i][j]);
        printf("\n");
    }
    printf("\n");
}
 
/* A utility function to check if a queen can
   be placed on board[row][col] safely or not */
bool isSafe(int board[N][N], int row, int col)
{
    int i, j;
 
    /* Check this row on left side */
    for (i = 0; i < col; i++)
        if (board[row][i])
            return false;
 
    /* Check upper diagonal on left side */
    for (i=row, j=col; i>=0 && j>=0; i--, j--)
        if (board[i][j])
            return false;
 
    /* Check lower diagonal on left side */
    for (i=row, j=col; j>=0 && i<N; i++, j--)
        if (board[i][j])
            return false;
 
    return true;
}
 
/* A recursive utility function to solve N
   Queen problem */
bool solveNQUtil(int board[N][N], int col)
{
    /* base case: If all queens are placed
       then return true */
    if (col == N)
    {
        printSolution(board);
        return true;
    }
 
    /* Consider this column and try placing
       this queen in all rows one by one */
    bool res = false;
    for (int i = 0; i < N; i++)
    {
        /* Check if queen can be placed on
           board[i][col] */
        if ( isSafe(board, i, col) )
        {
            /* Place this queen in board[i][col] */
            board[i][col] = 1;
 
            // Make result true if any placement
            // is possible
            res = solveNQUtil(board, col + 1) || res;
 
            /* If placing queen in board[i][col]
               doesn't lead to a solution, then
               remove queen from board[i][col] */
            board[i][col] = 0; // BACKTRACK
        }
    }
 
    /* If queen can not be place in any row in
       this column col then return false */
    return res;
}
 
/* This function solves the N Queen problem using
   Backtracking. It mainly uses solveNQUtil() to
   solve the problem. It returns false if queens
   cannot be placed, otherwise return true and
   placement of queens in the form of 1s.
   Please note that there may be more than one
   solutions, this function prints one  of the
   feasible solutions.*/
bool solveNQ()
{
    int board[N][N] = { {0, 0, 0, 0, 0, 0},
        {0, 0, 0, 0, 0, 0},
        {0, 0, 0, 0, 0, 0},
        {0, 0, 0, 0, 0, 0},
        {0, 0, 0, 0, 0, 0},
        {0, 0, 0, 0, 0, 0}
    };
 
    if (solveNQUtil(board, 0) == false)
    {
      printf("Solution does not exist");
      return false;
    }
 
    return true;
}
 
// driver program to test above function
int main()
{
    solveNQ();
    return 0;
}
```

```c
# incluir <stdio.h>
# definir N 8
 
/* Una función de utilidad para imprimir la solución */
void printSolution(tablero int[N][N])
{
    int estático k = 1;
    printf("%d-\n\n",k++);
    para (int i = 0; i < N; i++)
    {
        para (int j = 0; j < N; j++)
            printf(" %d ", tablero[i][j]);
        imprimirf("\n");
    }
    imprimirf("\n");
}
 
/* Una función de utilidad para verificar si una reina puede
   colocarse a bordo[fila][col] de forma segura o no */
bool isSafe(tablero int[N][N], fila int, columna int)
{
    i, j;
 
    /* Verifique esta fila en el lado izquierdo */
    para (i = 0; i < col; i++)
        si (tablero [fila] [i])
            falso retorno;
 
    /* Revisa la diagonal superior del lado izquierdo */
    para (i=fila, j=columna; i>=0 && j>=0; i--, j--)
        si (tablero[i][j])
            falso retorno;
 
    /* Revisar la diagonal inferior del lado izquierdo */
    para (i=fila, j=columna; j>=0 && i<N; i++, j--)
        si (tablero[i][j])
            falso retorno;
 
    devolver verdadero;
}
 
/* Una función de utilidad recursiva para resolver N
   Problema de la reina */
bool solveNQUtil(tablero int[N][N], columna int)
{
    /* caso base: si se colocan todas las reinas
       luego devuelve verdadero */
    si (columna == N)
    {
        imprimirSolucion(tablero);
        devolver verdadero;
    }
 
    /* Considere esta columna e intente colocar
       esta reina en todas las filas una a una */
    booleano res = falso;
    para (int i = 0; i < N; i++)
    {
        /* Comprobar si la reina se puede colocar en
           tablero[i][col] */
        if ( isSafe(tablero, i, col) )
        {
            /* Coloca esta reina en el tablero[i][col] */
            tablero[i][col] = 1;
 
            // Hacer que el resultado sea verdadero si hay alguna ubicación
            // es posible
            res = solveNQUtil(tablero, columna + 1) || res;
 
            /* Si se coloca la reina en el tablero[i][col]
               no conduce a una solución, entonces
               quitar reina del tablero[i][col] */
            tablero[i][col] = 0; // RETRACTARSE
        }
    }
 
    /* Si la reina no se puede colocar en ninguna fila en
       esta columna col luego devuelve falso */
    volver res;
}
 
/* Esta función resuelve el problema de N Queen usando
   Retrocediendo. Utiliza principalmente solveNQUtil() para
   resolver el problema. Devuelve falso si reinas
   no se puede colocar, de lo contrario devuelve verdadero y
   colocación de reinas en forma de 1s.
   Tenga en cuenta que puede haber más de uno