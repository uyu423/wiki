---
title: [C언어] 046: 트라이
description: 
published: true
date: 2023-02-13T19:56:14.223Z
tags: 
editor: markdown
dateCreated: 2023-02-13T19:56:12.646Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 046: Trie***English** document is available*](/en/Knowledge-base/Algorithm/c-language-046-trie)
{.links-list}


# 046: 트라이

디지털 트리 또는 접두사 트리라고도 하는 트리는 키가 일반적으로 문자열인 동적 집합 또는 연관 배열을 저장하는 데 사용되는 정렬된 트리 데이터 구조입니다. 이진 검색 트리와 달리 트리의 어떤 노드도 해당 노드와 관련된 키를 저장하지 않습니다. 대신 트리에서 해당 위치는 연결된 키를 정의합니다. 노드의 모든 자손은 해당 노드와 연결된 문자열의 공통 접두사를 가지며 루트는 빈 문자열과 연결됩니다. 값이 반드시 모든 노드와 연관되는 것은 아닙니다. 오히려 값은 리프 및 관심 키에 해당하는 일부 내부 노드와 연결되는 경향이 있습니다.

## 개념

트리는 문자열을 저장하는 트리와 같은 데이터 구조로 볼 수 있습니다. 트라이에서 각 노드는 여러 자식을 가질 수 있습니다. 트리의 각 노드는 문자를 저장하고 문자열은 루트에서 특정 노드로 이동하여 형성됩니다.

![Trie](https://upload.wikimedia.org/wikipedia/commons/b/be/Trie_example.svg)

위의 예에서 루트 노드는 빈 문자열로 표시되고 각 노드는 루트에서 해당 노드까지의 경로에 있는 문자를 연결하여 형성된 문자열을 나타냅니다. 리프는 트리에서 다른 문자열의 접두사가 아닌 문자열을 나타내는 노드입니다. 이 예에서는 문자열 "to", "tea", "ted", "ten", "i", "in" 및 "inn"이 저장됩니다.

## 코드 예

다음은 C에서 트라이를 간단하게 구현한 것입니다.

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

## 운동

1. 문자열을 받아 트리에 삽입하는 함수를 구현합니다.

2. 문자열을 받아 트리에서 검색하는 함수를 구현합니다.

3. 문자열을 받아 트라이에서 발생하는 횟수를 반환하는 함수를 구현합니다.

4. 문자열을 받아 해당 문자열로 시작하는 트라이에서 단어 수를 반환하는 함수를 구현합니다.

## 응답 코드

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

삼.

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

## 해설

시도는 문자열을 저장하는 매우 효율적인 방법입니다. 맞춤법 검사기, 자동 완성 제안 및 IP 라우팅과 같은 많은 애플리케이션에서 사용됩니다.