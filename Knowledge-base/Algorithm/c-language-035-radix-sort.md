---
title: [C언어] 035: 기수 정렬
description: 
published: true
date: 2023-02-13T15:33:04.743Z
tags: 
editor: markdown
dateCreated: 2023-02-13T15:32:57.188Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 035: Radix Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-035-radix-sort)
{.links-list}


# 기수 정렬

기수 정렬은 동일한 중요한 위치와 값을 공유하는 개별 숫자별로 키를 그룹화하여 정수 키로 데이터를 정렬하는 효율적인 정렬 알고리즘입니다. 위치 표기법이 필요하지만 정수는 문자열을 나타낼 수 있기 때문에(예: 이진법에서는 문자를 8비트로 나타낼 수 있음) 기수 정렬은 정수로 제한되지 않습니다.

기수 정렬은 각 키에 대한 버킷을 생성하고 동일한 숫자를 가진 모든 키를 동일한 버킷에 배치하여 비교 정렬의 효율성을 향상시킵니다. 이렇게 하면 데이터를 정렬하는 데 필요한 비교 횟수가 줄어듭니다.

기수 정렬의 시간 복잡도는 O(n * k)이며 여기서 n은 키의 수이고 k는 자릿수입니다.

## 코드 예

다음은 C에서 기수 정렬을 간단하게 구현한 것입니다.

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

## 설명

기수 정렬은 최하위 숫자(LSD)로 시작하여 해당 숫자를 기준으로 데이터를 정렬하는 방식으로 작동합니다. LSD는 one 위치의 숫자입니다. 왼쪽에 있는 다음 숫자는 십의 자리에 있는 숫자인 두 번째 LSD입니다. 이 프로세스는 모든 숫자가 고려될 때까지 반복됩니다.

데이터를 정렬하기 위해 기수 정렬은 각 숫자에 대해 카운팅 정렬을 사용합니다. 카운팅 정렬은 특정 위치에 주어진 숫자가 있는 키의 수를 추적합니다. 예를 들어 LSD를 고려 중인 경우 계수 정렬은 LSD 위치에 0이 있는 키의 수, LSD 위치에 1이 있는 키의 수 등을 추적합니다.

LSD에 대한 카운팅 정렬이 수행되면 동일한 LSD를 가진 모든 키가 서로 옆에 있도록 데이터가 재정렬됩니다. 그런 다음 키는 왼쪽의 다음 숫자(즉, 두 번째 LSD)를 기준으로 정렬됩니다. 이 프로세스는 모든 숫자가 고려될 때까지 반복됩니다.

기수 정렬은 키가 오른쪽에서 왼쪽으로 숫자를 기준으로 정렬되기 때문에 안정적인 정렬 알고리즘입니다. 즉, 가장 왼쪽 위치에 동일한 숫자가 있는 키는 상대적인 순서를 유지합니다.

## 복잡성

기수 정렬의 시간 복잡도는 O(n * k)이며 여기서 n은 키의 수이고 k는 자릿수입니다. 공간 복잡도는 O(n + k)입니다.