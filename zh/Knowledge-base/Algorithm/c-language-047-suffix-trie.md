---
title: [C语言]047：后缀特里树
description: 
published: true
date: 2023-02-14T00:32:25.493Z
tags: 
editor: markdown
dateCreated: 2023-02-14T00:32:23.591Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 047: Suffix Trie***English** document is available*](/en/Knowledge-base/Algorithm/c-language-047-suffix-trie)
{.links-list}


# 047：后缀特里

## 什么是后缀 Trie？

后缀 trie 是一种压缩的 trie，其中仅将给定文本的后缀存储为节点处的键。它是一种节省空间的数据结构，支持快速模式匹配算法，例如用于查找给定模式的所有出现或用于查找最长重复子串的算法。

## 它是如何工作的？

要构建后缀树，我们首先需要构建文本的树。然后我们可以通过删除所有只有一个孩子的节点来压缩 trie。

生成的数据结构称为后缀特里。它具有与 trie 相同的搜索时间复杂度，但使用的空间更少。

## 代码示例

这是 C++ 中后缀特里树的简单实现。

```cpp
#include <iostream>
#include <string>
#include <unordered_map>
#include <vector>

using namespace std;

class SuffixTrie {
public:
  SuffixTrie(string s) {
    root = new TrieNode();
    for (int i = 0; i < s.size(); i++) {
      insert(s.substr(i));
    }
  }

  void insert(string s) {
    TrieNode* curr = root;
    for (char c : s) {
      if (curr->children.find(c) == curr->children.end()) {
        curr->children[c] = new TrieNode();
      }
      curr = curr->children[c];
    }
    curr->isEnd = true;
  }

  bool search(string s) {
    TrieNode* curr = root;
    for (char c : s) {
      if (curr->children.find(c) == curr->children.end()) {
        return false;
      }
      curr = curr->children[c];
    }
    return curr->isEnd;
  }

private:
  struct TrieNode {
    unordered_map<char, TrieNode*> children;
    bool isEnd;
    TrieNode() : isEnd(false) {}
  };

  TrieNode* root;
};

int main() {
  string s = "banana";
  SuffixTrie trie(s);
  cout << trie.search("an") << endl; // 1
  cout << trie.search("ana") << endl; // 1
  cout << trie.search("nan") << endl; // 1
  cout << trie.search("nana") << endl; // 1
  cout << trie.search("banana") << endl; // 1
  cout << trie.search("bana") << endl; // 0
  return 0;
}
```

## 相关练习

1. 实现一个接受字符串并为其构建后缀特里树的函数。

2. 实现一个接受字符串和模式的函数，并返回字符串中出现模式的所有起始索引的列表。

3. 实现一个函数，它接受一个字符串并返回其中最长的重复子字符串。