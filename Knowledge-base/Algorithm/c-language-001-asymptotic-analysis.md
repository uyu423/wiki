---
title: [C언어] 001: 점근적 해석
description: 
published: true
date: 2023-02-12T13:32:23.496Z
tags: 
editor: markdown
dateCreated: 2023-02-12T13:32:21.617Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 001: Asymptotic Analysis***English** document is available*](/en/Knowledge-base/Algorithm/c-language-001-asymptotic-analysis)
{.links-list}


# [C Language] 001: 점근적 분석

점근 분석은 입력이 커짐에 따라 함수의 동작을 이해하는 데 사용되는 수학적 도구입니다. 이를 통해 큰 입력에 대해 실제로 알고리즘을 실행하지 않고도 알고리즘의 실행 시간에 대한 진술을 할 수 있습니다.

점근 분석에는 최악의 경우 분석과 평균 사례 분석의 두 가지 주요 유형이 있습니다.

## 최악의 경우 분석

최악의 경우 분석은 점근 분석의 가장 간단한 형태입니다. 단순히 알고리즘에 대한 최악의 입력을 보고 이 경우 런타임을 분석합니다.

예를 들어 n개의 숫자 배열을 정렬하는 알고리즘이 있다고 가정해 보겠습니다. 이 알고리즘의 최악의 입력은 이미 역순으로 정렬된 배열입니다. 이 경우 알고리즘의 실행 시간은 O(n^2)입니다.

## 평균 사례 분석

평균 사례 분석은 최악 사례 분석보다 조금 더 복잡합니다. 알고리즘에 대한 모든 가능한 입력을 살펴보고 평균 실행 시간을 계산합니다.

정렬 알고리즘 예제의 경우 평균 사례 실행 시간은 O(n log n)입니다. 이것은 n이 있기 때문입니다! 알고리즘에 대한 가능한 입력과 각 입력에 대한 실행 시간이 다릅니다. 평균 실행 시간을 계산하려면 모든 실행 시간의 합계를 n!으로 나누면 됩니다.

## 점근적 표기법

점근적 표기법은 알고리즘의 실행 시간을 설명하는 데 사용되는 수학적 표기법입니다. 세 가지 가장 일반적인 표기법은 O(n), Ω(n) 및 Θ(n)입니다.

O(n) 표기법은 알고리즘의 최악의 런타임을 설명하는 데 사용됩니다. 정렬 알고리즘 예제의 경우 최악의 런타임은 O(n^2)입니다.

Ω(n) 표기법은 알고리즘의 최상의 실행 시간을 설명하는 데 사용됩니다. 정렬 알고리즘 예제의 경우 최상의 실행 시간은 Ω(n log n)입니다.

Θ(n) 표기법은 알고리즘의 평균 사례 런타임을 설명하는 데 사용됩니다. 정렬 알고리즘 예제의 경우 평균 사례 실행 시간은 Θ(n log n)입니다.

## 수업 과정

1. 다음 코드가 주어지면 점근적 런타임은 무엇입니까?

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

이 코드의 점근적 실행 시간은 O(n)입니다.

2. 다음 코드가 주어지면 점근적 런타임은 무엇입니까?

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

이 코드의 점근적 실행 시간은 O(n)입니다.