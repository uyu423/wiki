---
title: 데이터 캐싱 및 관리를 위해 Redis와 함께 TypeScript 사용
description: 
published: true
date: 2023-02-24T11:32:50.388Z
tags: 
editor: markdown
dateCreated: 2023-02-24T11:32:43.391Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Using TypeScript with Redis for Data Caching and Management***English** document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-redis-for-data-caching-and-management)
{.links-list}



# 데이터 캐싱 및 관리를 위해 Redis와 함께 TypeScript 사용

TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. TypeScript가 기존 JavaScript 코드를 이해할 수 있도록 기존 JavaScript 라이브러리의 유형 정보를 포함할 수 있는 정의 파일을 지원합니다.

Redis는 데이터베이스, 캐시 및 메시지 브로커로 사용되는 오픈 소스 인 메모리 데이터 구조 저장소입니다. 문자열, 해시, 목록, 집합, 범위 쿼리가 포함된 정렬된 집합, 비트맵, 하이퍼로그 및 반경 쿼리가 포함된 지리 공간 인덱스와 같은 데이터 구조를 지원합니다.

이 기사에서는 Redis와 함께 TypeScript를 사용하여 데이터를 캐시하고 효과적으로 관리하는 방법을 보여줍니다. 다음 주제를 다룹니다.

- 필요한 도구 설치
- TypeScript 설정
- TypeScript를 사용하여 Redis에서 데이터 캐싱
- Redis에서 데이터 검색
- Redis에서 데이터 삭제
- Redis에서 데이터 업데이트

## 필요한 도구 설치

시작하기 전에 다음 도구를 설치해야 합니다.

- [Node.js](https://nodejs.org/en/)
- [레디스](https://redis.io/)

## TypeScript 설정

이제 필요한 도구가 설치되었으므로 TypeScript를 설정할 수 있습니다. 먼저 TypeScript 컴파일러를 설치해야 합니다.

```
npm install -g typescript
```

TypeScript 컴파일러가 설치되면 `.ts` 파일을 만들고 코드 작성을 시작할 수 있습니다. 이 기사에서는 파일 이름을 `redis.ts`로 지정합니다.

## Redis에서 TypeScript로 데이터 캐싱

Redis에서 `SET` 명령을 사용하여 데이터를 캐시할 수 있습니다. `SET` 명령은 키와 값을 인수로 사용합니다. 값은 문자열, 정수 또는 부동 소수점 숫자일 수 있습니다.

`redis.ts` 파일에서 사용자의 ID와 이름을 캐시합니다.

```typescript
let userId: number = 1;
let userName: string = "John Doe";

redis.set("user:id", userId);
redis.set("user:name", userName);
```

## Redis에서 데이터 가져오기

Redis에서 `GET` 명령을 사용하여 데이터를 검색할 수 있습니다. `GET` 명령은 키를 인수로 사용하고 키 값을 반환합니다.

`redis.ts` 파일에서 사용자의 ID와 이름을 검색합니다.

```typescript
let userId: number = redis.get("user:id");
let userName: string = redis.get("user:name");
```

## Redis에서 데이터 삭제

Redis에서 `DEL` 명령을 사용하여 데이터를 삭제할 수 있습니다. 'DEL' 명령은 하나 이상의 키를 인수로 사용하고 삭제된 키 수를 반환합니다.

`redis.ts` 파일에서 사용자의 ID와 이름을 삭제합니다.

```typescript
redis.del("user:id");
redis.del("user:name");
```

## Redis에서 데이터 업데이트

Redis에서 `SET` 명령을 사용하여 데이터를 업데이트할 수 있습니다. `SET` 명령은 키와 값을 인수로 사용합니다. 값은 문자열, 정수 또는 부동 소수점 숫자일 수 있습니다.

`redis.ts` 파일에서 사용자 이름을 업데이트합니다.

```typescript
let userName: string = "Jane Doe";

redis.set("user:name", userName);
```

## 결론

이 기사에서는 Redis와 함께 TypeScript를 사용하여 데이터를 캐시하고 효과적으로 관리하는 방법을 보여주었습니다. 우리는 다음 주제를 다루었습니다.

- 필요한 도구 설치
- TypeScript 설정
- TypeScript를 사용하여 Redis에서 데이터 캐싱
- Redis에서 데이터 검색
- Redis에서 데이터 삭제
- Redis에서 데이터 업데이트

TypeScript 또는 Redis에 대해 자세히 알아보려면 아래에 몇 가지 리소스가 포함되어 있습니다.

## 자원

- [TypeScript 설명서](https://www.typescriptlang.org/docs/handbook/basic-types.html)
- [레디스 문서](https://redis.io/documentation)