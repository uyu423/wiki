---
title: [C언어] 049: Radix Tree(Compact Trie)
description: 
published: true
date: 2023-02-10T12:55:21.084Z
tags: 
editor: markdown
dateCreated: 2023-02-10T12:55:19.354Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 049: Radix Tree (Compact Trie)***English** document is available*](/en/Knowledge-base/Algorithm/c-language-049-radix-tree-compact-trie)
{.links-list}


# 049: 라딕스 트리(컴팩트 트리)

## 1. 소개

압축 트리라고도 하는 기수 트리는 문자열을 저장하는 데 사용되는 공간 효율적인 데이터 구조입니다. 이진 트리와 유사하지만 각 노드에는 노드당 두 개의 자식이 아니라 두 개의 자식만 있습니다.

## 2. 알고리즘

기수 트리 알고리즘은 문자열을 저장하는 공간 효율적인 방법입니다. 이진 트리와 유사하지만 각 노드에는 노드당 두 개의 자식이 아니라 두 개의 자식만 있습니다.

기수 트리 알고리즘은 문자열을 저장하는 공간 효율적인 방법입니다. 이진 트리와 유사하지만 각 노드에는 노드당 두 개의 자식이 아니라 두 개의 자식만 있습니다.

문자열을 기수 트리에 삽입하려면 먼저 문자열과 루트 노드 사이에서 가장 긴 공통 접두사를 찾습니다. 가장 긴 공통 접두사가 문자열과 같으면 문자열을 루트 노드의 트리에 삽입합니다. 그렇지 않으면 가장 긴 공통 접두사에 해당하는 노드의 트리에 문자열을 삽입합니다.

기수 트리에서 문자열을 검색하려면 먼저 문자열과 루트 노드 사이에서 가장 긴 공통 접두사를 찾습니다. 가장 긴 공통 접두사가 문자열과 같으면 루트 노드를 반환합니다. 그렇지 않으면 하위 트리에서 가장 긴 공통 접두사에 해당하는 문자열을 검색합니다.

## 3. 코드 예제

### 3.1 삽입

```c
void insert(Node* root, char* str) {
  int i, j, k;
  Node* cur = root;
  for (i = 0; str[i] != '\0'; i++) {
    for (j = 0; j < cur->n; j++) {
      if (cur->children[j]->c == str[i]) {
        cur = cur->children[j];
        break;
      }
    }
    if (j == cur->n) {
      Node* newNode = malloc(sizeof(Node));
      newNode->c = str[i];
      newNode->n = 1;
      cur->children[cur->n] = newNode;
      cur->n++;
    }
  }
}
```

### 3.2 검색

```c
Node* search(Node* root, char* str) {
  int i, j;
  Node* cur = root;
  for (i = 0; str[i] != '\0'; i++) {
    for (j = 0; j < cur->n; j++) {
      if (cur->children[j]->c == str[i]) {
        cur = cur->children[j];
        break;
      }
    }
    if (j == cur->n) {
      return NULL;
    }
  }
  return cur;
}
```

## 4. 운동

1. 선호하는 프로그래밍 언어로 기수 트리 알고리즘을 구현합니다.

2. 기수 트리 알고리즘을 사용하여 영어 단어 목록을 저장합니다.

3. 기수 트리 알고리즘을 사용하여 DNA 문자열 목록을 저장합니다.

## 5. 답변

1. 위의 코드 예제를 참조하십시오.

2. 코드 예제 3.2를 참조하십시오.

3. 코드 예제 3.1을 참조하십시오.