---
title: [JavaScript] 046: Trie
description: 
published: true
date: 2023-02-11T00:33:13.641Z
tags: 
editor: markdown
dateCreated: 2023-02-11T00:33:07.197Z
---

- [[JavaScript] 046: Trio***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-046-trie)
{.links-list}
- [[JavaScript] 046：特里***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-046-trie)
{.links-list}
- [[JavaScript] 046: 트라이***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-046-trie)
{.links-list}


# JavaScript 046: Trie

A trie, also called a digital tree or sometimes radix tree or prefix tree (as they can be searched by prefixes), is an ordered tree data structure that is used to store a dynamic set or associative array where the keys are usually strings. Unlike a binary search tree, no node in the tree stores the key associated with that node; instead, its position in the tree defines the key with which it is associated. All the descendants of a node have a common prefix of the string associated with that node, and the root is associated with the empty string. Values are not necessarily associated with every node. Rather, values tend to be associated with leaves, and with some inner nodes that correspond to keys of interest.

For the sake of simplicity, we will assume in this article that keys are single characters. A more realistic assumption would be that keys are strings of characters, but even this more general case can be reduced to the single-character case by considering the characters in the string to be a sequence of keystrokes.

## The Tree

A trie can be viewed as a tree with a very special property, namely that all the paths from the root to the leaves have the same length, and at each node on the path, this length is equal to the depth of the node in the tree. In other words, a trie is a tree in which all the leaves are at the same level.

![Trie](https://i.imgur.com/fgNcuqP.png)

Each node of the tree is labeled with a letter. The path from the root to a leaf corresponds to a word, and the label of each node on the path is the letter that forms the word. For example, in the above figure, the path from the root to the node labeled with the letter ‘c’ corresponds to the word “car”.

## The Algorithm

The basic idea behind the trie algorithm is to store the string to be searched in a trie data structure, and then to search the trie for the desired string.

The search algorithm starts at the root of the trie, and at each node it checks to see if the label on the node matches the next letter of the string to be searched. If there is a match, it moves to the next node in the trie (i.e., the child of the current node); if there is no match, it moves to the next node in the tree (i.e., the sibling of the current node). If the search reaches a leaf node without finding a match, then the string is not present in the trie.

![Trie-Search](https://i.imgur.com/bvU4r4e.png)

For example, consider the trie shown in the figure above, and suppose we want to search for the string “car”. The search algorithm starts at the root node, which is labeled with the letter ‘a’. Since this matches the first letter of the string, it moves to the child node, which is labeled with the letter ‘c’. Since this also matches the second letter of the string, it moves to the child node, which is labeled with the letter ‘a’. Since this does not match the third letter of the string, it moves to the next node, which is labeled with the letter ‘r’. Since this also does not match, it moves to the next node, which is labeled with the letter ‘b’. Since there are no more nodes, the search terminates, and we conclude that the string is not present in the trie.

## Insertion

The insertion algorithm is similar to the search algorithm, except that when it reaches a node that does not match the next letter of the string to be inserted, it creates a new node with the label of the next letter and inserts it as a child of the current node.

![Trie-Insert](https://i.imgur.com/TGiukHr.png)

For example, consider the trie shown in the figure above, and suppose we want to insert the string “cat”. The insertion algorithm starts at the root node, which is labeled with the letter ‘a’. Since this matches the first letter of the string, it moves to the child node, which is labeled with the letter ‘c’. Since this also matches the second letter of the string, it moves to the child node, which is labeled with the letter ‘a’. Since this does not match the third letter of the string, it creates a new node with the label ‘t’ and inserts it as a child of the current node.

## Deletion

The deletion algorithm is similar to the insertion algorithm, except that when it reaches a node that does not match the next letter of the string to be deleted, it deletes the node and all its descendants.

![Trie-Delete](https://i.imgur.com/vALDKdR.png)

For example, consider the trie shown in the figure above, and suppose we want to delete the string “cat”. The deletion algorithm starts at the root node, which is labeled with the letter ‘a’. Since this matches the first letter of the string, it moves to the child node, which is labeled with the letter ‘c’. Since this also matches the second letter of the string, it moves to the child node, which is labeled with the letter ‘a’. Since this does not match the third letter of the string, it deletes the node and all its descendants.

## Implementation

The trie data structure can be implemented using a linked list or an array.

### Linked List

A linked list is a data structure that consists of a set of nodes, each of which contains a reference to the next node in the list.

![Trie-LinkedList](https://i.imgur.com/rYUjg9O.png)

Each node in the list contains two fields:

-   The first field is the label of the node, which is a single character.
-   The second field is a reference to the next node in the list.

The first node in the list is called the head node, and the last node in the list is called the tail node.

The linked list implementation of the trie is very simple. To search for a string, we start at the head node, and for each character in the string, we follow the reference to the next node until we reach the tail node. If the string is not present in the trie, then the search will reach the tail node before it reaches the end of the string.

To insert a string, we start at the head node, and for each character in the string, we follow the reference to the next node until we reach the tail node. If the string is not present in the trie, then the insertion will reach the tail node before it reaches the end of the string, and at that point it will insert a new node with the label of the next character and update the reference of the tail node to point to the new node.

To delete a string, we start at the head node, and for each character in the string, we follow the reference to the next node until we reach the tail node. If the string is not present in the trie, then the deletion will reach the tail node before it reaches the end of the string. If the string is present in the trie, then the deletion will reach the end of the string, and at that point it will delete the node and all its descendants.

### Array

An array is a data structure that consists of a set of elements, each of which is identified by an index.

![Trie-Array](https://i.imgur.com/kzKVLCc.png)

In the array implementation of the trie, each node in the trie is represented by an array of size 26, where each element of the array is a reference to the next node in the trie. The array is indexed by the characters in the alphabet, so that the index of the character ‘a’ is 0, the index of the character ‘b’ is 1, and so on.

To search for a string, we start at the root node, and for each character in the string, we follow the reference to the next node. If the string is not present in the trie, then the search will reach a null node before it reaches the end of the string.

To insert a string, we start at the root node, and for each character in the string, we follow the reference to the next node. If the string is not present in the trie, then the insertion will reach a null node before it reaches the end of the string, and at that point it will insert a new node and update the reference of the node.

To delete a string, we start at the root node, and for each character in the string, we follow the reference to the next node. If the string is not present in the trie, then the deletion will reach a null node before it reaches the end of the string. If the string is present in the trie, then the deletion will reach the end of the string, and at that point it will delete the node and all its descendants.

## Applications

The trie data structure is used in many applications, such as spell checkers, word games, and data compression.

The spell checker application uses a trie to store a dictionary of words, and the search algorithm is used to check whether a given word is in the dictionary.

The word game application uses a trie to store the words in the game, and the search algorithm is used to find all the words that can be formed from a given set of letters.

The data compression application uses a trie to store a dictionary of words, and the search algorithm is used to find the longest word in the dictionary that is a prefix of a given string. The length of the longest word is then used to encode the string.

## Exercises

1.  Implement the trie data structure using a linked list.

2.  Implement the trie data structure using an array.

3.  Use the trie data structure to store a dictionary of words, and implement a spell checker application that uses the search algorithm to check whether a given word is in the dictionary.

4.  Use the trie data structure to store the words in a word game, and implement the search algorithm to find all the words that can be formed from a given set of letters.

5.  Use the trie data structure to store a dictionary of words, and implement the search algorithm to find the longest word in the dictionary that is a prefix of a given string.