---
title: Redis 키-값 저장소: 기본 사항 이해
description: 
published: true
date: 2023-03-04T17:32:33.861Z
tags: 
editor: markdown
dateCreated: 2023-03-04T17:32:32.429Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Redis Key-Value Store: Understanding the Basics***English** document is available*](/en/Knowledge-base/NoSQL/redis-key-value-store-understanding-the-basics)
{.links-list}
Redis 키-값 저장소: 기본 사항 이해

Redis는 데이터베이스, 캐시 및 메시지 브로커로 사용되는 오픈 소스 메모리 내 데이터 구조 저장소입니다. 단순성, 속도 및 유연성으로 인해 개발자에게 인기 있는 선택입니다. Redis는 데이터를 키-값 쌍으로 저장하여 키-값 저장소로 만듭니다. 이 기사에서는 Redis 키-값 저장소의 기본 사항, 해당 데이터 유형 및 애플리케이션에서 이를 사용하는 방법에 대해 설명합니다.

## 키-값 저장소란?

키-값 저장소는 키-값 쌍의 형태로 데이터를 저장하는 데이터베이스 유형입니다. 키는 해당 값을 검색하는 데 사용되는 고유 식별자입니다. 이 유형의 데이터베이스는 일반적으로 캐싱, 세션 관리 및 데이터에 대한 빠른 액세스가 필요한 기타 애플리케이션에 사용됩니다.

## 레디스란?

Redis는 빠르고 확장 가능하며 사용하기 쉽게 설계된 키-값 저장소입니다. 메모리 내 데이터베이스로 모든 데이터가 메모리에 저장되어 기존 디스크 기반 데이터베이스보다 훨씬 빠릅니다. Redis는 캐시, 메시지 브로커, 완전한 데이터베이스로도 사용할 수 있습니다.

## Redis 데이터 유형

Redis는 다양한 유형의 데이터를 저장하는 데 사용할 수 있는 여러 데이터 유형을 지원합니다. 이러한 데이터 유형에는 다음이 포함됩니다.

### 문자열

문자열은 Redis에서 가장 단순한 데이터 유형이며 문자열, 정수 및 부동 소수점 숫자를 저장할 수 있습니다. 문자열의 크기는 최대 512MB까지 가능하므로 많은 양의 데이터를 저장하는 데 적합합니다.

Redis에서 문자열 값을 설정하려면 다음 명령을 사용합니다.

```
SET key value
```

문자열 값을 검색하려면 다음 명령을 사용하십시오.

```
GET key
```

### 목록

목록은 추가된 순서대로 저장되는 문자열 모음입니다. 큐, 스택 및 기타 데이터 구조를 구현하는 데 사용할 수 있습니다. 목록에는 최대 40억 개의 요소가 포함될 수 있습니다.

목록에 요소를 추가하려면 다음 명령을 사용하십시오.

```
RPUSH key value
```

목록의 요소를 검색하려면 다음 명령을 사용하십시오.

```
LRANGE key start stop
```

### 세트

세트는 고유한 문자열의 모음입니다. 태그, 사용자 그룹 및 기타 유사한 구조를 구현하는 데 사용할 수 있습니다. 세트는 최대 40억 개의 요소를 포함할 수 있습니다.

세트에 요소를 추가하려면 다음 명령을 사용하십시오.

```
SADD key value
```

세트의 요소를 검색하려면 다음 명령을 사용하십시오.

```
SMEMBERS key
```

### 해시

해시는 키-값 쌍의 모음입니다. 개체, 사용자 프로필 및 기타 유사한 구조를 저장하는 데 사용할 수 있습니다. 해시는 최대 40억 개의 필드-값 쌍을 포함할 수 있습니다.

해시 필드의 값을 설정하려면 다음 명령을 사용하십시오.

```
HSET key field value
```

해시 필드의 값을 검색하려면 다음 명령을 사용하십시오.

```
HGET key field
```

### 정렬된 세트

정렬된 세트는 일반 세트와 같지만 각 요소는 점수와 연결됩니다. 순위표, 순위 및 기타 유사한 구조를 구현하는 데 사용할 수 있습니다. 정렬된 세트는 최대 40억 개의 요소를 포함할 수 있습니다.

정렬된 세트에 요소를 추가하려면 다음 명령을 사용하십시오.

```
ZADD key score value
```

정렬된 집합의 요소를 검색하려면 다음 명령을 사용합니다.

```
ZRANGE key start stop
```

## 애플리케이션에서 Redis 사용

애플리케이션에서 Redis를 사용하려면 먼저 시스템에 Redis를 설치해야 합니다. Redis는 Linux, macOS 및 Windows에 설치할 수 있습니다. Redis가 설치되면 Redis 클라이언트 라이브러리 중 하나를 사용하여 선택한 프로그래밍 언어로 Redis와 상호 작용할 수 있습니다.

다음은 Python에서 Redis를 사용하는 방법의 예입니다.

```python
import redis

# Connect to Redis
r = redis.Redis(host='localhost', port=6379, db=0)

# Set a string value
r.set('mykey', 'Hello World!')

# Get the string value
value = r.get('mykey')
print(value)
```

이 예에서는 먼저 Redis 라이브러리를 가져오고 로컬 시스템에서 실행 중인 Redis에 연결합니다. 그런 다음 Redis에서 문자열 값을 설정하고 해당 값을 검색합니다. 마지막으로 문자열의 값을 인쇄합니다.

## 결론

Redis는 속도, 단순성 및 유연성 때문에 전 세계 개발자가 사용하는 인기 있는 키-값 저장소입니다. Redis는 다양한 유형의 데이터를 저장하는 데 사용할 수 있는 여러 데이터 유형을 지원하며 캐시, 메시지 브로커 및 본격적인 데이터베이스로도 사용할 수 있습니다. 애플리케이션에서 Redis를 사용하면 애플리케이션의 성능과 확장성을 개선하고 사용자에게 더 나은 사용자 경험을 제공할 수 있습니다.

## 외부 리소스

- [Redis 공식 문서](https://redis.io/documentation)
- [레디스랩스](https://redislabs.com/)
- Baeldung의 [Redis 데이터 유형 소개](https://www.baeldung.com/redis-data-types)
- [Redis: 기초 이해하기](https://www.sitepoint.com/redis-understanding-the-basics/) by SitePoint