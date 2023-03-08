---
title: [JavaScript] 007：回溯算法
description: 
published: true
date: 2023-02-09T09:32:33.672Z
tags: 
editor: markdown
dateCreated: 2023-02-09T09:32:32.090Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 007: Backtracking Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/javascript-007-backtracking-algorithms)
{.links-list}


# JavaScript 007：回溯算法

回溯是一种用于寻找某些计算问题的所有（或部分）解决方案的通用算法，它会逐步构建解决方案的候选方案，并在确定 c 不可能完成为 a 时立即放弃每个部分候选方案 c（“回溯”）有效的解决方案。

## 基础

回溯是一种算法技术，用于递归地解决问题，方法是尝试逐步构建一个解决方案，一次一个，一旦识别出那些不能满足所有要求的解决方案，就将其移除。当前片段的要求由约束表示，回溯算法在继续前检查下一个片段的约束是否满足。如果没有，它会通过撤消对前一块的更改并尝试不同的方法来“备份”。

回溯算法的经典例子是八皇后难题，它要求所有可能的方法将八个皇后放在棋盘上，使得它们中的任何一个都不能互相攻击。

## 代码示例

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

## 解释

回溯算法首先将皇后放置在棋盘的第一行，然后继续将皇后放置在后续行中。在每一行中，它首先寻找可以安全放置皇后的列，如果找到这样的列，它会在该列中放置一个皇后并移动到下一行。如果在当前行中没有找到安全列，它会从上一行中删除皇后并回溯到上一行。

isValid 函数用于检查在给定的行和列中放置皇后是否安全。它检查是否有皇后位于同一列、同一行或任何对角线上。

## 复杂度分析

回溯算法的时间复杂度为 O(N^N)，其中 N 为皇后数。这是因为在每一行中，我们有 N 列选择放置皇后，并且有 N 行。

该算法的空间复杂度为O(N^2)，也就是棋盘的大小。