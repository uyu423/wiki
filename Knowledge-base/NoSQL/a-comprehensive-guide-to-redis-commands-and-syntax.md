---
title: Redis 명령 및 구문에 대한 종합 가이드
description: 
published: true
date: 2023-03-07T10:32:45.919Z
tags: 
editor: markdown
dateCreated: 2023-03-07T10:32:38.598Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [A Comprehensive Guide to Redis Commands and Syntax***English** document is available*](/en/Knowledge-base/NoSQL/a-comprehensive-guide-to-redis-commands-and-syntax)
{.links-list}

# 소개
Redis는 데이터베이스, 캐시 및 메시지 브로커로 사용되는 오픈 소스 메모리 내 데이터 구조 저장소입니다. 빠르고 안정적이며 사용하기 쉬운 것으로 알려져 있습니다. Redis는 데이터 구조를 메모리 내에서 처리하므로 디스크 기반 데이터베이스와 비교할 때 매우 빠릅니다. Redis는 데이터를 디스크에 지속적으로 저장하므로 정전이나 서버 중단 시 데이터가 손실되지 않습니다. Redis 명령은 문자열 조작, 정렬된 집합, 해시 등을 포함하여 다양한 범주로 그룹화됩니다. 이 포괄적인 가이드는 가장 유용한 Redis 명령 및 구문 중 일부를 다룹니다.

## 문자열 조작
Redis는 문자열을 조작하기 위한 다양한 명령을 제공합니다. Redis의 문자열은 바이너리 안전하므로 모든 종류의 바이너리 데이터를 저장할 수 있습니다.

### 세트
SET 명령은 키 값을 설정하는 데 사용됩니다. 키가 이미 있으면 값을 덮어씁니다.

#### 구문
```
SET key value [EX seconds] [PX milliseconds] [NX|XX]
```

#### 예
이 예에서는 "user"라는 키의 값을 "John"으로 설정합니다.
```
SET user John
```

### 얻다
GET 명령은 키 값을 검색하는 데 사용됩니다.

#### 구문
```
GET key
```

#### 예
이 예에서는 "user"라는 키 값을 검색합니다.
```
GET user
```

## 정렬된 세트
Redis는 집합과 유사한 정렬된 집합을 제공하지만 각 요소에는 연결된 점수가 있습니다.

### 자드
ZADD 명령은 정렬된 집합에 하나 이상의 구성원을 추가하거나 이미 존재하는 구성원의 점수를 업데이트하는 데 사용됩니다.

#### 구문
```
ZADD key [NX|XX] [CH] [INCR] score member [score member ...]
```

#### 예
이 예에서는 "scores"라는 정렬된 세트에 두 개의 멤버를 추가합니다.
```
ZADD scores 10 John 20 Jane
```

### 즈레인지
ZRANGE 명령은 인덱스별로 정렬된 집합에서 구성원 범위를 검색하는 데 사용됩니다.

#### 구문
```
ZRANGE key start stop [WITHSCORES]
```

#### 예
이 예에서는 "scores"라는 정렬된 집합에서 점수가 10에서 20 사이인 구성원을 검색합니다.
```
ZRANGE scores 0 -1 WITHSCORES
```

## 해시
Redis는 각 필드가 값과 연결된 사전과 유사한 해시를 제공합니다.

### HSET
HSET 명령은 해시의 필드 값을 설정하는 데 사용됩니다.

#### 구문
```
HSET key field value
```

#### 예
이 예에서는 "user"라는 해시의 "age" 필드 값을 30으로 설정합니다.
```
HSET user age 30
```

### HGET
HGET 명령은 해시에서 필드 값을 검색하는 데 사용됩니다.

#### 구문
```
HGET key field
```

#### 예
이 예제에서는 "user"라는 해시에서 "age" 필드 값을 검색합니다.
```
HGET user age
```

## 결론
Redis는 데이터베이스, 캐시 및 메시지 브로커로 사용할 수 있는 강력하고 다양한 도구입니다. 문자열, 정렬된 세트 및 해시를 포함하여 다양한 데이터 구조를 조작하기 위한 다양한 명령을 제공합니다. 이러한 명령과 해당 구문을 이해하면 Redis를 최대한 활용하고 애플리케이션의 성능을 향상할 수 있습니다.

## 외부 리소스
- [레디스 명령어](https://redis.io/commands)
- [레디스 문서](https://redis.io/documentation)