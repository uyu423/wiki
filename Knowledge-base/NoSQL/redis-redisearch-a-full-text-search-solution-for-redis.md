---
title: Redis RediSearch: Redis용 전체 텍스트 검색 솔루션
description: 
published: true
date: 2023-03-04T05:32:39.370Z
tags: 
editor: markdown
dateCreated: 2023-03-04T05:32:32.324Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Redis RediSearch: A Full-Text Search Solution for Redis***English** document is available*](/en/Knowledge-base/NoSQL/redis-redisearch-a-full-text-search-solution-for-redis)
{.links-list}
Redis RediSearch: Redis용 전체 텍스트 검색 솔루션

Redis는 일반적으로 데이터베이스, 캐시 및 메시지 브로커로 사용되는 오픈 소스 메모리 내 데이터 구조 저장소입니다. Redis는 단순성, 성능 및 다양성으로 인해 수년 동안 인기를 얻었습니다. 가장 인기 있는 Redis 모듈 중 하나는 Redis에 강력한 전체 텍스트 검색 기능을 제공하는 RediSearch입니다.

## 레디서치란?

RediSearch는 Redis에서 전체 텍스트 검색 기능을 활성화하는 Redis 모듈입니다. 이는 Redis 엔진 위에 구축되어 RediSearch가 Redis의 인메모리 데이터 구조와 빠른 성능을 활용할 수 있음을 의미합니다. RediSearch는 복잡한 쿼리를 처리하고 마이크로초 내에 검색 결과를 반환할 수 있는 강력하고 효율적인 검색 엔진입니다.

## RediSearch를 사용하는 이유는 무엇입니까?

이미 Redis를 데이터베이스, 캐시 또는 메시지 브로커로 사용하고 있는 경우 RediSearch를 통합하면 귀중한 전체 텍스트 검색 기능을 애플리케이션에 추가할 수 있습니다. RediSearch는 전자 상거래 웹 사이트, 소셜 네트워킹 플랫폼 및 콘텐츠 관리 시스템과 같이 데이터를 빠르게 검색하고 검색해야 하는 애플리케이션에 특히 유용합니다.

RediSearch는 구성 및 배포도 쉽습니다. Redis에는 이미 다양한 프로그래밍 언어로 사용할 수 있는 광범위한 클라이언트 라이브러리가 있으므로 RediSearch를 기존 애플리케이션에 쉽게 통합할 수 있습니다. 또한 RediSearch는 Redis Streams 및 Redis Graph와 같은 다른 Redis 모듈과 함께 사용하여 강력한 데이터 파이프라인을 생성할 수 있습니다.

## 레디서치의 특징

RediSearch는 Redis를 위한 훌륭한 검색 엔진이 되는 몇 가지 기능을 제공합니다.

### 1. 전체 텍스트 검색

RediSearch는 전체 텍스트 검색을 지원하므로 문서에 포함된 텍스트를 기반으로 문서를 검색할 수 있습니다. RediSearch는 역 인덱스를 사용하여 텍스트 데이터를 저장하므로 빠르고 효율적인 검색 쿼리가 가능합니다.

### 2. 자동 완성

RediSearch는 자동 완성도 지원하므로 사용자가 입력할 때 검색어를 제안해야 하는 애플리케이션에 유용합니다. RediSearch는 지금까지 입력한 검색어를 기반으로 제안을 제공하여 사용자가 원하는 것을 쉽게 찾을 수 있도록 합니다.

### 3. 숫자 필터

RediSearch는 숫자 값을 기반으로 검색 결과를 필터링할 수도 있습니다. 이는 가격, 연령 또는 기타 숫자 데이터를 기반으로 문서를 검색해야 하는 애플리케이션에 유용할 수 있습니다.

### 4. 지역 필터링

RediSearch는 지리적 위치에 따라 검색 결과를 필터링할 수도 있습니다. 이는 특정 위치에 대한 근접성을 기반으로 문서를 검색해야 하는 애플리케이션에 유용합니다.

### 5. 문서 채점

RediSearch는 검색 쿼리와의 관련성에 따라 각 문서에 점수를 할당합니다. 이는 관련성을 기준으로 검색 결과를 정렬하거나 필터링해야 하는 애플리케이션에 유용할 수 있습니다.

## 레디서치 사용하기

RediSearch를 사용하려면 먼저 Redis 서버와 RediSearch 모듈을 설치해야 합니다. 그런 다음 인덱스를 만들고 여기에 문서를 추가할 수 있습니다. 다음은 Redis 명령줄 인터페이스를 사용하여 인덱스를 만들고 여기에 문서를 추가하는 방법의 예입니다.

```redis
127.0.0.1:6379> FT.CREATE myIndex SCHEMA title TEXT body TEXT
OK
127.0.0.1:6379> FT.ADD myIndex doc1 1.0 FIELDS title "Redis RediSearch" body "Redis RediSearch is a full-text search solution for Redis."
OK
127.0.0.1:6379> FT.ADD myIndex doc2 1.0 FIELDS title "Redis Streams" body "Redis Streams is a new data type introduced in Redis 5.0."
OK
```

이 예에서는 "제목"과 "본문"이라는 두 개의 텍스트 필드가 있는 "myIndex"라는 인덱스를 생성합니다. 그런 다음 각각 고유 ID와 1.0 점수를 가진 두 개의 문서를 인덱스에 추가합니다.

인덱스를 검색하려면 FT.SEARCH 명령을 사용할 수 있습니다. 다음은 "Redis"라는 단어가 포함된 문서에 대해 "myIndex" 인덱스를 검색하는 방법의 예입니다.

```redis
127.0.0.1:6379> FT.SEARCH myIndex "Redis"
1) (integer) 2
2) "doc2"
3) 1) "title"
   2) "Redis Streams"
   3) "body"
   4) "Redis Streams is a new data type introduced in Redis 5.0."
4) "doc1"
5) 1) "title"
   2) "Redis RediSearch"
   3) "body"
   4) "Redis RediSearch is a full-text search solution for Redis."
```

이 예에서 검색 쿼리는 "Redis"라는 단어가 포함된 두 개의 문서를 반환합니다. 문서는 관련성 순으로 순위가 매겨지며 가장 관련성이 높은 문서가 먼저 나열됩니다.

## 결론

RediSearch는 Redis를 위한 강력하고 효율적인 전체 텍스트 검색 솔루션입니다. 데이터를 빠르게 검색하고 검색해야 하는 애플리케이션을 위한 훌륭한 검색 엔진이 되는 몇 가지 기능을 제공합니다. RediSearch는 구성 및 배포가 쉬우며 다른 Redis 모듈과 함께 사용하여 강력한 데이터 파이프라인을 생성할 수 있습니다.

이미 Redis를 사용하고 있는 경우 RediSearch를 애플리케이션에 통합하면 귀중한 전체 텍스트 검색 기능을 추가할 수 있습니다. 빠른 성능과 강력한 검색 기능을 갖춘 RediSearch는 데이터를 빠르게 검색하고 검색해야 하는 모든 애플리케이션에 탁월한 선택입니다.

## 외부 리소스

- [레디서치 문서](https://oss.redislabs.com/redisearch/)
- [레디스 문서](https://redis.io/documentation)
- [Redis Gears: Redis용 서버리스 엔진](https://redisgears.io/)