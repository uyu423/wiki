---
title: 003: 재귀를 사용하여 JavaScript에서 일반적인 프로그래밍 문제 해결
description: 
published: true
date: 2023-02-17T08:06:46.177Z
tags: 
editor: markdown
dateCreated: 2023-02-17T08:06:44.839Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [003: Using recursion to solve common programming problems in JavaScript***English** document is available*](/en/Knowledge-base/Functional_JavaScript/Learning/003-using-recursion-to-solve-common-programming-problems-in-javascript)
{.links-list}


# 재귀를 사용하여 JavaScript에서 일반적인 프로그래밍 문제 해결

재귀는 많은 일반적인 프로그래밍 문제를 해결하는 데 사용할 수 있는 강력한 도구입니다. 이 게시물에서는 재귀를 사용하여 JavaScript의 일반적인 문제를 해결하는 방법을 살펴봅니다.

## 재귀란?

재귀는 함수가 자신을 호출하는 프로세스입니다. 솔루션을 더 작은 하위 문제로 나눌 수 있는 문제를 해결하는 데 사용할 수 있습니다.

## 재귀함수는 어떻게 사용하나요?

재귀를 사용할 때 기본 사례와 재귀 사례가 있는 것이 중요합니다. 기본 사례는 문제의 가장 간단한 형태이며 재귀 사례는 함수가 자신을 호출하는 경우입니다.

## 예: 계승

재귀의 한 가지 일반적인 예는 숫자의 계승을 계산하는 것입니다. 숫자의 계승은 1에서 해당 숫자까지의 모든 정수의 곱입니다. 예를 들어, 5의 계승은 5 * 4 * 3 * 2 * 1입니다.

다음과 같이 재귀를 사용하여 숫자의 계승을 계산할 수 있습니다.

```javascript
function factorial(n) {
  // Base case
  if (n === 1) {
    return 1;
  }
  // Recursive case
  return n * factorial(n - 1);
}

console.log(factorial(5)); // 120
```

위의 예에서 기본 사례는 n이 1인 경우입니다. 재귀 사례는 함수가 n-1로 자신을 호출하는 경우입니다. 베이스 케이스에 도달할 때까지 계속 호출합니다.

## 예: 피보나치 수열

재귀의 또 다른 일반적인 예는 피보나치 수열입니다. 피보나치 수열은 각 숫자가 앞의 두 숫자의 합인 일련의 숫자입니다. 시퀀스의 처음 두 숫자는 0과 1입니다. 예를 들어 피보나치 수열은 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610입니다. , 987, 1597, 2584, 4181, 6765, 10946, 17711, 28657, 46368, 75025, 121393, 196418, 317811, 514229, 832040, 1346269, 2178309, 3524578, 5702887, 9227465, 14930352, 24157817, 39088169, 63245986, 102334155 , 165580141, 267914296, 433494437, 701408733, 1134903170, 1836311903, 2971215073, 4807526976, 7778742049, 12586269025, 20365011074, 32951280099, 53316291173, 86267571272, 139583862445, 225851433717, 365435296162, 591286729879, 969323036873, 1548008755920, 2504730781961, 4052739537881, 6557470319842, 10610209857723, 17167680177565 , 27777890035288, 44945570212853, 72723460248141, 11805916207174, 1930392490709135, 313528776555673
```

We can use recursion to calculate the Fibonacci sequence as follows:

```자바스크립트
함수 fib(n) {
  // 기본 케이스
  경우 (n <= 1) {
    n을 반환합니다.
  }
  // 재귀 사례
  fib(n - 1) + fib(n - 2) 반환;
}

console.log(fib(10)); // 55
```

In the example above, the base case is when n is less than or equal to 1. The recursive case is when the function calls itself with n-1 and n-2. This will keep calling itself until it reaches the base case.

## Example: Greatest Common Divisor

Another common example of recursion is finding the greatest common divisor (GCD) of two numbers. The GCD of two numbers is the largest number that divides both numbers evenly. For example, the GCD of 12 and 18 is 6.

We can use recursion to calculate the GCD of two numbers as follows:

```자바스크립트
함수 gcd(a, b) {
  // 기본 케이스
  경우 (b === 0) {
    반환;
  }
  // 재귀 사례
  return gcd(b, a % b);
}

console.log(gcd(12, 18)); // 6
```

In the example above, the base case is when b equals 0. The recursive case is when the function calls itself with b and a mod b. This will keep calling itself until it reaches the base case.

## Example: Binary Search

Binary search is a common algorithm that is used to search for an element in a sorted array. The binary search algorithm works by dividing the array in half and comparing the element to be searched for with the element in the middle of the array. If the element to be searched for is less than the element in the middle of the array, the algorithm will search the first half of the array. If the element to be searched for is greater than the element in the middle of the array, the algorithm will search the second half of the array. This process is repeated until the element is found or the array is exhausted.

We can use recursion to implement binary search as follows:

```자바스크립트
function binarySearch(arr, 요소) {
  // 기본 케이스
  if (배열 길이 === 0) {
    거짓을 반환합니다.
  }
  // 재귀 사례
  const 중간 = Math.floor(arr.length / 2);
  const middleElem = arr[중간];
  if (요소 === 중간 요소) {
    true를 반환합니다.
  } 그렇지 않으면 (요소 < 중간 요소) {
    return binarySearch(arr.slice(0, middle), elem);
  } 또 다른 {
    return binarySearch(arr.slice(middle + 1), elem);
  }
}

상수 arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
console.log(binarySearch(arr, 5)); // 진실
console.log(binarySearch(arr, 11)); // 거짓
```

위의 예에서 기본 사례는 배열이 비어 있는 경우입니다. 재귀적인 경우는 검색할 요소가 배열 중간에 있는 요소보다 작거나 큰지에 따라 함수가 배열의 첫 번째 절반 또는 두 번째 절반으로 자신을 호출하는 경우입니다. 베이스 케이스에 도달할 때까지 계속 호출합니다.

## 결론

이 게시물에서는 재귀를 사용하여 JavaScript의 일반적인 문제를 해결하는 방법을 살펴보았습니다. 재귀는 많은 일반적인 프로그래밍 문제를 해결하는 데 사용할 수 있는 강력한 도구입니다.