---
title: [C Language] 046: Trie
description: 
published: true
date: 2023-02-13T19:56:19.730Z
tags: 
editor: markdown
dateCreated: 2023-02-13T19:56:12.651Z
---

- [[Lenguaje C] 046: Trio***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-046-trie)
{.links-list}
- [【C语言】046：特里树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-046-trie)
{.links-list}
- [[C언어] 046: 트라이***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-046-trie)
{.links-list}


# 046: Trie

A trie, also called a digital tree or prefix tree, is an ordered tree data structure that is used to store a dynamic set or associative array where the keys are usually strings. Unlike a binary search tree, no node in the tree stores the key associated with that node; instead, its position in the tree defines the key with which it is associated. All the descendants of a node have a common prefix of the string associated with that node, and the root is associated with the empty string. Values are not necessarily associated with every node. Rather, values tend to be associated with leaves, and with some inner nodes that correspond to keys of interest.

## Concept

A trie can be seen as a tree-like data structure that stores strings. In a trie, each node can have multiple children. Each node in a trie stores a character, and strings are formed by traversing from the root to a particular node.

![Trie](https://upload.wikimedia.org/wikipedia/commons/b/be/Trie_example.svg)

In the above example, the root node is represented by the empty string, and each node represents a string formed by concatenating the characters on the path from the root to that node. The leaves are the nodes that represent strings that are not prefixes of any other string in the trie. In this example, the strings "to", "tea", "ted", "ten", "i", "in", and "inn" are stored.

## Code Example

Here is a simple implementation of a trie in C.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define ALPHABET_SIZE 26

// A node in the trie
struct TrieNode
{
    // The children of this node
    struct TrieNode *children[ALPHABET_SIZE];

    // Is this the end of a word?
    int is_end_of_word;
};

// Returns a new TrieNode
struct TrieNode *get_node(void)
{
    struct TrieNode *p_node = (struct TrieNode *)malloc(sizeof(struct TrieNode));

    if (p_node)
    {
        int i;

        p_node->is_end_of_word = 0;

        for (i = 0; i < ALPHABET_SIZE; i++)
            p_node->children[i] = NULL;
    }

    return p_node;
}

// Inserts a word into the trie
void insert(struct TrieNode *root, const char *key)
{
    int level;
    int length = strlen(key);
    int index;

    struct TrieNode *p_crawl = root;

    for (level = 0; level < length; level++)
    {
        index = CHAR_TO_INDEX(key[level]);

        if (!p_crawl->children[index])
            p_crawl->children[index] = get_node();

        p_crawl = p_crawl->children[index];
    }

    // Mark the last node as leaf
    p_crawl->is_end_of_word = 1;
}

// Searches a word in the trie
int search(struct TrieNode *root, const char *key)
{
    int level;
    int length = strlen(key);
    int index;
    struct TrieNode *p_crawl = root;

    for (level = 0; level < length; level++)
    {
        index = CHAR_TO_INDEX(key[level]);

        if (!p_crawl->children[index])
            return 0;

        p_crawl = p_crawl->children[index];
    }

    return (p_crawl != NULL && p_crawl->is_end_of_word);
}

// Driver
int main()
{
    // Input keys (use only 'a' through 'z' and lower case)
    char keys[][8] = {"the", "a", "there", "answer", "any", "by", "bye", "their"};
    int n = sizeof(keys) / sizeof(keys[0]);

    struct TrieNode *root = get_node();

    // Construct trie
    int i;
    for (i = 0; i < n; i++)
        insert(root, keys[i]);

    // Search for different keys
    search(root, "the") ? printf("Yes\n") : printf("No\n");
    search(root, "these") ? printf("Yes\n") : printf("No\n");
    search(root, "their") ? printf("Yes\n") : printf("No\n");
    search(root, "thaw") ? printf("Yes\n") : printf("No\n");

    return 0;
}
```

## Exercise

1. Implement a function that takes a string and inserts it into a trie.

2. Implement a function that takes a string and searches for it in a trie.

3. Implement a function that takes a string and returns the number of times it occurs in a trie.

4. Implement a function that takes a string and returns the number of words in a trie that start with that string.

## Answer Code

1. 

```c
void insert(struct TrieNode *root, const char *key)
{
    int level;
    int length = strlen(key);
    int index;

    struct TrieNode *p_crawl = root;

    for (level = 0; level < length; level++)
    {
        index = CHAR_TO_INDEX(key[level]);

        if (!p_crawl->children[index])
            p_crawl->children[index] = get_node();

        p_crawl = p_crawl->children[index];
    }

    // Mark the last node as leaf
    p_crawl->is_end_of_word = 1;
}
```

2. 

```c
int search(struct TrieNode *root, const char *key)
{
    int level;
    int length = strlen(key);
    int index;
    struct TrieNode *p_crawl = root;

    for (level = 0; level < length; level++)
    {
        index = CHAR_TO_INDEX(key[level]);

        if (!p_crawl->children[index])
            return 0;

        p_crawl = p_crawl->children[index];
    }

    return (p_crawl != NULL && p_crawl->is_end_of_word);
}
```

3. 

```c
int search(struct TrieNode *root, const char *key)
{
    int level;
    int length = strlen(key);
    int index;
    struct TrieNode *p_crawl = root;

    for (level = 0; level < length; level++)
    {
        index = CHAR_TO_INDEX(key[level]);

        if (!p_crawl->children[index])
            return 0;

        p_crawl = p_crawl->children[index];
    }

    return (p_crawl != NULL && p_crawl->is_end_of_word);
}
```

4. 

```c
int starts_with(struct TrieNode *root, const char *key)
{
    int level;
    int length = strlen(key);
    int index;
    struct TrieNode *p_crawl = root;

    for (level = 0; level < length; level++)
    {
        index = CHAR_TO_INDEX(key[level]);

        if (!p_crawl->children[index])
            return 0;

        p_crawl = p_crawl->children[index];
    }

    return 1;
}
```

## Commentary

Tries are a very efficient way of storing strings. They are used in many applications, such as spell checkers, autocomplete suggestions, and IP routing.