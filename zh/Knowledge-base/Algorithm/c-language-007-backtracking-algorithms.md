---
title: 【C语言】007：回溯算法
description: 
published: true
date: 2023-02-12T18:34:01.759Z
tags: 
editor: markdown
dateCreated: 2023-02-12T18:34:00.118Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 007: Backtracking Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/c-language-007-backtracking-algorithms)
{.links-list}


# C语言007：回溯算法

## 什么是回溯？

回溯是一种通用算法，用于找到某些计算问题的所有（或部分）解决方案，特别是约束满足问题，它会逐步构建解决方案的候选方案，并在确定候选方案不能时立即放弃每个部分候选方案（“回溯”）可能完成一个有效的解决方案。

## 基本思想

基本思想是一次构建一个元素的部分解决方案。当我们陷入困境并且无法向部分解决方案添加更多元素时，我们通过删除我们添加的最后一个元素来“回溯”并尝试另一种可能性。我们一直这样做，直到找到所有解决方案或用尽所有可能性。

## 代码示例

这是一个用 C 编写的简单回溯算法，用于解决 8 皇后问题。 8 皇后问题是在一个棋盘上放置 8 个皇后，使得任何两个皇后都不能互相攻击。

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

## 锻炼

1.修改上面的代码，解决N=4,6,8,10的N皇后问题。

2. 尝试解决 N = 12 的 N 皇后问题。有多少种解决方案？

## 答案

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
# include <stdio.h>
# 定义 N 8
 
/* 打印解决方案的实用函数 */
void printSolution(int board[N][N])
{
    静态整数 k = 1；
    printf("%d-\n\n",k++);
    对于 (int i = 0; i < N; i++)
    {
        对于 (int j = 0; j < N; j++)
            printf(" %d ", board[i][j]);
        printf("\n");
    }
    printf("\n");
}
 
/* 一个实用函数来检查女王是否可以
   是否安全地放在船上[行][列] */
bool isSafe(int board[N][N], int row, int col)
{
    诠释我，j;
 
    /* 检查左边这一行 */
    对于 (i = 0; i < col; i++)
        如果（板[行][i]）
            返回假；
 
    /* 检查左边的上对角线 */
    for (i=row, j=col; i>=0 && j>=0; i--, j--)
        如果（棋盘[i][j]）
            返回假；
 
    /* 检查左边的下对角线 */
    for (i=row, j=col; j>=0 && i<N; i++, j--)
        如果（棋盘[i][j]）
            返回假；
 
    返回真；
}
 
/* 求解 N 的递归效用函数
   皇后问题 */
bool solveNQUtil(int board[N][N], int col)
{
    /* 基本情况：如果所有皇后都被放置
       然后返回真值 */
    如果（col == N）
    {
        打印解决方案（板）；
        返回真；
    }
 
    /* 考虑这一列并尝试放置
       所有行中的这个女王都一一*/
    布尔水库 = 假;
    对于 (int i = 0; i < N; i++)
    {
        /* 检查皇后是否可以放置
           棋盘[i][列] */
        if ( isSafe(board, i, col) )
        {
            /* 将这个皇后放在 board[i][col] 中 */
            板[i][col] = 1;
 
            // 如果有任何放置，则使结果为真
            // 是可能的
            res = solveNQUtil(board, col + 1) ||资源；
 
            /* 如果把皇后放在 board[i][col]
               不会导致解决方案，那么
               从 board[i][col] 中移除皇后 */
            板[i][col] = 0; // 回溯
        }
    }
 
    /* 如果皇后不能放在任何一行中
       此列 col 然后返回 false */
    返回资源；
}
 
/* 这个函数解决了 N 皇后问题，使用
   回溯。它主要使用solveNQUtil()来
   解决这个问题。如果是皇后则返回 false
   不能放置，否则返回 true 和
   以 1 的形式放置皇后。
   请注意，可能有多个