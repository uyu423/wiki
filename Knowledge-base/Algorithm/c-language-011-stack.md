---
title: [C언어] 011: 스택
description: 
published: true
date: 2023-02-09T09:55:46.138Z
tags: 
editor: markdown
dateCreated: 2023-02-09T09:55:39.781Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 011: Stack***English** document is available*](/en/Knowledge-base/Algorithm/c-language-011-stack)
{.links-list}


# 스택

스택은 객체가 다른 객체 위에 쌓인 구조인 실제 물리적 스택 또는 더미로 표현되는 선형 구조로 논리적으로 생각할 수 있는 기본 데이터 구조입니다. 스택의 기본 원칙은 스택에 마지막으로 삽입된 요소가 가장 먼저 제거되는 요소라는 것입니다.

스택은 작업을 수행할 수 있는 미리 정의된 순서가 있기 때문에 제한된 데이터 구조입니다. 주문은 LIFO(Last In First Out)로 제한됩니다.

스택의 실제 사례는 많이 있습니다. 몇 가지 예는 다음과 같습니다.

- 카드 한 벌
- 음식 한 접시
- 책 더미

## 구현

스택은 배열 또는 연결 목록을 사용하여 구현할 수 있습니다. 이 게시물에서는 배열을 사용하여 스택을 구현하는 방법에 대해 설명합니다.

### 어레이 구현

스택의 배열 구현은 매우 간단합니다. 스택의 맨 위 요소를 추적하는 변수를 유지하기만 하면 됩니다. 맨 위 요소는 스택에 마지막으로 추가된 요소입니다.

스택에서 수행할 수 있는 작업은 다음과 같습니다.

- 푸시: 이 작업은 스택의 맨 위에 요소를 추가합니다.
- 팝: 이 작업은 스택의 맨 위에서 요소를 제거합니다.
- Peek: 이 작업은 스택의 맨 위에 있는 요소를 제거하지 않고 반환합니다.
- isEmpty: 이 작업은 스택이 비어 있으면 true를 반환하고 그렇지 않으면 false를 반환합니다.

다음은 C 프로그래밍 언어에서 배열을 사용하여 스택을 구현한 것입니다.

```c
#include <stdio.h>
#include <stdlib.h>
 
#define MAXSIZE 10
 
struct stack
{
    int top;
    int items[MAXSIZE];
};
 
struct stack* createStack()
{
    struct stack* s = (struct stack*) malloc(sizeof(struct stack));
    s->top = -1;
    return s;
}
 
int isEmpty(struct stack* s)
{
    return (s->top == -1);
}
 
int peek(struct stack* s)
{
    if (!isEmpty(s))
        return s->items[s->top];
    return -1;
}
 
void push(struct stack* s, int x)
{
    if (s->top == MAXSIZE-1)
    {
        printf("Stack overflow\n");
        return;
    }
    s->items[++s->top] = x;
}
 
int pop(struct stack* s)
{
    if (isEmpty(s))
    {
        printf("Stack underflow\n");
        return -1;
    }
    return s->items[s->top--];
}
 
int main()
{
    struct stack* s = createStack();
    push(s, 1);
    push(s, 2);
    push(s, 3);
    printf("%d popped from stack\n", pop(s));
    printf("Top element is %d\n", peek(s));
    return 0;
}
```

산출:

```
3 popped from stack
Top element is 2
```

위의 프로그램에서 MAXSIZE=10 크기의 스택을 만들었습니다. top 변수는 스택의 최상위 요소 인덱스를 저장합니다. 푸시 작업은 스택 상단에 요소를 추가하고 팝 작업은 스택 상단에서 요소를 제거합니다. peek 작업은 제거하지 않고 스택 맨 위에 있는 요소를 반환합니다. isEmpty 연산은 스택이 비어 있으면 true를 반환하고 그렇지 않으면 false를 반환합니다.

## 애플리케이션

스택은 컴퓨터 과학에서 많은 응용 분야를 가지고 있습니다. 스택의 일부 응용 프로그램은 다음과 같습니다.

- 파싱: 스택은 파싱에 사용됩니다. 예를 들어 "3 + ((5*9) + 2)"와 같은 산술식이 주어지면 스택을 이용하여 파싱할 수 있다.
- 역추적: 스택은 역추적에 사용됩니다. 예를 들어 미로가 주어졌을 때 스택을 사용하여 경로를 추적하고 막다른 골목에 도달하면 역추적할 수 있습니다.
- 텍스트 편집기에서 실행 취소 작업: 스택은 텍스트 편집기에서 실행 취소 작업을 구현하는 데 사용됩니다. 예를 들어 문자를 입력하면 스택으로 푸시됩니다. 실행 취소 버튼을 누르면 맨 위 문자가 스택에서 팝됩니다.
- 식 평가 및 변환: 스택은 중위 표기법의 식 평가 및 후위 표기법으로의 변환에 사용됩니다.