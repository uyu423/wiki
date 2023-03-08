---
title: [JavaScript] 018：跳过列表
description: 
published: true
date: 2023-02-09T20:32:39.950Z
tags: 
editor: markdown
dateCreated: 2023-02-09T20:32:38.412Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 018: Skip List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-018-skip-list)
{.links-list}


# 跳过列表

跳跃列表是一种数据结构，允许在有序的元素序列中进行有效搜索。它是一种链表，采用节点的层次结构，每个节点都有多个“链接”到层次结构中不同级别的其他节点。 Pugh 在他 1990 年的论文“Skip Lists: A Probabilistic Alternative to Balanced Trees”中首次描述了这个跳跃列表。

跳跃列表是一种随机数据结构，这意味着节点链接在一起的顺序由随机数生成器确定。这种方法的优点是它允许在 O(n) 时间内构造跳跃列表，其中 n 是要插入列表的元素数。

跳跃列表有很多应用，包括数据库和文件系统。它也用于 Linux 内核的基数树数据结构。

## 跳跃列表如何工作

跳表由一系列级别组成，每个级别都有一组节点。第一层是最低层，最后一层是最高层。级别数由随机数生成器确定。

每个级别上的节点都按排序顺序链接在一起。最低层的节点按值递增的顺序连接在一起，较高层的节点按值递减的顺序连接在一起。

跳过列表还有一个“头”节点，它是最低层的第一个节点。头节点有一个指向上一层的第一个节点的指针。如果上一层没有节点，则头节点的指针将为空。

跳过列表中的每个节点都有一个“值”字段和一个“级别”字段。 value字段存储节点的值，level字段存储节点的级别。

节点的级别由随机数生成器决定。节点将被分配到级别 i 的概率是 1/(2^i)。这意味着一个节点被分配到最高级别的机会是 1/2，一个节点被分配到第二高级别的机会是 1/4，依此类推。

通过从头节点开始并跟随指向同一级别下一个节点的指针来搜索跳过列表。如果下一个结点的值小于要查找的值，则指针指向下一个同级结点。重复此过程，直到到达一个值大于或等于正在搜索的值的节点。此时，搜索跟随指针指向下一层的下一个节点并重复该过程。

如果要搜索的值未在跳过列表中找到，则搜索返回 null。

## 代码示例

这是跳跃列表的简单 Java 实现。 “SkipList”类代表一个跳跃列表，“Node”类代表跳跃列表中的一个节点。

```java
public class SkipList {
    
    private Node head;
    private int size;
    private Random random;
    
    public SkipList() {
        head = new Node(Integer.MIN_VALUE);
        size = 0;
        random = new Random();
    }
    
    public void insert(int value) {
        Node node = new Node(value);
        Node current = head;
        while (current.value < value) {
            current = current.next;
        }
        node.next = current.next;
        current.next = node;
        size++;
    }
    
    public boolean contains(int value) {
        Node current = head;
        while (current.value < value) {
            current = current.next;
        }
        return current.value == value;
    }
    
    public int size() {
        return size;
    }
    
    private class Node {
        int value;
        Node next;
        
        public Node(int value) {
            this.value = value;
        }
    }
    
}
```

## 练习

1.实现SkipList类的“insert”和“contains”方法。

2.修改SkipList类，使用双向链表代替单向链表。

3. 修改SkipList 类以跟踪每一层的节点数。

4. 修改 SkipList 类以允许自定义比较器用于对列表中的元素进行排序。

5. 修改 SkipList 类以允许使用自定义哈希函数对列表中的元素进行哈希处理。