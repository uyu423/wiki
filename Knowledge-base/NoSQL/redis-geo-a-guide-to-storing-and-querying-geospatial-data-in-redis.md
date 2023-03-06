---
title: Redis Geo: Redis에서 지리 공간 데이터를 저장하고 쿼리하기 위한 가이드
description: 
published: true
date: 2023-03-06T13:32:32.665Z
tags: 
editor: markdown
dateCreated: 2023-03-06T13:32:32.665Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Redis Geo: A Guide to Storing and Querying Geospatial Data in Redis***English** document is available*](/en/Knowledge-base/NoSQL/redis-geo-a-guide-to-storing-and-querying-geospatial-data-in-redis)
{.links-list}

Redis Geo: Redis에서 지리 공간 데이터를 저장하고 쿼리하기 위한 가이드

Redis는 캐싱 및 기타 애플리케이션에 널리 사용되는 키-값 저장소입니다. Redis는 높은 성능과 확장성으로 유명합니다. Redis Geo는 지리 공간 데이터를 저장하고 쿼리할 수 있는 Redis에서 사용할 수 있는 모듈입니다. 이 가이드에서는 Redis Geo 모듈과 이를 사용하여 Redis에서 지리 공간 데이터를 저장하고 쿼리하는 방법을 살펴봅니다.

## 레디스 지오란?

Redis Geo는 지리 공간 인덱싱 및 쿼리 기능을 제공하는 Redis에서 사용할 수 있는 모듈입니다. 지도에 포인트를 저장하고 조회할 수 있으며, 주어진 포인트에서 일정 거리 내에 있는 포인트를 검색할 수 있습니다. Redis Geo는 Haversine 공식을 사용하여 지구 표면의 지점 간 거리를 계산합니다.

## Redis Geo 사용 방법

Redis Geo를 사용하려면 Redis에서 모듈을 활성화해야 합니다. Redis 구성 파일에 다음 줄을 추가하여 이 작업을 수행할 수 있습니다.

```
# Load the Redis Geo module
loadmodule /path/to/redis-geo.so
```

모듈을 활성화하면 Redis Geo 명령을 사용하여 지리 공간 데이터를 저장하고 쿼리할 수 있습니다.

### 지리 공간 데이터 저장

Redis에 공간 데이터를 저장하려면 `GEOADD` 명령을 사용해야 합니다. `GEOADD` 명령은 키 이름, 경도, 위도 및 구성원 이름을 인수로 사용합니다. 다음은 예입니다.

```redis
GEOADD cities -122.4194 37.7749 SanFrancisco
```

이 예에서는 경도 및 위도 좌표가 각각 -122.4194 및 37.7749인 샌프란시스코 시를 저장하고 있습니다. 키 이름은 "cities"이고 구성원 이름은 "SanFrancisco"입니다.

한 번에 여러 포인트를 저장할 수도 있습니다. 다음은 예입니다.

```redis
GEOADD cities -122.4194 37.7749 SanFrancisco -118.2437 34.0522 LosAngeles
```

이 예에서는 샌프란시스코와 로스앤젤레스의 도시를 저장하고 있습니다.

### 지리 공간 데이터 쿼리

Redis에서 지리 공간 데이터를 쿼리하려면 `GEORADIUS` 명령을 사용해야 합니다. `GEORADIUS` 명령은 키 이름, 경도, 위도, 반지름 및 단위를 인수로 사용합니다. 다음은 예입니다.

```redis
GEORADIUS cities -122.4194 37.7749 1000 km
```

이 예에서는 지점(-122.4194, 37.7749)에서 반경 1000km 이내의 도시를 쿼리합니다. 키 이름은 "도시"입니다.

`GEORADIUS` 명령은 지정된 지점으로부터의 거리를 기준으로 정렬된 순서로 지정된 반경 내에 있는 멤버를 반환합니다. 반환할 결과 수 및 결과에 구성원의 좌표를 포함할지 여부와 같은 추가 옵션을 지정할 수도 있습니다.

## 결론

Redis Geo는 Redis에서 지리 공간적 인덱싱 및 쿼리 기능을 제공하는 강력한 모듈입니다. Redis Geo를 사용하면 지리 공간 데이터를 쉽게 저장하고 쿼리할 수 있습니다. Redis Geo는 사용하기 쉽고 고성능과 확장성을 제공합니다. Redis에서 지리 공간 데이터로 작업하는 경우 Redis Geo는 확실히 확인할 가치가 있습니다.

## 외부 리소스

- [Redis Geo 공식 문서](https://redis.io/commands# geo)
- [Redis Geo 튜토리얼](https://www.tutorialspoint.com/redis/redis_geo.htm)
- [Redis Geo 예시](https://github.com/RedisLabs/redis-geo)