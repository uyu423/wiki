---
title: [JavaScript] 049: Radix Tree (Compact Trie)
description: 
published: true
date: 2023-02-11T03:32:21.792Z
tags: 
editor: markdown
dateCreated: 2023-02-11T03:32:20.152Z
---

- [[JavaScript] 049: Árbol Radix (Trie compacto)***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-049-radix-tree-compact-trie)
{.links-list}
- [[JavaScript] 049：基数树（Compact Trie）***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-049-radix-tree-compact-trie)
{.links-list}
- [[JavaScript] 049: 기수 트리(Compact Trie)***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-049-radix-tree-compact-trie)
{.links-list}


# Radix Tree (Compact Trie)

A radix tree, also known as a compact trie, is a space-efficient data structure that is used to store strings. It is similar to a trie, but instead of storing each character in a node, it stores each character in an edge. This allows the radix tree to take up less space than a trie.

Radix trees are often used to store strings that are too long to fit in a traditional trie. They are also used to store strings that are frequently accessed, such as in a dictionary.

## How it works

A radix tree is a tree-like data structure that stores strings. Each node in the radix tree represents a character in the string. The edges between nodes represent the characters that are adjacent to each other in the string.

The radix tree is similar to a trie, but instead of storing each character in a node, it stores each character in an edge. This allows the radix tree to take up less space than a trie.

The radix tree is also more efficient than a trie when it comes to searching for strings. A trie must search through all of the nodes in the tree to find a string, while a radix tree can stop searching as soon as it reaches a node that does not match the string.

## Code example

Here is a simple implementation of a radix tree in JavaScript.

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

## Related exercises

- [Radix Tree Exercise](https://repl.it/@jimt/Radix-Tree-Exercise)
- [Compact Trie Exercise](https://repl.it/@jimt/Compact-Trie-Exercise)

## Conclusion

Radix trees are a space-efficient data structure that is used to store strings. They are similar to tries, but they store each character in an edge instead of a node. This allows the radix tree to take up less space than a trie.

Radix trees are often used to store strings that are too long to fit in a traditional trie. They are also used to store strings that are frequently accessed, such as in a dictionary.