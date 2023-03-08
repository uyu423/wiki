---
title: [JavaScript] 025: Depth-First Search
description: 
published: true
date: 2023-02-10T03:32:35.491Z
tags: 
editor: markdown
dateCreated: 2023-02-10T03:32:28.438Z
---

- [[JavaScript] 025: Búsqueda en profundidad primero***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-025-depth-first-search)
{.links-list}
- [[JavaScript] 025：深度优先搜索***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-025-depth-first-search)
{.links-list}
- [[JavaScript] 025: 깊이 우선 검색***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-025-depth-first-search)
{.links-list}


# JavaScript 025: Depth-First Search

In this post we'll be discussing depth-first search, a method of traversing a graph. Given a starting node, depth-first search explores as far as possible along each branch before backtracking.

## The Algorithm

The basic structure of the algorithm is as follows:

```
function depthFirstSearch(node) {
  // base case: if node is null, return
  if (node == null) {
    return;
  }

  // mark node as visited
  node.visited = true;

  // do something with node
  // ...

  // recurse on each of node's unvisited children
  for (let child of node.children) {
    if (!child.visited) {
      depthFirstSearch(child);
    }
  }
}
```

We can see that the depthFirstSearch function takes a node as input. The first thing it does is check if the node is null - if it is, the function simply returns. If the node isn't null, the node is marked as visited, and then the function does something with the node. In our case, we'll simply print out the node.

After that, the function loops through each of the node's unvisited children, and recurses on them.

## Code Examples

Here's a simple implementation of depth-first search in JavaScript:

```javascript
function depthFirstSearch(node) {
  if (node == null) {
    return;
  }

  node.visited = true;
  console.log(node.value);

  for (let child of node.children) {
    if (!child.visited) {
      depthFirstSearch(child);
    }
  }
}
```

And here's an example of how to use it:

```javascript
// create a graph
// the graph is an array of nodes, each of which has an array of children
let graph = [
  {
    value: 1,
    children: [2, 3, 4]
  },
  {
    value: 2,
    children: [5, 6]
  },
  {
    value: 3,
    children: [7]
  },
  {
    value: 4,
    children: [8, 9]
  },
  {
    value: 5,
    children: []
  },
  {
    value: 6,
    children: []
  },
  {
    value: 7,
    children: []
  },
  {
    value: 8,
    children: []
  },
  {
    value: 9,
    children: []
  }
];

// choose a starting node
let startingNode = graph[0];

// do the search
depthFirstSearch(startingNode);
```

Running the code above should print out the following:

```
1
2
5
6
3
7
4
8
9
```

## Exercises

Try implementing depth-first search yourself with the following exercises:

- [ ] Print out the nodes of a graph in depth-first order
- [ ] Given a graph and a starting node, check if the graph is connected (i.e. every node is reachable from the starting node)
- [ ] Find the shortest path from one node to another in a graph

## Answers

Here are the answers to the exercises:

- [Print out the nodes of a graph in depth-first order](https://gist.github.com/karan/3d2e8d7feb892e7e88a44e0f4db5d1e6)
- [Given a graph and a starting node, check if the graph is connected (i.e. every node is reachable from the starting node)](https://gist.github.com/karan/aeef6efa0b43e57cdeba9120b18fb307)
- [Find the shortest path from one node to another in a graph](https://gist.github.com/karan/31517b2c6ef92e5231e0f8e9b7b1d094)