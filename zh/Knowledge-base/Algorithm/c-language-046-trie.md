---
title: 【C语言】046：特里树
description: 
published: true
date: 2023-02-13T19:56:14.360Z
tags: 
editor: markdown
dateCreated: 2023-02-13T19:56:12.646Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 046: Trie***English** document is available*](/en/Knowledge-base/Algorithm/c-language-046-trie)
{.links-list}


# 046：特里

trie，也称为数字树或前缀树，是一种有序树数据结构，用于存储动态集或关联数组，其中键通常是字符串。与二叉搜索树不同，树中没有节点存储与该节点关联的键；相反，它在树中的位置定义了与其关联的键。一个节点的所有后代都有一个与该节点关联的字符串的公共前缀，并且根与空字符串关联。值不一定与每个节点相关联。相反，值往往与叶子相关联，并且与一些与感兴趣的键相对应的内部节点相关联。

## 概念

trie 可以看作是一种存储字符串的树状数据结构。在 trie 中，每个节点可以有多个子节点。 trie 中的每个节点存储一个字符，字符串是通过从根遍历到特定节点形成的。

![特里树](https://upload.wikimedia.org/wikipedia/commons/b/be/Trie_example.svg)

在上面的示例中，根节点由空字符串表示，每个节点表示一个字符串，该字符串由从根节点到该节点的路径上的字符连接而成。叶子是代表字符串的节点，这些字符串不是 trie 中任何其他字符串的前缀。在此示例中，存储了字符串“to”、“tea”、“ted”、“ten”、“i”、“in”和“inn”。

## 代码示例

这是 C 中 trie 的简单实现。

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

## 锻炼

1. 实现一个接受字符串并将其插入到树中的函数。

2. 实现一个接受字符串并在 trie 中搜索它的函数。

3. 实现一个函数，它接受一个字符串并返回它在 trie 中出现的次数。

4. 实现一个函数，它接受一个字符串并返回 trie 中以该字符串开头的单词数。

## 答案代码

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

## 评论

尝试是一种非常有效的字符串存储方式。它们用于许多应用程序，例如拼写检查器、自动完成建议和 IP 路由。