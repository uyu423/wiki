---
title: 【C语言】022：特里树
description: 
published: true
date: 2023-02-11T00:17:29.267Z
tags: 
editor: markdown
dateCreated: 2023-02-11T00:17:27.433Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 022: Trie***English** document is available*](/en/Knowledge-base/Algorithm/c-language-022-trie)
{.links-list}


# 022：特里

trie 是一种树状数据结构，用于存储动态集或关联数组，其中键通常是字符串。与二叉搜索树不同，树中没有节点存储与该节点关联的键；相反，它在树中的位置定义了与其关联的键。一个节点的所有后代都有一个与该节点关联的字符串的公共前缀，并且根与空字符串关联。值不一定与每个节点相关联。相反，值往往与叶子相关联，并且与一些与感兴趣的键相对应的内部节点相关联。

![特里树](https://upload.wikimedia.org/wikipedia/commons/b/be/Trie_example.svg)

在示例图像中，键列在节点中，值列在它们下方。每个完整的英文单词下面都有一个星号。在这里，特里存储了一组英文单词。键是单词中的字母，值是单词本身。

## 代码示例

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

## 解释

在上面的代码示例中，我们用C编程语言实现了一个trie。该代码包括一个将键插入到 trie 中的函数，以及一个在 trie 中搜索给定键的函数。

我们还定义了一个结构来表示一个 trie 节点。每个节点都有一个指向子节点的指针数组（每个字母对应一个字母），以及一个布尔标志来指示该节点是否代表单词的结尾。

insert 函数将根节点和键作为输入，并将键插入到 trie 中。如果关键字已经存在于 trie 中，则该函数不执行任何操作。

搜索函数将根节点和键作为输入，如果键存在于 trie 中，则返回 true，否则返回 false。

## 应用

尝试通常用于存储经常使用的字符串，例如字典中的单词。它们还用于存储共享一个公共前缀的字符串，例如 DNA 序列。

尝试也可用于存储非字符串键，例如整数。在这种情况下，每个节点将存储一个数字而不是一个字母，并且键将按照它们在序列中出现的顺序存储。

## 练习

1. 实现一个从 trie 中删除键的函数。

2. 实现一个函数来查找给定键的最短唯一前缀。

3. 实现一个函数来查找一组键的最长公共前缀。

4. 实现一个函数来检查给定的字符串是否是给定的 trie 中的有效单词。