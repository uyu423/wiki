---
title: Redis Lua 스크립팅: 고급 Redis 명령 빌드
description: 
published: true
date: 2023-03-04T20:32:36.492Z
tags: 
editor: markdown
dateCreated: 2023-03-04T20:32:29.167Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Redis Lua Scripting: Building More Advanced Redis Commands***English** document is available*](/en/Knowledge-base/NoSQL/redis-lua-scripting-building-more-advanced-redis-commands)
{.links-list}


Redis Lua 스크립팅: 고급 Redis 명령 빌드

Redis는 고성능 데이터베이스를 제공하는 오픈 소스 인 메모리 데이터 구조 저장소입니다. Redis Lua 스크립팅은 Redis 명령을 확장하는 데 사용되는 서버 측 스크립팅 언어입니다. 이를 통해 개발자는 단일 트랜잭션에서 여러 Redis 작업을 실행할 수 있는 사용자 지정 원자 명령을 만들 수 있습니다. Redis Lua 스크립팅을 사용하여 데이터 처리 속도를 높이고, 복잡한 논리를 구현하고, Redis 핵심 명령에서 사용할 수 없는 사용자 지정 명령을 만들 수 있습니다.

## Redis Lua 스크립팅 시작하기

Redis Lua 스크립팅은 Redis 버전 2.6 이상에서 지원됩니다. Redis Lua 스크립팅을 사용하려면 Redis를 설치하고 실행해야 합니다. 그런 다음 Redis CLI를 사용하여 Lua 스크립트를 실행할 수 있습니다.

Lua 스크립트를 실행하려면 `EVAL` 명령 다음에 Lua 스크립트와 스크립트에 전달된 인수의 수를 사용하십시오. 예를 들어,

```redis
EVAL "return 'Hello, World!'" 0
```

이 스크립트는 문자열 "Hello, World!"를 반환합니다.

## Redis Lua 스크립트 작성

Redis Lua 스크립트는 실행을 위해 Redis 서버로 전달되는 Lua 코드를 포함하는 문자열입니다. Redis Lua 스크립팅은 기본 데이터 유형, 제어 구조 및 기능을 포함하는 Lua 언어의 하위 집합을 사용합니다. Redis Lua 스크립트는 문자열, 목록, 집합 및 해시 테이블과 같은 Redis 데이터 구조에 액세스할 수 있습니다.

Redis 데이터 구조에 액세스하기 위해 Redis Lua 스크립트는 `redis.call()` 및 `redis.pcall()`과 같은 Redis Lua API 함수를 사용합니다. `redis.call()` 함수는 Redis 명령을 실행하는 데 사용되는 반면 `redis.pcall()`은 스크립트가 오류를 처리하고 오류 메시지를 반환할 수 있는 보호 모드에서 Redis 명령을 실행하는 데 사용됩니다.

Redis Lua 스크립트는 런타임 시 스크립트에 전달되는 인수를 정의할 수도 있습니다. 인수는 'ARGV' Lua 전역 변수를 사용하여 액세스합니다. 예를 들어,

```redis
EVAL "return ARGV[1] + ARGV[2]" 0 2 3
```

이 스크립트는 두 개의 인수를 더한 결과인 5를 반환합니다.

## 사용자 지정 Redis 명령 빌드

Redis Lua 스크립팅은 Redis 핵심 명령에서 사용할 수 없는 사용자 지정 Redis 명령을 빌드하는 데 사용할 수 있습니다. 사용자 지정 Redis 명령을 빌드하려면 원하는 작업을 수행하는 Lua 함수를 정의한 다음 `redis.register_script()` 함수를 사용하여 해당 함수를 Redis 명령으로 등록할 수 있습니다.

예를 들어 다음 Redis Lua 스크립트는 Redis 키 값을 지정된 양만큼 증가시키고 새 값을 반환하는 'INCRBYX'라는 사용자 지정 Redis 명령을 정의합니다.

```redis
local key = KEYS[1]
local increment = tonumber(ARGV[1])

local current_value = tonumber(redis.call('get', key)) or 0
local new_value = current_value + increment

redis.call('set', key, new_value)
return new_value
```

이 사용자 지정 Redis 명령을 사용하려면 스크립트의 해시를 인수로 사용하는 `EVALSHA` 명령을 사용하여 호출할 수 있습니다.

```redis
EVALSHA <script hash> 1 <key> <increment>
```

## Redis Lua 스크립팅의 장점

Redis Lua 스크립팅은 기존 Redis 명령에 비해 몇 가지 이점을 제공합니다.

### 원자성

Redis Lua 스크립팅은 원자성을 제공합니다. 즉, Lua 스크립트 내의 Redis 명령이 단일 원자 트랜잭션으로 실행됩니다. 이렇게 하면 스크립트 실행에 실패하더라도 Redis 데이터 구조가 일관성 없는 상태로 남아 있지 않습니다.

### 성능

Redis Lua 스크립팅을 사용하면 클라이언트와 Redis 서버 간의 네트워크 왕복 횟수를 줄여 데이터 처리 속도를 높일 수 있습니다. 이는 Redis Lua 스크립트가 단일 트랜잭션에서 여러 Redis 명령을 실행하여 네트워크 통신의 오버헤드를 줄일 수 있기 때문입니다.

### 유연성

Redis Lua 스크립팅은 개발자가 복잡한 논리를 구현하고 Redis 핵심 명령에서 사용할 수 없는 사용자 지정 Redis 명령을 생성할 수 있으므로 유연성을 제공합니다. 이를 통해 개발자는 Redis를 특정 요구 사항에 맞게 조정할 수 있습니다.

## 결론

Redis Lua 스크립팅은 고급 Redis 명령을 빌드하기 위한 강력한 도구입니다. 원자성, 성능 및 유연성을 제공하며 데이터 처리 속도를 높이고 복잡한 논리를 구현하고 사용자 지정 Redis 명령을 만드는 데 사용할 수 있습니다. Redis Lua 스크립팅에는 Lua 프로그래밍 언어에 대한 약간의 지식이 필요하지만 향상된 기능 및 성능 측면에서 상당한 이점을 제공합니다.

## 외부 리소스

- [Redis Lua 스크립팅](https://redis.io/commands/eval)
- [루아 프로그래밍 언어](https://www.lua.org/manual/5.1/)
- [Redis의 Lua 스크립팅 소개](https://www.sitepoint.com/introduction-to-lua-scripting-in-redis/)