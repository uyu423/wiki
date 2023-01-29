---
title: Nest.js에서 Redis 사용
description: 
published: true
date: 2023-01-29T20:16:32.674Z
tags: 
editor: markdown
dateCreated: 2023-01-29T20:14:53.446Z
---

- [Using Redis in Nest.js***English** version of this document is available*](/en/Knowledge-base/Backend/using-redis-in-nest-js)
{.links-list}

# Nest.js에서 Redis 사용

Nest.js는 효율적이고 확장 가능한 Node.js 서버 측 애플리케이션을 구축하기 위한 프레임워크입니다. 최신 JavaScript를 사용하고 TypeScript(순수 JavaScript와의 호환성 유지)로 구축되었으며 OOP(Object Oriented Programming), FP(Functional Programming) 및 FRP(Functional Reactive Programming)의 요소를 결합합니다. 내부적으로 Nest.js는 Express.js를 사용하지만 대안으로 Fastify를 사용할 수도 있습니다.

Redis는 데이터베이스, 캐시 및 메시지 브로커로 사용되는 오픈 소스(BSD 라이센스), 메모리 내 데이터 구조 저장소입니다. 문자열, 해시, 목록, 집합, 범위 쿼리가 있는 정렬된 집합, 비트맵, 하이퍼로그 및 반경 쿼리가 있는 지리 공간 인덱스와 같은 데이터 구조를 지원합니다. Redis는 기본 제공 복제, Lua 스크립팅, LRU 제거, 트랜잭션 및 다양한 수준의 온디스크 지속성을 갖추고 있으며 Redis Sentinel을 통한 고가용성 및 Redis 클러스터를 통한 자동 파티셔닝을 제공합니다.

## Nest.js와 함께 Redis를 사용하는 이유는 무엇인가요?

Nest.js는 효율적이고 확장 가능한 서버 측 애플리케이션을 구축하기 위한 훌륭한 프레임워크입니다. 그러나 데이터 작업과 관련하여 Nest.js는 가장 효율적인 솔루션이 아닙니다. Redis가 들어오는 곳입니다.

Redis는 MySQL과 같은 기존 데이터베이스를 사용하는 것보다 훨씬 빠른 메모리 내 데이터 구조 저장소입니다. 또한 복제 및 고가용성 기능이 내장되어 있습니다. Nest.js와 함께 Redis를 사용하면 애플리케이션의 성능을 개선하고 확장성을 높일 수 있습니다.

## Redis를 Nest.js와 함께 사용하는 방법은 무엇인가요?

Nest.js와 함께 Redis를 사용하는 방법에는 두 가지가 있습니다.

1. @nestjs/redis 모듈을 사용합니다.

2. redis 패키지를 사용합니다.

### @nestjs/redis 모듈 사용

@nestjs/redis 모듈은 Redis 패키지를 Nest.js와 함께 쉽게 사용할 수 있도록 해주는 래퍼입니다. @nestjs/redis 모듈을 사용하려면 먼저 설치해야 합니다.

```
npm install @nestjs/redis
```

모듈이 설치되면 RedisModule을 가져와 Nest.js 애플리케이션에서 사용할 수 있습니다.

```javascript
import { Module } from '@nestjs/common';
import { RedisModule } from '@nestjs/redis';

@Module({
  imports: [
    RedisModule.forRoot({
      host: 'localhost',
      port: 6379,
    }),
  ],
})
export class AppModule {}
```

위의 예에서는 로컬 Redis 인스턴스를 사용하도록 RedisModule을 구성하고 있습니다. Redis 인스턴스가 비밀번호로 보호되는 경우 비밀번호를 지정할 수도 있습니다.

RedisModule을 가져오면 RedisService를 Nest.js 구성 요소에 삽입할 수 있습니다.

```javascript
import { Component } from '@nestjs/common';
import { RedisService } from '@nestjs/redis';

@Component()
export class SomeComponent {
  constructor(private readonly redisService: RedisService) {}

  someMethod() {
    this.redisService.set('some key', 'some value');
  }
}
```

RedisService는 모든 Redis 명령에 대한 메서드를 제공합니다. 전체 명령어 목록은 [Redis 문서](https://redis.io/documentation)를 참조하세요.

### redis 패키지 사용

@nestjs/redis 모듈을 사용하지 않으려면 redis 패키지를 직접 사용할 수 있습니다. redis 패키지를 사용하려면 먼저 설치해야 합니다.

```
npm install redis
```

패키지가 설치되면 redis 패키지를 가져와 Nest.js 애플리케이션에서 사용할 수 있습니다.

```javascript
import * as redis from 'redis';

const client = redis.createClient({
  host: 'localhost',
  port: 6379,
});

client.set('some key', 'some value');
```

위의 예에서는 Redis 클라이언트를 생성하고 이를 사용하여 키/값 쌍을 설정합니다. 전체 명령 목록은 [redis 패키지 설명서](https://www.npmjs.com/package/redis)를 참조하세요.

## 결론

이 기사에서는 Redis를 Nest.js와 함께 사용하는 방법을 살펴보았습니다. 또한 Redis를 Nest.js와 함께 사용하는 두 가지 다른 방법, 즉 @nestjs/redis 모듈을 사용하거나 redis 패키지를 직접 사용하는 방법도 살펴보았습니다.