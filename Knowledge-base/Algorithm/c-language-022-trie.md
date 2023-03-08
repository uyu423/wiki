---
title: [C언어] 022: 트라이
description: 
published: true
date: 2023-02-11T00:17:29.073Z
tags: 
editor: markdown
dateCreated: 2023-02-11T00:17:27.433Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 022: Trie***English** document is available*](/en/Knowledge-base/Algorithm/c-language-022-trie)
{.links-list}


# 022: 트라이

트리는 키가 일반적으로 문자열인 동적 집합 또는 연관 배열을 저장하는 데 사용되는 트리와 유사한 데이터 구조입니다. 이진 검색 트리와 달리 트리의 어떤 노드도 해당 노드와 관련된 키를 저장하지 않습니다. 대신 트리에서 해당 위치는 연결된 키를 정의합니다. 노드의 모든 자손은 해당 노드와 연결된 문자열의 공통 접두사를 가지며 루트는 빈 문자열과 연결됩니다. 값이 반드시 모든 노드와 연관되는 것은 아닙니다. 오히려 값은 리프 및 관심 키에 해당하는 일부 내부 노드와 연결되는 경향이 있습니다.

![Trie](https://upload.wikimedia.org/wikipedia/commons/b/be/Trie_example.svg)

예제 이미지에서 키는 노드와 그 아래의 값에 나열됩니다. 각 완전한 영어 단어 아래에는 별표가 있습니다. 여기에서 trie는 영어 단어 세트를 저장합니다. 키는 단어의 문자이고 값은 단어 자체입니다.

## 코드 예

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

## 설명

위의 코드 예제에서는 C 프로그래밍 언어로 트라이를 구현했습니다. 코드에는 trie에 키를 삽입하는 기능과 주어진 키에 대해 trie를 검색하는 기능이 포함되어 있습니다.

트리 노드를 나타내는 구조체도 정의했습니다. 각 노드에는 자식 노드에 대한 포인터 배열(알파벳 문자마다 하나씩)과 노드가 단어의 끝을 나타내는지 여부를 나타내는 부울 플래그가 있습니다.

삽입 기능은 루트 노드와 키를 입력으로 받아 트리에 키를 삽입합니다. 키가 트라이에 이미 있는 경우 함수는 아무 작업도 수행하지 않습니다.

검색 기능은 루트 노드와 키를 입력으로 사용하고 키가 트리에 있으면 true를 반환하고 그렇지 않으면 false를 반환합니다.

## 애플리케이션

시도는 사전의 단어와 같이 자주 사용되는 문자열을 저장하는 데 자주 사용됩니다. 또한 DNA 시퀀스와 같은 공통 접두사를 공유하는 문자열을 저장하는 데 사용됩니다.

시도는 정수와 같은 문자열이 아닌 키를 저장하는 데에도 사용할 수 있습니다. 이 경우 각 노드는 문자 대신 숫자를 저장하고 키는 시퀀스에 나타나는 순서대로 저장됩니다.

## 운동

1. 트라이에서 키를 삭제하는 기능을 구현합니다.

2. 주어진 키의 가장 짧은 고유 접두사를 찾는 함수를 구현합니다.

3. 키 집합의 가장 긴 공통 접두사를 찾는 함수를 구현합니다.

4. 주어진 문자열이 주어진 트라이에서 유효한 단어인지 확인하는 함수를 구현합니다.