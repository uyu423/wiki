---
title: [C언어] 006: 그리디 알고리즘
description: 
published: true
date: 2023-02-12T17:32:26.795Z
tags: 
editor: markdown
dateCreated: 2023-02-12T17:32:25.151Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 006: Greedy Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/c-language-006-greedy-algorithms)
{.links-list}


# 그리디 알고리즘

컴퓨터 과학에서 그리디 알고리즘은 전역 최적을 찾기 위해 각 단계에서 로컬 최적 선택을 하는 문제 해결 휴리스틱을 따르는 알고리즘입니다. 많은 문제에서 탐욕적 전략은 일반적으로 최적의 솔루션을 생성하지 않지만 그럼에도 불구하고 탐욕적 휴리스틱은 합리적인 시간 내에 올바른 솔루션에 대한 근사치를 생성하는 일부 문제에 대한 최상의 전략일 수 있습니다.

## 그리디 알고리즘이란?

그리디 알고리즘은 전역 최적을 찾기 위해 각 단계에서 로컬 최적을 선택하는 알고리즘입니다.

그리디 알고리즘과 다른 알고리즘의 주요 차이점은 그리디 알고리즘은 더 나은 전체 솔루션으로 이어지더라도 자신의 선택을 재고하지 않는다는 것입니다.

## 그리디 알고리즘은 어떻게 작동합니까?

Greedy 알고리즘은 전역 최적값을 찾기 위해 각 단계에서 로컬 최적 선택을 수행하여 작동합니다.

그리디 알고리즘이 작동하는 방식을 이해하는 열쇠는 알고리즘이 항상 최상의 전체 솔루션을 찾는 것이 아니라 각 개별 단계에서 최상의 솔루션을 찾고 있다는 사실을 깨닫는 것입니다.

## Greedy 알고리즘은 언제 사용하나요?

그리디 알고리즘은 로컬 최적 선택이 전체 최적으로 이어질 가능성이 있을 때 가장 잘 사용됩니다.

이에 대한 한 가지 일반적인 예는 최단 경로 문제입니다. 최단 경로 문제에서는 노드 집합과 노드 집합을 연결하는 가장자리 집합이 제공됩니다. 또한 시작 노드와 목표 노드가 제공됩니다. 문제의 목표는 시작 노드에서 목표 노드까지의 최단 경로를 찾는 것입니다.

그리디 알고리즘은 항상 현재 노드에서 목표 노드까지의 최단 경로를 선택하여 이 문제를 해결합니다. 전체적으로 최단 경로를 찾지 못할 수도 있지만 최단 경로에 가까운 경로를 찾을 가능성이 높습니다.

## 코드 예제

다음은 탐욕스러운 알고리즘이 작동하는 간단한 예입니다. 다음 문제를 고려하십시오.

가치가 다른 동전 세트가 주어지고 일정 금액의 돈을 벌기 위해 필요한 최소 동전 수를 찾아야 합니다.

그리디 알고리즘은 항상 가장 가치가 높은 코인을 먼저 선택함으로써 이 문제를 해결할 것입니다. 예를 들어 사용 가능한 동전이 1, 5, 10, 25이고 벌고자 하는 금액이 30이면 탐욕 알고리즘은 먼저 가치가 25인 동전을 선택한 다음 가치가 5인 동전을 선택합니다. 이것은 총 2개의 코인을 제공하며, 이는 30개를 만드는 데 필요한 최소 코인 수입니다.

## 운동

1. 코인 변경 문제에 대한 그리디 알고리즘을 구현합니다.

2. 다음 문제를 고려하십시오. 각각 특정 기간이 있는 완료해야 하는 일련의 작업이 주어집니다. 또한 각각 특정 시간의 사용 가능한 시간이 있는 일련의 기계가 있습니다. 문제의 목표는 모든 작업을 완료하는 데 필요한 최소 기계 수를 찾는 것입니다.

3. 그리디 알고리즘을 사용하여 문제를 해결합니다.

4. 다음 문제를 고려하십시오. 각각 특정 기간이 있는 n개의 작업 세트가 주어집니다. 또한 각각 특정 시간의 사용 가능한 시간이 있는 m개의 기계 세트가 있습니다. 문제의 목표는 모든 작업을 완료하는 데 필요한 최소 기계 수를 찾는 것입니다.

5. 그리디 알고리즘을 사용하여 문제를 해결합니다.