---
title: [JavaScript] 022: Trie
description: 
published: true
date: 2023-02-10T00:32:37.132Z
tags: 
editor: markdown
dateCreated: 2023-02-10T00:32:30.718Z
---

- [[JavaScript] 022: Trio***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-022-trie)
{.links-list}
- [[JavaScript] 022：特里***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-022-trie)
{.links-list}
- [[JavaScript] 022: 트라이***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-022-trie)
{.links-list}


# JavaScript 022: Trie

In computer science, a trie, also called digital tree or prefix tree, is a kind of search tree—an ordered tree data structure that is used to store a dynamic set or associative array where the keys are usually strings. Unlike a binary search tree, no node in the tree stores the key associated with that node; instead, its position in the tree defines the key with which it is associated. All the descendants of a node have a common prefix of the string associated with that node, and the root is associated with the empty string. Values are not necessarily associated with every node. Rather, values tend to be associated with leaves, and with some inner nodes that correspond to keys of interest. 

![Trie](https://upload.wikimedia.org/wikipedia/commons/thumb/b/be/Trie_example.svg/200px-Trie_example.svg.png)

In the example shown, keys are listed in the nodes and values below them. Each complete English word has an arbitrary integer value associated with it. When the trie is traversed from the root towards a particular key, the associated value is retrieved by concatenating the letters on the edges traversed. 

A trie can be seen as a tree-shaped deterministic finite automaton. A deterministic finite automaton is built from a set of states Q and a set of input symbols Σ, where Σ is the alphabet of the trie. The automaton has a start state s, a set of final states F, and a transition function that maps each state and input symbol to a new state. In a trie, the set of final states is generally the set of all strings. 

The transition function for a trie is defined as follows: given a state s and an input symbol a, the new state is obtained by descending from the state s along the edge labeled with the symbol a. If there is no edge labeled with the symbol a, then the new state is the failure state. In a trie, the failure state is generally the root.

A trie can be seen as a special case of an N-ary tree in which each node has at most N children, where N is the number of symbols in the alphabet. The path from the root to any leaf describes a prefix of the string associated with that leaf.

## Implementation

A trie can be implemented as an N-ary tree, a radix tree, a digital search tree, a digital tree, or a Patricia tree. 

### N-ary Tree

An N-ary tree is a rooted tree in which each node has no more than N children. A trie with N symbols in its alphabet can be seen as an N-ary tree in which each node has at most N children. 

![N-ary Tree](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Trie_nary_tree_example.svg/200px-Trie_nary_tree_example.svg.png)

In the example shown, the keys are listed in the nodes and the values are below them. Each complete English word has an arbitrary integer value associated with it. When the trie is traversed from the root towards a particular key, the associated value is retrieved by concatenating the letters on the edges traversed. 

A trie can be seen as a special case of an N-ary tree in which each node has at most N children, where N is the number of symbols in the alphabet. The path from the root to any leaf describes a prefix of the string associated with that leaf.

### Radix Tree

A radix tree or compressed tree is a kind of search tree in which the keys are strings. The tree is compressed by storing only the differences between successive keys. For example, if the keys are the words "Hello", "World", and "Hell", the root node will have the letters "H" and "W", and the first child of the root will have the letter "o". The second child of the root will have the letters "r" and "l". 

![Radix Tree](https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Radix_tree.svg/200px-Radix_tree.svg.png)

In the example shown, the keys are listed in the nodes and the values are below them. Each complete English word has an arbitrary integer value associated with it. When the trie is traversed from the root towards a particular key, the associated value is retrieved by concatenating the letters on the edges traversed. 

A radix tree can be seen as a special case of an N-ary tree in which each node has at most N children, where N is the number of symbols in the alphabet. The path from the root to any leaf describes a prefix of the string associated with that leaf.

### Digital Search Tree

A digital search tree or digital tree is a kind of search tree in which the keys are strings. The tree is compressed by storing only the differences between successive keys. For example, if the keys are the words "Hello", "World", and "Hell", the root node will have the letters "H" and "W", and the first child of the root will have the letter "o". The second child of the root will have the letters "r" and "l". 

![Digital Tree](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b4/Digital_tree.svg/200px-Digital_tree.svg.png)

In the example shown, the keys are listed in the nodes and the values are below them. Each complete English word has an arbitrary integer value associated with it. When the trie is traversed from the root towards a particular key, the associated value is retrieved by concatenating the letters on the edges traversed. 

A digital tree can be seen as a special case of an N-ary tree in which each node has at most N children, where N is the number of symbols in the alphabet. The path from the root to any leaf describes a prefix of the string associated with that leaf.

### Patricia Tree

A Patricia tree or radix tree is a kind of search tree in which the keys are strings. The tree is compressed by storing only the differences between successive keys. For example, if the keys are the words "Hello", "World", and "Hell", the root node will have the letters "H" and "W", and the first child of the root will have the letter "o". The second child of the root will have the letters "r" and "l". 

![Patricia Tree](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0d/Patricia_tree.svg/200px-Patricia_tree.svg.png)

In the example shown, the keys are listed in the nodes and the values are below them. Each complete English word has an arbitrary integer value associated with it. When the trie is traversed from the root towards a particular key, the associated value is retrieved by concatenating the letters on the edges traversed. 

A Patricia tree can be seen as a special case of an N-ary tree in which each node has at most N children, where N is the number of symbols in the alphabet. The path from the root to any leaf describes a prefix of the string associated with that leaf.

## Applications

Tries are used in many applications, such as:

- **Compression**: Tries can be used to compress strings by storing strings that have a common prefix in the same node. For example, the string "aaaabbbbccccdddd" can be compressed to "4a4b4c4d".

- **Spelling correction**: Tries can be used to store a dictionary of words and then used to check if a given word is spelled correctly.

- **IP address lookup**: Tries can be used to store a list of IP addresses and then used to lookup the IP address of a given host.

- **DNA sequence analysis**: Tries can be used to store DNA sequences and then used to find the matching DNA sequence for a given query.