---
title: [JavaScript] 006: Greedy Algorithms
description: 
published: true
date: 2023-02-09T08:32:39.184Z
tags: 
editor: markdown
dateCreated: 2023-02-09T08:32:33.206Z
---

- [[JavaScript] 006: Algoritmos codiciosos***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-006-greedy-algorithms)
{.links-list}
- [[JavaScript] 006：贪心算法***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-006-greedy-algorithms)
{.links-list}
- [[JavaScript] 006: 탐욕스러운 알고리즘***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-006-greedy-algorithms)
{.links-list}


# Greedy Algorithms

Greedy algorithms are a type of algorithm that make the best choice at each step in order to achieve the overall goal. For example, if the goal is to find the shortest path from point A to point B, a greedy algorithm would choose the path that is shortest at each step, without regard for the overall path length.

One of the most famous examples of a greedy algorithm is the travelling salesman problem. The goal of this problem is to find the shortest path that visits each city exactly once and returns to the starting point. A naive approach to this problem would be to try every possible path and compare the lengths of each. However, this is very inefficient and would take a long time to run.

A greedy algorithm, on the other hand, would make the following steps:

1. Start at the starting point.
2. Find the closest city and visit it.
3. Find the closest unvisited city from the current city and visit it.
4. Repeat step 3 until all cities have been visited.
5. Return to the starting point.

The steps above will always find a path, but it may not be the shortest possible path. In some cases, it is possible to find the optimal solution using a greedy algorithm. In other cases, it is not.

## Implementation

Let's say we have the following cities and distances between them:

```
City 1: 0km
City 2: 100km
City 3: 200km
City 4: 300km
City 5: 400km
```

If we use the greedy algorithm described above, the path taken would be:

```
City 1 -> City 2 -> City 3 -> City 4 -> City 5 -> City 1
```

Which has a total distance of:

```
0 + 100 + 200 + 300 + 400 + 0 = 1000km
```

However, the optimal path would be:

```
City 1 -> City 5 -> City 4 -> City 3 -> City 2 -> City 1
```

Which has a total distance of:

```
0 + 400 + 300 + 200 + 100 + 0 = 1000km
```

As you can see, the greedy algorithm does not always find the optimal solution. However, it is usually much faster than other algorithms, such as the brute force approach, and so it is often used in practice.

## Exercises

1. Implement the greedy algorithm for the travelling salesman problem in your chosen programming language.
2. Run your algorithm on the following set of cities and distances:

```
City 1: 0km
City 2: 10km
City 3: 15km
City 4: 20km
City 5: 25km
```

What is the path taken and the total distance? Is this the optimal path?

3. Run your algorithm on the following set of cities and distances:

```
City 1: 0km
City 2: 100km
City 3: 200km
City 4: 300km
City 5: 400km
```

What is the path taken and the total distance? Is this the optimal path?

4. Try other sets of cities and distances and see what path is taken by the algorithm. Can you find a set where the algorithm does not find the optimal path?

5. Try to improve the algorithm so that it always finds the optimal path.