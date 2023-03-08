---
title: [C Language] 007: Backtracking Algorithms
description: 
published: true
date: 2023-02-12T18:34:07.013Z
tags: 
editor: markdown
dateCreated: 2023-02-12T18:34:00.122Z
---

- [[Lenguaje C] 007: Algoritmos de retroceso***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-007-backtracking-algorithms)
{.links-list}
- [【C语言】007：回溯算法***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-007-backtracking-algorithms)
{.links-list}
- [[C언어] 007: 역추적 알고리즘***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-007-backtracking-algorithms)
{.links-list}


# C Language 007: Backtracking Algorithms

## What is Backtracking?

Backtracking is a general algorithm for finding all (or some) solutions to some computational problems, notably constraint satisfaction problems, that incrementally builds candidates to the solutions, and abandons each partial candidate ("backtracks") as soon as it determines that the candidate cannot possibly be completed to a valid solution.

## The Basic Idea

The basic idea is to construct partial solutions one element at a time. When we get stuck and cannot add any more element to the partial solutions, we "backtrack" by removing the last element we added and try another possibility. We keep doing this until we have found all solutions or we have exhausted all possibilities.

## Code Example

Here is a simple backtracking algorithm written in C that solves the 8-queens problem. The 8-queens problem is to place 8 queens on a chessboard so that no two queens can attack each other.

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

## Exercise

1. Modify the above code to solve the N-queens problem for N = 4, 6, 8, 10.

2. Try to solve the N-queens problem for N = 12. How many solutions are there?

## Answers

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