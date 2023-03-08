---
title: [C Language] 006: Greedy Algorithms
description: 
published: true
date: 2023-02-12T17:32:31.858Z
tags: 
editor: markdown
dateCreated: 2023-02-12T17:32:25.155Z
---

- [[Lenguaje C] 006: Algoritmos codiciosos***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-006-greedy-algorithms)
{.links-list}
- [【C语言】006：贪心算法***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-006-greedy-algorithms)
{.links-list}
- [[C언어] 006: 그리디 알고리즘***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-006-greedy-algorithms)
{.links-list}


# Greedy Algorithms

In computer science, a greedy algorithm is an algorithm that follows the problem-solving heuristic of making the locally optimal choice at each stage with the hope of finding a global optimum. In many problems, a greedy strategy does not usually produce an optimal solution, but nonetheless a greedy heuristic may be the best strategy for some problems, producing an approximation to a correct solution in a reasonable amount of time.

## What is a Greedy Algorithm?

A greedy algorithm is an algorithm that makes the locally optimal choice at each stage with the hope of finding the global optimum.

The main difference between a greedy algorithm and other algorithms is that a greedy algorithm never reconsiders its choices, even if that would lead to a better overall solution.

## How do Greedy Algorithms Work?

Greedy algorithms work by making the locally optimal choice at each stage with the hope of finding the global optimum.

The key to understanding how greedy algorithms work is to realize that they are not always looking for the best overall solution, but rather for the best solution at each individual stage.

## When to Use Greedy Algorithms?

Greedy algorithms are best used when the locally optimal choice is likely to lead to the global optimum.

One common example of this is the shortest path problem. In the shortest path problem, we are given a set of nodes and a set of edges connecting them. We are also given a starting node and a goal node. The goal of the problem is to find the shortest path from the starting node to the goal node.

A greedy algorithm would solve this problem by always choosing the shortest path from the current node to the goal node. While this might not always find the shortest path overall, it is likely to find a path that is close to the shortest path.

## Code Examples

Here is a simple example of a greedy algorithm in action. Consider the following problem:

You are given a set of coins with different values, and you are asked to find the minimum number of coins needed to make a certain amount of money.

A greedy algorithm would solve this problem by always choosing the coin with the highest value first. For example, if the coins available are 1, 5, 10, and 25, and the amount of money you want to make is 30, then the greedy algorithm would choose the coin with value 25 first, followed by the coin with value 5. This would give a total of 2 coins, which is the minimum number of coins needed to make 30.

## Exercises

1. Implement the greedy algorithm for the coin change problem.

2. Consider the following problem: You are given a set of tasks that need to be completed, each with a certain duration. You also have a set of machines, each with a certain number of hours of available time. The goal of the problem is to find the minimum number of machines needed to complete all the tasks.

3. Use the greedy algorithm to solve the problem.

4. Consider the following problem: You are given a set of n tasks, each with a certain duration. You also have a set of m machines, each with a certain number of hours of available time. The goal of the problem is to find the minimum number of machines needed to complete all the tasks.

5. Use the greedy algorithm to solve the problem.