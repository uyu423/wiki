---
title: [C언어] 007: 역추적 알고리즘
description: 
published: true
date: 2023-02-12T18:34:01.846Z
tags: 
editor: markdown
dateCreated: 2023-02-12T18:34:00.118Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 007: Backtracking Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/c-language-007-backtracking-algorithms)
{.links-list}


# C 언어 007: 역추적 알고리즘

## 백트래킹이란?

역추적은 일부 계산 문제, 특히 제약 조건 만족 문제에 대한 모든(또는 일부) 솔루션을 찾기 위한 일반적인 알고리즘으로, 솔루션에 대한 후보를 점진적으로 구축하고 후보가 할 수 없다고 판단하는 즉시 각 부분 후보를 포기합니다("역추적"). 유효한 솔루션으로 완료될 수 있습니다.

## 기본 아이디어

기본 아이디어는 한 번에 한 요소씩 부분 솔루션을 구성하는 것입니다. 문제가 발생하여 부분 솔루션에 더 이상 요소를 추가할 수 없으면 추가한 마지막 요소를 제거하여 "역추적"하고 다른 가능성을 시도합니다. 우리는 모든 해결책을 찾거나 모든 가능성을 소진할 때까지 이 작업을 계속합니다.

## 코드 예

다음은 8퀸 문제를 해결하는 C로 작성된 간단한 역추적 알고리즘입니다. 8퀸 문제는 8개의 퀸을 체스판 위에 올려 두 퀸이 서로 공격할 수 없도록 하는 것입니다.

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

## 운동

1. 위 코드를 수정하여 N = 4, 6, 8, 10에 대한 N-queens 문제를 해결합니다.

2. N = 12인 N-queens 문제를 풀려고 합니다. 몇 개의 솔루션이 있습니까?

## 답변

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
# define N 8
 
/* 솔루션을 출력하기 위한 유틸리티 함수 */
무효 printSolution(int 보드[N][N])
{
    정적 정수 k = 1;
    printf("%d-\n\n",k++);
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
            printf(" %d ", 보드[i][j]);
        printf("\n");
    }
    printf("\n");
}
 
/* 여왕이 할 수 있는지 확인하는 유틸리티 함수
   board[row][col]에 안전하게 배치될 것인지 아닌지 */
bool isSafe(int 보드[N][N], int 행, int 열)
{
    정수 i, j;
 
    /* 왼쪽에서 이 행을 확인 */
    for (i = 0; i < 열; i++)
        if (보드[행][i])
            거짓을 반환합니다.
 
    /* 왼쪽 상단 대각선 확인 */
    for (i=row, j=col; i>=0 && j>=0; i--, j--)
        if (보드[i][j])
            거짓을 반환합니다.
 
    /* 왼쪽 하단 대각선 확인 */
    for (i=row, j=col; j>=0 && i<N; i++, j--)
        if (보드[i][j])
            거짓을 반환합니다.
 
    true를 반환합니다.
}
 
/* N을 해결하기 위한 재귀 유틸리티 함수
   여왕 문제 */
bool solveNQUtil(int board[N][N], int col)
{
    /* 기본 사례: 모든 여왕이 배치된 경우
       그런 다음 true 반환 */
    if(열 == N)
    {
        printSolution(보드);
        true를 반환합니다.
    }
 
    /* 이 열을 고려하고 배치해 보십시오.
       이 여왕은 모든 행에서 하나씩 */
    부울 해상도 = 거짓;
    for (int i = 0; i < N; i++)
    {
        /* 퀸을 배치할 수 있는지 확인
           보드[i][col] */
        if ( isSafe(board, i, col) )
        {
            /* 이 여왕을 board[i][col]에 배치 */
            보드[i][col] = 1;
 
            // 배치가 있으면 결과를 true로 만듭니다.
            // 가능하다
            res = solveNQUtil(보드, 열 + 1) || 입술;
 
            /* board[i][col]에 여왕을 배치하는 경우
               해결책으로 이어지지 않고
               보드[i][col]에서 퀸 제거 */
            보드[i][col] = 0; // 역추적
        }
    }
 
    /* 어떤 행에도 여왕을 배치할 수 없는 경우
       이 열 col은 false를 반환합니다 */
    반환 해상도;
}
 
/* 이 함수는 다음을 사용하여 N Queen 문제를 해결합니다.
   역추적. 주로 solveNQUtil()을 사용하여
   문제를 풀다. 여왕이면 거짓을 반환합니다.
   배치할 수 없습니다. 그렇지 않으면 true를 반환하고
   1의 형태로 여왕 배치.
   1개 이상이 있을 수 있으니 참고하세요