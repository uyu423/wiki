---
title: [C Language] 047: Suffix Trie
description: 
published: true
date: 2023-02-14T00:32:30.805Z
tags: 
editor: markdown
dateCreated: 2023-02-14T00:32:23.598Z
---

- [[Lenguaje C] 047: Sufijo Trie***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-047-suffix-trie)
{.links-list}
- [[C语言]047：后缀特里树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-047-suffix-trie)
{.links-list}
- [[ C언어 ] 047 : 접미사 트라이***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-047-suffix-trie)
{.links-list}


# 047: Suffix Trie

## What is a Suffix Trie?

A suffix trie is a kind of compressed trie where only the suffixes of a given text are stored as the keys at the nodes. It is a space-efficient data structure that enables fast pattern matching algorithms such as those for finding all occurrences of a given pattern or for finding the longest repeated substring.

## How does it work?

To build a suffix trie, we first need to construct a trie for the text. We can then compress the trie by removing all the nodes that have only one child.

The resulting data structure is called a suffix trie. It has the same search time complexity as a trie, but uses less space.

## Code Example

Here is a simple implementation of a suffix trie in C++.

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

## Related Exercises

1. Implement a function that takes a string and builds a suffix trie for it.

2. Implement a function that takes a string and a pattern, and returns the list of all starting indices in the string where the pattern occurs.

3. Implement a function that takes a string and returns the longest repeated substring in it.