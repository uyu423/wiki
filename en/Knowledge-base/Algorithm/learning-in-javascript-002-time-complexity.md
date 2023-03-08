---
title: [Learning in JavaScript] 002: Time Complexity
description: 
published: true
date: 2023-02-09T04:33:16.114Z
tags: 
editor: markdown
dateCreated: 2023-02-09T04:33:09.141Z
---

- [[Aprendizaje en JavaScript] 002: Complejidad del tiempo***Spanish** document is available*](/es/Knowledge-base/Algorithm/learning-in-javascript-002-time-complexity)
{.links-list}
- [[学习JavaScript] 002：时间复杂度***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/learning-in-javascript-002-time-complexity)
{.links-list}
- [[자바스크립트 학습] 002: 시간 복잡도***Korean** document is available*](/ko/Knowledge-base/Algorithm/learning-in-javascript-002-time-complexity)
{.links-list}


# Learning in JavaScript: 002 Time Complexity

In computer science, the time complexity of an algorithm is the amount of time it takes to run, measured in the number of operations performed. Time complexity is usually expressed as a function of the input size, n. For example, an algorithm that takes seconds to run on an input of size n would have a time complexity of O(n^2).

There are two types of time complexity: worst-case and average-case. Worst-case time complexity is the amount of time it takes for the algorithm to run on the worst-case input, which is the input of size n that takes the most time to run. Average-case time complexity is the amount of time it takes for the algorithm to run on average-case inputs, which are inputs of size n that take an average amount of time to run.

The time complexity of an algorithm can be affected by the choice of data structures, the order in which operations are performed, and the algorithmic design pattern used.

## Data Structures

The choice of data structures can affect the time complexity of an algorithm. For example, consider the problem of searching for an element in an array. If the array is unsorted, the worst-case time complexity of the search algorithm is O(n), because the entire array must be searched. However, if the array is sorted, the worst-case time complexity of the search algorithm is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

## Order of Operations

The order in which operations are performed can also affect the time complexity of an algorithm. For example, consider the problem of sorting an array. The worst-case time complexity of the sorting algorithm is O(n log n), because the array must be divided into n log n partitions, and each partition must be sorted. However, if the array is already sorted, the worst-case time complexity of the sorting algorithm is O(n), because the array does not need to be divided into partitions and each element can be compared to the next element in the array.

## Algorithmic Design Patterns

There are a number of algorithmic design patterns that can be used to improve the time complexity of an algorithm. These design patterns include:

- Divide and conquer: This design pattern is used to divide the problem into smaller subproblems, solve the subproblems, and combine the solutions to the subproblems to solve the original problem.

- Greedy: This design pattern is used to make a locally optimal choice at each step in the hope of finding a global optimum.

- Dynamic programming: This design pattern is used to break the problem into smaller subproblems, solve the subproblems, and store the solutions to the subproblems in a table. The solutions to the subproblems can then be reused to solve the original problem.

- Brute force: This design pattern is used to try all possible solutions to the problem and select the best one.

## Code Examples

Here is a code example of a sorting algorithm with a time complexity of O(n log n):

```javascript
function sort(array) {
  if (array.length <= 1) {
    return array;
  }

  const pivot = array[0];
  const left = [];
  const right = [];

  for (let i = 1; i < array.length; i++) {
    const element = array[i];

    if (element <= pivot) {
      left.push(element);
    } else {
      right.push(element);
    }
  }

  return [...sort(left), pivot, ...sort(right)];
}
```

And here is a code example of a sorting algorithm with a time complexity of O(n):

```javascript
function sort(array) {
  for (let i = 0; i < array.length - 1; i++) {
    for (let j = i + 1; j < array.length; j++) {
      if (array[i] > array[j]) {
        const temp = array[i];
        array[i] = array[j];
        array[j] = temp;
      }
    }
  }

  return array;
}
```

## Exercises

1. Write a function that takes an array of integers and returns the sum of the elements in the array. What is the time complexity of the function?

2. Write a function that takes an array of integers and returns the largest integer in the array. What is the time complexity of the function?

3. Write a function that takes an array of integers and a target integer and returns the index of the target integer in the array. What is the time complexity of the function?

4. Write a function that takes an array of integers and a target integer and returns true if the target integer is in the array, and false if it is not. What is the time complexity of the function?

5. Write a function that takes an array of integers and returns the array sorted in ascending order. What is the time complexity of the function?

6. Write a function that takes an array of integers and a target integer and returns the index of the target integer in the array, or -1 if the target integer is not in the array. What is the time complexity of the function?

7. Write a function that takes an array of integers and a target integer and returns true if the target integer is in the array, and false if it is not. What is the time complexity of the function?

8. Write a function that takes an array of integers and returns the array sorted in ascending order. What is the time complexity of the function?

9. Write a function that takes an array of integers and a target integer and returns the index of the target integer in the array, or -1 if the target integer is not in the array. What is the time complexity of the function?

10. Write a function that takes an array of integers and a target integer and returns true if the target integer is in the array, and false if it is not. What is the time complexity of the function?

11. Write a function that takes an array of integers and a target integer and returns the index of the target integer in the array, or -1 if the target integer is not in the array. What is the time complexity of the function?

12. Write a function that takes an array of integers and a target integer and returns true if the target integer is in the array, and false if it is not. What is the time complexity of the function?

13. Write a function that takes an array of integers and returns the array sorted in ascending order. What is the time complexity of the function?

14. Write a function that takes an array of integers and a target integer and returns the index of the target integer in the array, or -1 if the target integer is not in the array. What is the time complexity of the function?

15. Write a function that takes an array of integers and a target integer and returns true if the target integer is in the array, and false if it is not. What is the time complexity of the function?

16. Write a function that takes an array of integers and a target integer and returns the index of the target integer in the array, or -1 if the target integer is not in the array. What is the time complexity of the function?

17. Write a function that takes an array of integers and a target integer and returns true if the target integer is in the array, and false if it is not. What is the time complexity of the function?

18. Write a function that takes an array of integers and a target integer and returns the index of the target integer in the array, or -1 if the target integer is not in the array. What is the time complexity of the function?

19. Write a function that takes an array of integers and a target integer and returns true if the target integer is in the array, and false if it is not. What is the time complexity of the function?

20. Write a function that takes an array of integers and a target integer and returns the index of the target integer in the array, or -1 if the target integer is not in the array. What is the time complexity of the function?

21. Write a function that takes an array of integers and a target integer and returns true if the target integer is in the array, and false if it is not. What is the time complexity of the function?

22. Write a function that takes an array of integers and a target integer and returns the index of the target integer in the array, or -1 if the target integer is not in the array. What is the time complexity of the function?

23. Write a function that takes an array of integers and a target integer and returns true if the target integer is in the array, and false if it is not. What is the time complexity of the function?

24. Write a function that takes an array of integers and a target integer and returns the index of the target integer in the array, or -1 if the target integer is not in the array. What is the time complexity of the function?

25. Write a function that takes an array of integers and a target integer and returns true if the target integer is in the array, and false if it is not. What is the time complexity of the function?

## Answers

1. The time complexity of the function is O(n), because the entire array must be traversed in order to calculate the sum.

2. The time complexity of the function is O(n), because the entire array must be traversed in order to find the largest integer.

3. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

4. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

5. The time complexity of the function is O(n log n), because the array must be divided into n log n partitions, and each partition must be sorted.

6. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

7. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

8. The time complexity of the function is O(n log n), because the array must be divided into n log n partitions, and each partition must be sorted.

9. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

10. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

11. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

12. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

13. The time complexity of the function is O(n log n), because the array must be divided into n log n partitions, and each partition must be sorted.

14. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

15. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

16. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

17. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

18. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

19. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

20. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

21. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

22. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

23. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

24. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.

25. The time complexity of the function is O(log n), because the array can be searched using a binary search, which halves the search space at each step.