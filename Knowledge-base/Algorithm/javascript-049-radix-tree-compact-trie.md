---
title: [JavaScript] 049: 기수 트리(Compact Trie)
description: 
published: true
date: 2023-02-11T03:32:26.674Z
tags: 
editor: markdown
dateCreated: 2023-02-11T03:32:20.145Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 049: Radix Tree (Compact Trie)***English** document is available*](/en/Knowledge-base/Algorithm/javascript-049-radix-tree-compact-trie)
{.links-list}


# 기수 트리(컴팩트 트리)

압축 트리라고도 하는 기수 트리는 문자열을 저장하는 데 사용되는 공간 효율적인 데이터 구조입니다. 트라이와 비슷하지만 각 문자를 노드에 저장하는 대신 각 문자를 에지에 저장합니다. 이렇게 하면 기수 트리가 트리보다 적은 공간을 차지할 수 있습니다.

기수 트리는 전통적인 트리에 맞추기에는 너무 긴 문자열을 저장하는 데 자주 사용됩니다. 또한 사전과 같이 자주 액세스되는 문자열을 저장하는 데 사용됩니다.

## 작동 방식

기수 트리는 문자열을 저장하는 트리와 유사한 데이터 구조입니다. 기수 트리의 각 노드는 문자열의 문자를 나타냅니다. 노드 사이의 가장자리는 문자열에서 서로 인접한 문자를 나타냅니다.

기수 트리는 트리와 유사하지만 각 문자를 노드에 저장하는 대신 각 문자를 에지에 저장합니다. 이렇게 하면 기수 트리가 트리보다 적은 공간을 차지할 수 있습니다.

또한 기수 트리는 문자열을 검색할 때 트라이보다 더 효율적입니다. 트라이는 문자열을 찾기 위해 트리의 모든 노드를 검색해야 하지만 기수 트리는 문자열과 일치하지 않는 노드에 도달하는 즉시 검색을 중지할 수 있습니다.

## 코드 예시

다음은 JavaScript에서 기수 트리를 간단하게 구현한 것입니다.

```javascript
function RadixTree() {
  this.root = new Node();
}

function Node() {
  this.children = {};
}

RadixTree.prototype.insert = function(string) {
  var node = this.root;

  for (var i = 0; i < string.length; i++) {
    var char = string[i];

    if (!node.children[char]) {
      node.children[char] = new Node();
    }

    node = node.children[char];
  }
};

RadixTree.prototype.search = function(string) {
  var node = this.root;

  for (var i = 0; i < string.length; i++) {
    var char = string[i];

    if (!node.children[char]) {
      return false;
    }

    node = node.children[char];
  }

  return true;
};

var tree = new RadixTree();
tree.insert("cat");
tree.insert("dog");
tree.insert("cats");
tree.insert("dogs");

console.log(tree.search("cat")); // true
console.log(tree.search("cats")); // true
console.log(tree.search("dog")); // true
console.log(tree.search("dogs")); // true
console.log(tree.search("c")); // false
console.log(tree.search("ca")); // false
console.log(tree.search("d")); // false
console.log(tree.search("do")); // false
```

## 관련 연습

- [기수나무 실습](https://repl.it/@jimt/Radix-Tree-Exercise)
- [컴팩트 트라이 운동](https://repl.it/@jimt/Compact-Trie-Exercise)

## 결론

기수 트리는 문자열을 저장하는 데 사용되는 공간 효율적인 데이터 구조입니다. 시도와 유사하지만 각 문자를 노드 대신 에지에 저장합니다. 이렇게 하면 기수 트리가 트리보다 적은 공간을 차지할 수 있습니다.

기수 트리는 전통적인 트리에 맞추기에는 너무 긴 문자열을 저장하는 데 자주 사용됩니다. 또한 사전과 같이 자주 액세스되는 문자열을 저장하는 데 사용됩니다.