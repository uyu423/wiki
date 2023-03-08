---
title: [JavaScript] 007: 역추적 알고리즘
description: 
published: true
date: 2023-02-09T09:32:33.644Z
tags: 
editor: markdown
dateCreated: 2023-02-09T09:32:32.089Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 007: Backtracking Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/javascript-007-backtracking-algorithms)
{.links-list}


# JavaScript 007: 역추적 알고리즘

역추적은 일부 계산 문제에 대한 모든(또는 일부) 솔루션을 찾기 위한 일반적인 알고리즘으로, 솔루션에 대한 후보를 점진적으로 구축하고 각 부분 후보 c를 포기합니다("역추적"). 유효한 해결책.

## 기본 사항

역추적은 한 번에 한 조각씩 점진적으로 솔루션을 구축하고 모든 요구 사항을 충족하지 못하는 솔루션이 인식되는 즉시 제거함으로써 재귀적으로 문제를 해결하는 알고리즘 기술입니다. 현재 조각에 대한 요구 사항은 제약 조건으로 표시되며 역추적 알고리즘은 계속 진행하기 전에 다음 조각에 대한 제약 조건이 충족되는지 확인합니다. 그렇지 않은 경우 이전 조각에 대한 변경 사항을 실행 취소하고 다른 접근 방식을 시도하여 "백업"합니다.

역추적 알고리즘의 고전적인 예는 8개의 여왕 퍼즐로, 체스판에 8개의 여왕을 서로 공격할 수 없도록 배치하는 모든 가능한 방법을 묻습니다.

## 코드 예

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

## 설명

역추적 알고리즘은 체스판의 첫 번째 행에 여왕을 배치하는 것으로 시작하여 다음 행에 여왕을 배치합니다. 각 행에서 먼저 Queen을 배치하기에 안전한 열을 찾고, 그러한 열을 찾으면 해당 열에 Queen을 배치하고 다음 행으로 이동합니다. 현재 행에서 안전한 열을 찾지 못하면 이전 행에서 여왕을 제거하고 이전 행으로 되돌아갑니다.

isValid 함수는 주어진 행과 열에 여왕을 배치하는 것이 안전한지 확인하는 데 사용됩니다. 같은 열, 같은 행 또는 대각선에 배치된 여왕이 있는지 확인합니다.

## 복잡성 분석

역추적 알고리즘의 시간 복잡도는 O(N^N)이며, 여기서 N은 여왕의 수입니다. 각 행에는 여왕을 배치할 열에 대해 N개의 선택 항목이 있고 N개의 행이 있기 때문입니다.

알고리즘의 공간 복잡도는 체스판의 크기인 O(N^2)입니다.