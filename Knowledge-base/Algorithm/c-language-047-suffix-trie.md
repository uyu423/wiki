---
title: [ C언어 ] 047 : 접미사 트라이
description: 
published: true
date: 2023-02-14T00:32:25.173Z
tags: 
editor: markdown
dateCreated: 2023-02-14T00:32:23.589Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 047: Suffix Trie***English** document is available*](/en/Knowledge-base/Algorithm/c-language-047-suffix-trie)
{.links-list}


# 047: 접미사 트라이

## Suffix Trie란?

접미사 트라이는 주어진 텍스트의 접미사만 노드에 키로 저장하는 일종의 압축 트라이입니다. 주어진 패턴의 모든 항목을 찾거나 가장 긴 반복 하위 문자열을 찾는 것과 같은 빠른 패턴 일치 알고리즘을 가능하게 하는 공간 효율적인 데이터 구조입니다.

## 어떻게 작동하나요?

접미사 트라이를 구축하려면 먼저 텍스트에 대한 트라이를 구성해야 합니다. 그런 다음 자식이 하나만 있는 모든 노드를 제거하여 트라이를 압축할 수 있습니다.

결과 데이터 구조를 접미사 트리라고 합니다. 트라이와 동일한 검색 시간 복잡도를 갖지만 공간을 덜 사용합니다.

## 코드 예

다음은 C++에서 접미사 트리를 간단하게 구현한 것입니다.

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

## 관련 연습

1. 문자열을 받아 이에 대한 접미사 트라이를 구축하는 함수를 구현합니다.

2. 문자열과 패턴을 취하고 패턴이 발생하는 문자열의 모든 시작 인덱스 목록을 반환하는 함수를 구현합니다.

3. 문자열을 가져와서 가장 길게 반복되는 하위 문자열을 반환하는 함수를 구현합니다.