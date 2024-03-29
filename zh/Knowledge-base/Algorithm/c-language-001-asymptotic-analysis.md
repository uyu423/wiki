---
title: 【C语言】001：渐近分析
description: 
published: true
date: 2023-02-12T13:32:23.225Z
tags: 
editor: markdown
dateCreated: 2023-02-12T13:32:21.618Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 001: Asymptotic Analysis***English** document is available*](/en/Knowledge-base/Algorithm/c-language-001-asymptotic-analysis)
{.links-list}


# 【C语言】001：渐近分析

渐近分析是一种数学工具，用于理解函数在输入变大时的行为。它允许我们对算法的运行时间做出陈述，而不必在大输入上实际运行算法。

渐近分析有两种主要类型：最坏情况分析和平均情况分析。

## 最坏情况分析

最坏情况分析是渐近分析的最简单形式。它只是查看算法的最坏可能输入并分析这种情况下的运行时间。

例如，假设我们有一个对 n 个数字的数组进行排序的算法。该算法的最坏情况输入是一个已经按相反顺序排序的数组。在这种情况下，算法的运行时间为 O(n^2)。

## 平均案例分析

平均情况分析比最坏情况分析稍微复杂一些。它查看算法的所有可能输入并计算平均运行时间。

对于我们的排序算法示例，平均案例运行时间为 O(n log n)。这是因为有 n!算法的可能输入，并且每个输入的运行时间是不同的。要计算平均运行时间，我们只需将所有运行时间的总和除以 n!。

## 渐近符号

渐近符号是一种用于描述算法运行时间的数学符号。三个最常见的符号是 O(n)、Ω(n) 和 Θ(n)。

O(n) 表示法用于描述算法的最坏情况运行时间。对于我们的排序算法示例，最坏情况下的运行时间是 O(n^2)。

Ω(n) 符号用于描述算法的最佳运行时间。对于我们的排序算法示例，最佳情况运行时间是 Ω(n log n)。

Θ(n) 符号用于描述算法的平均情况运行时间。对于我们的排序算法示例，平均案例运行时间为 Θ(n log n)。

## 练习

1. 给定以下代码，什么是渐近运行时？

```C
int sum(int n) {
    int i;
    int s = 0;
    for (i = 1; i <= n; i++) {
        s = s + i;
    }
    return s;
}
```

此代码的渐近运行时间为 O(n)。

2. 给定以下代码，什么是渐近运行时？

```C
int sum(int n) {
    int i;
    int s = 0;
    for (i = 1; i <= n; i++) {
        s = s + i;
        if (s > 100) {
            break;
        }
    }
    return s;
}
```

此代码的渐近运行时间为 O(n)。