---
title: [C Language] 035: Radix Sort
description: 
published: true
date: 2023-02-13T15:32:59.287Z
tags: 
editor: markdown
dateCreated: 2023-02-13T15:32:57.192Z
---

- [[Lenguaje C] 035: Clasificación Radix***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-035-radix-sort)
{.links-list}
- [[C语言]035：基数排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-035-radix-sort)
{.links-list}
- [[C언어] 035: 기수 정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-035-radix-sort)
{.links-list}


# Radix Sort

Radix sort is an efficient sorting algorithm that sorts data with integer keys by grouping keys by the individual digits which share the same significant position and value. A positional notation is required, but because integers can represent strings of characters (e.g., in binary, a character can be represented by eight bits), radix sort is not limited to integers.

Radix sort improves on the efficiency of comparison sorts by creating a bucket for each key and placing all keys with the same digit into the same bucket. This reduces the number of comparisons required to sort the data.

The time complexity of radix sort is O(n * k), where n is the number of keys and k is the number of digits.

## Code Example

The following is a simple implementation of radix sort in C.

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

## Explanation

Radix sort works by starting with the least significant digit (LSD) and sorting the data based on that digit. The LSD is the digit in the ones position. The next digit to the left is the second LSD, the digit in the tens position. This process is repeated until all digits have been considered.

To sort the data, radix sort uses a counting sort for each digit. A counting sort keeps track of the number of keys that have a given digit in a specific position. For example, if the LSD is being considered, the counting sort will keep track of the number of keys that have a 0 in the LSD position, the number of keys that have a 1 in the LSD position, and so on.

Once the counting sort has been performed for the LSD, the data is rearranged so that all keys with the same LSD are next to each other. The keys are then sorted based on the next digit to the left (i.e., the second LSD). This process is repeated until all digits have been considered.

Radix sort is a stable sorting algorithm because the keys are sorted based on the digits from right to left. This means that keys with the same digits in the leftmost positions will retain their relative order.

## Complexity

The time complexity of radix sort is O(n * k), where n is the number of keys and k is the number of digits. The space complexity is O(n + k).