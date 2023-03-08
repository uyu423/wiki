---
title: [C语言]035：基数排序
description: 
published: true
date: 2023-02-13T15:33:04.743Z
tags: 
editor: markdown
dateCreated: 2023-02-13T15:32:57.188Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 035: Radix Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-035-radix-sort)
{.links-list}


# 基数排序

基数排序是一种高效的排序算法，它通过按共享相同有效位置和值的各个数字对键进行分组来对具有整数键的数据进行排序。位置符号是必需的，但因为整数可以表示字符串（例如，在二进制中，一个字符可以用八位表示），基数排序不限于整数。

基数排序通过为每个键创建一个桶并将具有相同数字的所有键放入同一个桶中来提高比较排序的效率。这减少了对数据进行排序所需的比较次数。

基数排序的时间复杂度为O(n * k)，其中n为键的个数，k为位数。

## 代码示例

下面是C中基数排序的简单实现。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
 
#define MAX_NUMBER_OF_DIGITS 10
 
void radix_sort(int *array, int n)
{
    int i, j, k, digit, divisor, count[10], temp[n];
 
    divisor = 1;
 
    for (i = 0; i < MAX_NUMBER_OF_DIGITS; i++)
    {
        for (j = 0; j < 10; j++)
        {
            count[j] = 0;
        }
 
        for (j = 0; j < n; j++)
        {
            digit = (array[j] / divisor) % 10;
            count[digit]++;
        }
 
        for (j = 1; j < 10; j++)
        {
            count[j] += count[j - 1];
        }
 
        for (j = n - 1; j >= 0; j--)
        {
            digit = (array[j] / divisor) % 10;
            temp[count[digit] - 1] = array[j];
            count[digit]--;
        }
 
        for (j = 0; j < n; j++)
        {
            array[j] = temp[j];
        }
 
        divisor *= 10;
    }
}
 
int main()
{
    int array[] = {329, 457, 657, 839, 436,720,355};
    int n = sizeof(array) / sizeof(array[0]);
 
    radix_sort(array, n);
 
    for (int i = 0; i < n; i++)
    {
        printf("%d ", array[i]);
    }
 
    return 0;
}
```

## 解释

基数排序的工作原理是从最低有效数字 (LSD) 开始并根据该数字对数据进行排序。 LSD 是个位上的数字。左边的下一个数字是第二个 LSD，十位中的数字。重复此过程，直到所有数字都已被考虑。

为了对数据进行排序，基数排序对每个数字使用计数排序。计数排序跟踪在特定位置具有给定数字的键的数量。例如，如果考虑 LSD，计数排序将跟踪 LSD 位置为 0 的键的数量，LSD 位置为 1 的键的数量，等等。

一旦对 LSD 执行了计数排序，就会重新排列数据，以便所有具有相同 LSD 的键彼此相邻。然后根据左边的下一个数字（即第二个 LSD）对键进行排序。重复此过程，直到所有数字都已被考虑。

基数排序是一种稳定的排序算法，因为键是根据从右到左的数字排序的。这意味着在最左边位置具有相同数字的键将保持其相对顺序。

## 复杂性

基数排序的时间复杂度为O(n * k)，其中n为键的个数，k为位数。空间复杂度为 O(n + k)。