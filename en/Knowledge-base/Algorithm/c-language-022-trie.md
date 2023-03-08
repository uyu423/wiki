---
title: [C Language] 022: Trie
description: 
published: true
date: 2023-02-11T00:17:34.045Z
tags: 
editor: markdown
dateCreated: 2023-02-11T00:17:27.440Z
---

- [[Lenguaje C] 022: Triángulo***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-022-trie)
{.links-list}
- [【C语言】022：特里树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-022-trie)
{.links-list}
- [[C언어] 022: 트라이***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-022-trie)
{.links-list}


# 022: Trie

A trie is a tree-like data structure that is used to store a dynamic set or associative array where the keys are usually strings. Unlike a binary search tree, no node in the tree stores the key associated with that node; instead, its position in the tree defines the key with which it is associated. All the descendants of a node have a common prefix of the string associated with that node, and the root is associated with the empty string. Values are not necessarily associated with every node. Rather, values tend to be associated with leaves, and with some inner nodes that correspond to keys of interest.

![Trie](https://upload.wikimedia.org/wikipedia/commons/b/be/Trie_example.svg)

In the example image, keys are listed in the nodes and values below them. Each complete English word has an asterisk below it. Here, the trie stores a set of English words. The keys are the letters in the words, and the values are the words themselves.

## Code Example

```c
#include <stdio.h> 
#include <stdlib.h> 
#include <string.h> 
#include <stdbool.h> 

#define ARRAY_SIZE(a) sizeof(a)/sizeof(a[0]) 
#define CHAR_TO_INDEX(c) ((int)c - (int)'a') 

// Alphabet size (# of symbols) 
#define ALPHABET_SIZE (26) 

// Converts key current character into index 
// use only 'a' through 'z' and lower case 
#define CHAR_TO_INDEX(c) ((int)c - (int)'a') 

// trie node 
struct TrieNode 
{ 
	struct TrieNode *children[ALPHABET_SIZE]; 

	// isEndOfWord is true if the node represents 
	// end of a word 
	bool isEndOfWord; 
}; 

// Returns new trie node (initialized to NULLs) 
struct TrieNode *getNode(void) 
{ 
	struct TrieNode *pNode = NULL; 

	pNode = (struct TrieNode *)malloc(sizeof(struct TrieNode)); 

	if (pNode) 
	{ 
		int i; 

		pNode->isEndOfWord = false; 

		for (i = 0; i < ALPHABET_SIZE; i++) 
			pNode->children[i] = NULL; 
	} 

	return pNode; 
} 

// If not present, inserts key into trie 
// If the key is prefix of trie node, just marks leaf node 
void insert(struct TrieNode *root, const char *key) 
{ 
	int level; 
	int length = strlen(key); 
	int index; 

	struct TrieNode *pCrawl = root; 

	for (level = 0; level < length; level++) 
	{ 
		index = CHAR_TO_INDEX(key[level]); 
		if (!pCrawl->children[index]) 
			pCrawl->children[index] = getNode(); 

		pCrawl = pCrawl->children[index]; 
	} 

	// mark last node as leaf 
	pCrawl->isEndOfWord = true; 
} 

// Returns true if key presents in trie, else false 
bool search(struct TrieNode *root, const char *key) 
{ 
	int level; 
	int length = strlen(key); 
	int index; 
	struct TrieNode *pCrawl = root; 

	for (level = 0; level < length; level++) 
	{ 
		index = CHAR_TO_INDEX(key[level]); 

		if (!pCrawl->children[index]) 
			return false; 

		pCrawl = pCrawl->children[index]; 
	} 

	return (pCrawl != NULL && pCrawl->isEndOfWord); 
} 

// Driver 
int main() 
{ 
	// Input keys (use only 'a' through 'z' and lower case) 
	char keys[][8] = {"the", "a", "there", "answer", "any", "by", "bye", "their"}; 

	char output[][32] = {"Not present in trie", "Present in trie"}; 


	struct TrieNode *root = getNode(); 

	// Construct trie 
	int i; 
	for (i = 0; i < ARRAY_SIZE(keys); i++) 
		insert(root, keys[i]); 

	// Search for different keys 
	printf("%s --- %s\n", "the", output[search(root, "the")] ); 
	printf("%s --- %s\n", "these", output[search(root, "these")] ); 
	printf("%s --- %s\n", "their", output[search(root, "their")] ); 
	printf("%s --- %s\n", "thaw", output[search(root, "thaw")] ); 

	return 0; 
} 
```

## Explanation

In the above code example, we have implemented a trie in the C programming language. The code includes a function to insert keys into the trie, and a function to search the trie for a given key.

We have also defined a struct to represent a trie node. Each node has an array of pointers to child nodes (one for each letter of the alphabet), and a boolean flag to indicate whether the node represents the end of a word.

The insert function takes a root node and a key as input, and inserts the key into the trie. If the key is already present in the trie, the function does nothing.

The search function takes a root node and a key as input, and returns true if the key is present in the trie, and false otherwise.

## Applications

Tries are often used for storing strings that are used frequently, such as words in a dictionary. They are also used for storing strings that share a common prefix, such as DNA sequences.

Tries can also be used for storing non-string keys, such as integers. In this case, each node would store a number instead of a letter, and the keys would be stored in the order in which they appear in the sequence.

## Exercises

1. Implement a function to delete a key from a trie.

2. Implement a function to find the shortest unique prefix of a given key.

3. Implement a function to find the longest common prefix of a set of keys.

4. Implement a function to check if a given string is a valid word in a given trie.