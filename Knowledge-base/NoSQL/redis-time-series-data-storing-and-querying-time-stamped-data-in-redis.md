---
title: Redis 시계열 데이터: Redis에서 타임스탬프 데이터 저장 및 쿼리
description: 
published: true
date: 2023-03-12T10:32:54.471Z
tags: 
editor: markdown
dateCreated: 2023-03-12T10:32:54.471Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Redis Time-Series Data: Storing and Querying Time-Stamped Data in Redis***English** document is available*](/en/Knowledge-base/NoSQL/redis-time-series-data-storing-and-querying-time-stamped-data-in-redis)
{.links-list}

Redis 시계열 데이터: Redis에서 타임스탬프 데이터 저장 및 쿼리

시계열 데이터는 연대순으로 구성된 데이터 요소의 모음입니다. 이러한 유형의 데이터는 금융, IoT, 건강 및 물류를 비롯한 다양한 산업에서 시간 경과에 따른 추세 및 패턴을 분석하는 데 일반적으로 사용됩니다. 이 기사에서는 Redis를 사용하여 타임스탬프가 있는 데이터를 효율적으로 저장하고 쿼리하는 방법을 살펴봅니다.

## 레디스란?

Redis는 데이터베이스, 캐시 및 메시지 브로커로 사용할 수 있는 메모리 내 데이터 구조 저장소입니다. 문자열, 해시, 목록, 세트 및 정렬된 세트를 포함한 광범위한 데이터 구조를 지원합니다. Redis는 속도, 단순성 및 유연성으로 유명하여 고성능 애플리케이션을 구축하는 데 널리 사용됩니다.

## 시계열 데이터에 Redis를 사용하는 이유는 무엇인가요?

Redis는 시계열 데이터를 저장하고 쿼리할 때 다음과 같은 몇 가지 이점을 제공합니다.

- **고성능:** Redis는 인메모리 스토리지에 최적화되어 있으며 초당 수백만 건의 작업을 처리할 수 있습니다. 따라서 대량의 시계열 데이터를 실시간으로 처리하는 데 이상적인 선택입니다.

- **효율적인 스토리지:** Redis는 데이터를 압축된 형식으로 저장하므로 메모리 사용량이 줄어듭니다. 이를 통해 시계열 데이터 저장 비용을 줄이고 비즈니스에 보다 비용 효율적입니다.

- **유연한 데이터 구조:** Redis는 정렬된 집합, 해시 및 목록을 포함하여 시계열 데이터를 저장하는 데 사용할 수 있는 여러 데이터 구조를 지원합니다. 이를 통해 개발자는 사용 사례에 가장 적합한 데이터 구조를 선택할 수 있습니다.

## Redis에 시계열 데이터를 저장하는 방법

Redis에 시계열 데이터를 저장하는 가장 일반적인 방법은 정렬된 세트를 사용하는 것입니다. 정렬된 집합은 각 요소가 점수와 연결된 고유한 요소의 모음입니다. Redis에서 점수는 데이터 포인트의 타임스탬프를 저장하는 데 사용할 수 있으며 요소는 데이터 값을 저장할 수 있습니다.

Redis에 시계열 데이터를 저장하려면 다음 단계를 따르세요.

1. 선택한 프로그래밍 언어로 Redis 클라이언트 인스턴스를 생성합니다. 예를 들어 Python에서는 Redis-py 라이브러리를 사용할 수 있습니다.

```python
import redis

r = redis.Redis(host='localhost', port=6379, db=0)
```

2. 'ZADD' 명령을 사용하여 정렬된 세트에 데이터 포인트를 추가합니다. `ZADD` 명령의 구문은 다음과 같습니다.

```python
r.zadd(key, {timestamp1: value1, timestamp2: value2, ...})
```

예를 들어 서로 다른 타임스탬프에서 센서의 온도 판독값을 저장하려면 다음 코드를 사용할 수 있습니다.

```python
r.zadd('temperature_sensor', {1622697600: 23, 1622697660: 24, 1622697720: 25})
```

이렇게 하면 타임스탬프 1622697600, 1622697660 및 1622697720에 각각 온도 판독값 23, 24 및 25가 추가됩니다.

## Redis에서 시계열 데이터를 쿼리하는 방법

Redis는 `ZRANGE`, `ZRANGEBYSCORE` 및 `ZREVRANGE`를 포함하여 시계열 데이터를 쿼리하기 위한 여러 명령을 제공합니다. 이러한 명령을 사용하면 특정 타임스탬프 범위 내에서 또는 특정 순서로 데이터 포인트를 검색할 수 있습니다.

Redis에서 시계열 데이터를 쿼리하려면 다음 단계를 따르세요.

1. 'ZRANGEBYSCORE' 명령을 사용하여 특정 타임스탬프 범위 내에서 데이터 포인트를 검색합니다. `ZRANGEBYSCORE` 명령의 구문은 다음과 같습니다.

```python
r.zrangebyscore(key, min_score, max_score, start=None, num=None, withscores=False, score_cast_func=float)
```

예를 들어 타임스탬프 1622697600과 1622697660 사이의 센서에 대한 온도 판독값을 검색하려면 다음 코드를 사용할 수 있습니다.

```python
r.zrangebyscore('temperature_sensor', 1622697600, 1622697660)
```

이렇게 하면 23과 24의 온도 판독값이 반환됩니다.

2. 'ZRANGE' 명령을 사용하여 특정 순서로 데이터 포인트를 검색합니다. `ZRANGE` 명령의 구문은 다음과 같습니다.

```python
r.zrange(key, start, end, desc=False, withscores=False, score_cast_func=float)
```

예를 들어 센서의 마지막 10개 온도 판독값을 검색하려면 다음 코드를 사용할 수 있습니다.

```python
r.zrange('temperature_sensor', -10, -1, withscores=True)
```

이렇게 하면 해당 타임스탬프와 함께 마지막 10개의 온도 판독값이 반환됩니다.

## 결론

Redis는 시계열 데이터를 저장하고 쿼리하는 빠르고 효율적이며 유연한 방법을 제공합니다. Redis의 정렬된 세트를 사용하여 개발자는 타임스탬프 데이터를 쉽게 저장하고 실시간으로 검색할 수 있습니다. Redis의 고성능 및 적은 메모리 공간은 대량의 시계열 데이터를 처리하는 데 이상적인 선택입니다.

## 외부 리소스

- [Redis 시계열 데이터 문서](https://redis.io/topics/timeseries)
- [Redis 시계열 튜토리얼](https://redislabs.com/blog/redis-time-series-tutorial/)
- [Redis-py 문서](https://redis-py.readthedocs.io/en/stable/)