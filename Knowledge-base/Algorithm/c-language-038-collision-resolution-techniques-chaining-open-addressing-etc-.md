---
title: [C 언어] 038: 충돌 해결 기술(체인화, 개방 주소 지정 등)
description: 
published: true
date: 2023-02-13T18:32:31.720Z
tags: 
editor: markdown
dateCreated: 2023-02-13T18:32:30.154Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 038: Collision Resolution Techniques (Chaining, Open Addressing, etc.)***English** document is available*](/en/Knowledge-base/Algorithm/c-language-038-collision-resolution-techniques-chaining-open-addressing-etc-)
{.links-list}


# 충돌 해결 기술

## 소개

컴퓨터 과학에서 충돌은 해시 테이블에서 두 개 이상의 요소가 충돌하는 경우입니다. 해시 테이블은 키와 값을 저장하는 데 사용되는 데이터 구조입니다. 키가 해시되면 해시 함수는 키-값 쌍을 해시 테이블에 저장하는 데 사용되는 인덱스를 반환합니다. 그러나 두 개의 키가 동일한 인덱스로 해시되면 충돌이 발생합니다.

세 가지 주요 충돌 해결 기술이 있습니다: 연결, 개방 주소 지정 및 이중 해싱. 이 게시물에서는 이러한 각 기술에 대해 자세히 설명합니다.

## 체이닝

체이닝은 연결된 목록을 사용하여 충돌한 키-값 쌍을 저장하는 충돌 해결 기술입니다. 키가 해시되면 해시 함수는 인덱스를 반환합니다. 인덱스가 비어 있으면 키-값 쌍이 단순히 해당 인덱스에 저장됩니다. 그러나 인덱스가 이미 사용 중인 경우 해당 인덱스의 연결 목록에 키-값 쌍이 추가됩니다.

체이닝의 장점은 구현하기 쉽다는 것입니다. 체이닝의 단점은 해시 테이블이 너무 꽉 차면 성능이 저하될 수 있다는 것입니다. 연결된 목록이 매우 길어지고 특정 키-값 쌍을 찾는 데 더 오래 걸리기 때문입니다.

다음은 의사 코드의 연결 예입니다.

```
function insert(key, value)
  index = hash(key)

  if table[index] is empty
    table[index] = key-value pair
  else
    add key-value pair to the linked list at table[index]
```

## 오픈 어드레싱

개방 주소 지정은 프로빙을 사용하여 키-값 쌍을 저장할 빈 인덱스를 찾는 충돌 해결 기술입니다. 키가 해시되면 해시 함수는 인덱스를 반환합니다. 인덱스가 비어 있으면 키-값 쌍이 단순히 해당 인덱스에 저장됩니다. 그러나 인덱스가 이미 점유된 경우 다음 빈 인덱스에 키-값 쌍이 저장됩니다.

개방형 주소 지정의 장점은 해시 테이블이 너무 꽉 차 있지 않은 경우 체인보다 빠를 수 있다는 것입니다. 개방형 주소 지정의 단점은 해시 테이블이 너무 꽉 차면 성능이 저하될 수 있다는 것입니다. 이는 해시 테이블이 가득 차면 프로빙이 매우 느려질 수 있기 때문입니다.

다음은 의사 코드에서 열린 주소 지정의 예입니다.

```
function insert(key, value)
  index = hash(key)

  while table[index] is occupied
    index = (index + 1) mod table.size

  table[index] = key-value pair
```

## 더블 해싱

이중 해싱은 두 개의 해시 함수를 사용하여 키-값 쌍을 저장할 빈 인덱스를 찾는 충돌 해결 기술입니다. 키가 해시되면 첫 번째 해시 함수는 인덱스를 반환합니다. 인덱스가 비어 있으면 키-값 쌍이 단순히 해당 인덱스에 저장됩니다. 그러나 인덱스가 이미 점유된 경우 두 번째 해시 함수로 키-값 쌍을 다시 해시합니다. 두 번째 해시 함수는 다른 인덱스를 반환하고 키-값 쌍은 해당 인덱스에 저장됩니다.

이중 해싱의 장점은 해시 테이블이 너무 가득 차 있지 않은 경우 개방 주소 지정보다 빠를 수 있다는 것입니다. 이중 해싱의 단점은 해시 테이블이 너무 꽉 차면 성능이 저하될 수 있다는 것입니다. 이는 두 번째 해시 함수가 첫 번째 해시 함수와 동일한 인덱스를 반환할 수 있어 무한 루프로 이어질 수 있기 때문입니다.

의사 코드에서 이중 해싱의 예는 다음과 같습니다.

```
function insert(key, value)
  index = hash(key)
  index2 = hash2(key)

  while table[index] is occupied
    index = (index + index2) mod table.size

  table[index] = key-value pair
```

## 결론

이 게시물에서는 세 가지 충돌 해결 기술인 연결, 개방 주소 지정 및 이중 해싱에 대해 논의했습니다. 이러한 각 기술에는 고유한 장점과 단점이 있습니다. 애플리케이션에 적합한 기술을 선택하십시오.