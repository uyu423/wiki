---
title: [C언어] 029: 버블정렬
description: 
published: true
date: 2023-02-13T10:33:00.264Z
tags: 
editor: markdown
dateCreated: 2023-02-13T10:32:58.601Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 029: Bubble Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-029-bubble-sort)
{.links-list}


# 029: 버블 정렬

버블 정렬은 인접한 요소의 순서가 잘못된 경우 반복적으로 교체하여 작동하는 정렬 알고리즘입니다. 버블 정렬이라는 이름은 작은 요소가 목록의 맨 위로 "버블링"하고 큰 요소는 맨 아래로 가라앉는다는 사실에서 유래되었습니다.

버블 정렬은 가장 간단한 정렬 알고리즘 중 하나이지만 가장 비효율적이기도 합니다. 최악의 경우 평균 복잡도는 **O(n^2)**입니다. 여기서 **n**은 정렬되는 항목의 수입니다. 단순성과 비효율성에도 불구하고 버블 정렬은 구현하기 쉽기 때문에 여전히 일부 경우에 사용됩니다.

## 알고리즘

버블 정렬의 기본 아이디어는 각 요소를 인접한 요소와 비교하고 순서가 잘못된 경우 교환하는 것입니다. 이 과정은 전체 목록이 정렬될 때까지 반복됩니다.

오름차순으로 정렬해야 하는 다음 숫자 목록을 고려하십시오.

[5, 1, 4, 2, 8]

처음 두 요소인 5와 1을 비교하고 5가 1보다 크기 때문에 교환합니다. 이제 목록은 다음과 같습니다.

[1, 5, 4, 2, 8]

다음 두 요소인 5와 4를 비교하고 5가 4보다 크기 때문에 교환합니다. 이제 목록은 다음과 같습니다.

[1, 4, 5, 2, 8]

다음 두 요소인 5와 2를 비교하고 5가 2보다 크기 때문에 교환합니다. 이제 목록은 다음과 같습니다.

[1, 4, 2, 5, 8]

다음 두 요소인 5와 8을 비교하고 5가 8보다 크지 않기 때문에 교환하지 않습니다. 이제 목록은 다음과 같습니다.

[1, 4, 2, 5, 8]

이 시점에서 목록은 이미 정렬되어 있으므로 중지할 수 있습니다.

다음 애니메이션은 목록 [5, 1, 4, 2, 8]에 대한 전체 버블 정렬 프로세스를 보여줍니다.

![버블 정렬 애니메이션](https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif)

## 복잡성

앞서 언급했듯이 버블 정렬은 최악의 경우 평균 복잡도가 **O(n^2)**입니다. 이는 알고리즘이 각 요소를 목록의 다른 모든 요소와 비교하고 순서가 잘못된 경우 교체해야 하기 때문입니다.

거품 정렬에 대한 최상의 시나리오는 목록이 이미 정렬된 경우에 발생합니다. 이 경우 알고리즘은 스와핑을 수행할 필요가 없으며 복잡도는 **O(n)**이 됩니다.

## 구현

다음은 C 프로그래밍 언어로 버블 정렬을 간단하게 구현한 것입니다.

```C
void bubble_sort(int array[], int n)
{
    int i, j, temp;

    for (i = 0; i < n - 1; i++)
    {
        for (j = 0; j < n - i - 1; j++)
        {
            if (array[j] > array[j + 1])
            {
                temp = array[j];
                array[j] = array[j + 1];
                array[j + 1] = temp;
            }
        }
    }
}
```

## 운동

1. 자신의 프로그래밍 언어로 버블 정렬 알고리즘을 구현합니다.

2. 목록이 이미 정렬된 경우 조기에 중지되도록 버블 정렬 알고리즘을 수정합니다.

## 답변

1.

```C
void bubble_sort(int array[], int n)
{
    int i, j, temp;

    for (i = 0; i < n - 1; i++)
    {
        for (j = 0; j < n - i - 1; j++)
        {
            if (array[j] > array[j + 1])
            {
                temp = array[j];
                array[j] = array[j + 1];
                array[j + 1] = temp;
            }
        }
    }
}
```

2.

```C
void bubble_sort(int array[], int n)
{
    int i, j, temp;
    bool swapped;

    for (i = 0; i < n - 1; i++)
    {
        swapped = false;

        for (j = 0; j < n - i - 1; j++)
        {
            if (array[j] > array[j + 1])
            {
                temp = array[j];
                array[j] = array[j + 1];
                array[j + 1] = temp;

                swapped = true;
            }
        }

        if (!swapped)
        {
            break;
        }
    }
}
```