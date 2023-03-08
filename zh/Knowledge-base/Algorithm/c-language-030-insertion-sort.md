---
title: [C语言]030：插入排序
description: 
published: true
date: 2023-02-13T00:17:32.979Z
tags: 
editor: markdown
dateCreated: 2023-02-13T00:17:31.313Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 030: Insertion Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-030-insertion-sort)
{.links-list}


# 030：插入排序

插入排序是一种简单的排序算法，它的工作原理是一次接受一个新项目并将它们插入到已排序列表中的正确位置。与快速排序、堆排序或合并排序等更高级的算法相比，它在大型列表上的效率要低得多。但是，它对于小列表非常有效，并且经常用作更复杂算法的一部分。它也是一种稳定排序，这意味着它保留了具有相同键的项目的顺序。

这是一个简单的插入排序示例。我们从一个未排序的数字列表开始：

```
5, 2, 4, 6, 1, 3
```

为了对这个列表进行排序，我们首先获取第二项 (`2`) 并将其插入到已经排序的列表 (`5, 2, 4, 6, 1, 3`) 中的正确位置。然后我们取出第三项 (`4`) 并将其插入到已排序列表 (`2, 4, 5, 6, 1, 3`) 中的正确位置。我们以这种方式继续，直到对整个列表进行排序：

```
1, 2, 3, 4, 5, 6
```

插入排序算法可以用几行代码实现。下面是一个简单的 C 实现：

```C
void insertion_sort(int array[], int n)
{
    int i, j, temp;
    
    for (i = 1; i < n; i++) {
        temp = array[i];
        j = i-1;
        while (j >= 0 && array[j] > temp) {
            array[j+1] = array[j];
            j--;
        }
        array[j+1] = temp;
    }
}
```

此实现对数组进行就地排序，这意味着它对数组进行就地排序而不创建新数组。

为了测试这个实现，我们可以创建一个随机数数组并使用插入排序算法对其进行排序。然后我们可以打印排序后的数组以查看它是否确实排序：

```C
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void insertion_sort(int array[], int n);

int main(void)
{
    int i, n = 10;
    int array[n];
    
    srand(time(NULL));
    
    for (i = 0; i < n; i++) {
        array[i] = rand() % 100;
    }
    
    insertion_sort(array, n);
    
    for (i = 0; i < n; i++) {
        printf("%d ", array[i]);
    }
    printf("\n");
    
    return 0;
}
```

运行这段代码会得到以下输出：

```
2 4 5 8 12 23 37 38 39 45 
```

我们可以看到数组确实是有序的。

## 复杂性

插入排序最坏情况下的时间复杂度是 O(n^2)。当数组以相反的顺序排序时会发生这种情况。最好的情况时间复杂度是 O(n) 并且在数组已经排序时发生。

插入排序是一种稳定排序，这意味着它保留了具有相同键的项目的顺序。它也是一种就地排序，这意味着它在不创建新数组的情况下就地对数组进行排序。

## 练习

1. 用你喜欢的编程语言实现插入排序算法。

2、修改插入排序算法，对单向链表进行排序。

3.修改插入排序算法，对字符串数组进行排序。