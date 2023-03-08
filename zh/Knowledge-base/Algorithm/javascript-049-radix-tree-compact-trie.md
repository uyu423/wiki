---
title: [JavaScript] 049：基数树（Compact Trie）
description: 
published: true
date: 2023-02-11T03:32:26.674Z
tags: 
editor: markdown
dateCreated: 2023-02-11T03:32:20.146Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 049: Radix Tree (Compact Trie)***English** document is available*](/en/Knowledge-base/Algorithm/javascript-049-radix-tree-compact-trie)
{.links-list}


# 基数树（Compact Trie）

基数树，也称为紧凑型特里树，是一种节省空间的数据结构，用于存储字符串。它类似于 trie，但不是将每个字符存储在一个节点中，而是将每个字符存储在一条边中。这使得基数树比 trie 占用更少的空间。

基数树通常用于存储太长而无法放入传统 trie 中的字符串。它们还用于存储经常访问的字符串，例如在字典中。

## 怎么运行的

基数树是一种存储字符串的树状数据结构。基数树中的每个节点代表字符串中的一个字符。节点之间的边表示字符串中彼此相邻的字符。

基数树类似于 trie，但它不是将每个字符存储在一个节点中，而是将每个字符存储在一条边中。这使得基数树比 trie 占用更少的空间。

在搜索字符串时，基数树也比特里树更有效。 trie 必须搜索树中的所有节点才能找到字符串，而基数树可以在到达与字符串不匹配的节点时立即停止搜索。

## 代码示例

这是 JavaScript 中基数树的简单实现。

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

## 相关练习

- [基数树练习](https://repl.it/@jimt/Radix-Tree-Exercise)
- [紧凑型 Trie 练习](https://repl.it/@jimt/Compact-Trie-Exercise)

## 结论

基数树是一种节省空间的数据结构，用于存储字符串。它们类似于尝试，但它们将每个字符存储在边而不是节点中。这使得基数树比 trie 占用更少的空间。

基数树通常用于存储太长而无法放入传统 trie 中的字符串。它们还用于存储经常访问的字符串，例如在字典中。