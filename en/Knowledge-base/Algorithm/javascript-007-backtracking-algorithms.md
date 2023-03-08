---
title: [JavaScript] 007: Backtracking Algorithms
description: 
published: true
date: 2023-02-09T09:32:38.173Z
tags: 
editor: markdown
dateCreated: 2023-02-09T09:32:32.093Z
---

- [[JavaScript] 007: Algoritmos de retroceso***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-007-backtracking-algorithms)
{.links-list}
- [[JavaScript] 007：回溯算法***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-007-backtracking-algorithms)
{.links-list}
- [[JavaScript] 007: 역추적 알고리즘***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-007-backtracking-algorithms)
{.links-list}


# JavaScript 007: Backtracking Algorithms

Backtracking is a general algorithm for finding all (or some) solutions to some computational problems, that incrementally builds candidates to the solutions, and abandons each partial candidate c ("backtracks") as soon as it determines that c cannot possibly be completed to a valid solution.

## The Basics

Backtracking is an algorithmic-technique for solving problems recursively by trying to build a solution incrementally, one piece at a time, removing those solutions that fail to satisfy all requirements as soon as they are recognized. The requirements for the current piece are represented by constraints, and the backtracking algorithm checks whether the constraints for the next piece are satisfied before moving on. If not, it "backs up" by undoing the changes to the previous piece, and trying a different approach.

The classic example of the backtracking algorithm is the Eight Queens Puzzle, which asks for all possible ways to place eight queens on a chessboard such that none of them can attack each other.

## Code Example

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

## Explanation

The backtracking algorithm starts by placing a queen in the first row of the chessboard and then proceeds to place queens in subsequent rows. In each row, it first looks for a column that is safe to place a queen in, and if it finds such a column, it places a queen in that column and moves on to the next row. If it does not find a safe column in the current row, it removes the queen from the previous row and backtracks to the previous row.

The isValid function is used to check if it is safe to place a queen in a given row and column. It checks if there are any queens placed in the same column, in the same row, or in any of the diagonals.

## Complexity Analysis

The time complexity of the backtracking algorithm is O(N^N), where N is the number of queens. This is because in each row, we have N choices for the column to place the queen in, and there are N rows.

The space complexity of the algorithm is O(N^2), which is the size of the chessboard.