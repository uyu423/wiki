---
title: Redis JSON 데이터 구조: Redis에서 JSON 데이터 저장 및 쿼리
description: 
published: true
date: 2023-03-07T22:33:01.455Z
tags: 
editor: markdown
dateCreated: 2023-03-07T22:32:53.845Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Redis JSON Data Structures: Storing and Querying JSON Data in Redis***English** document is available*](/en/Knowledge-base/NoSQL/redis-json-data-structures-storing-and-querying-json-data-in-redis)
{.links-list}

Redis JSON 데이터 구조: Redis에서 JSON 데이터 저장 및 쿼리

Redis는 데이터베이스, 캐시 및 메시지 브로커로 사용할 수 있는 메모리 내 데이터 구조 저장소입니다. Redis JSON은 Redis에서 JSON 데이터 구조에 대한 기본 지원을 제공하는 모듈입니다. Redis JSON을 사용하면 Redis에서 JSON 데이터를 저장하고 쿼리하는 것이 그 어느 때보다 쉬워졌습니다.

이 기사에서는 Redis JSON 데이터 구조와 이를 사용하여 Redis에서 JSON 데이터를 저장하고 쿼리하는 방법을 살펴봅니다.

## 레디스 JSON이 무엇인가요?

Redis JSON은 Redis에서 JSON 데이터 구조에 대한 지원을 추가하는 Redis 모듈입니다. 직렬화 또는 역직렬화하지 않고도 Redis에서 JSON 데이터를 저장하고 쿼리할 수 있습니다.

Redis JSON 모듈은 JSON 데이터 구조를 조작하는 데 사용할 수 있는 일련의 명령을 제공합니다. 이러한 명령을 사용하면 Redis에서 JSON 데이터를 저장, 검색, 업데이트 및 삭제할 수 있습니다.

## Redis JSON 데이터 구조

Redis JSON 데이터 구조를 사용하면 JSON 데이터를 Redis에 기본 데이터 유형으로 저장할 수 있습니다. Redis JSON 모듈은 두 가지 유형의 JSON 데이터 구조를 지원합니다.

- JSON 객체
- JSON 배열

### JSON 객체

JSON 개체는 키-값 쌍의 모음입니다. Redis JSON에서 JSON 개체는 Redis 해시로 저장됩니다. JSON 개체의 각 키-값 쌍은 Redis 해시에 필드-값 쌍으로 저장됩니다.

Redis에 JSON 객체를 저장하려면 `JSON.SET` 명령을 사용할 수 있습니다. 다음 예는 `JSON.SET` 명령을 사용하여 Redis에 JSON 객체를 저장하는 방법을 보여줍니다.

```{python}
JSON.SET user:id1234 '{"name":"John Doe","email":"johndoe@example.com"}'
```

위의 예에서는 Redis에서 사용자를 나타내는 JSON 개체를 저장하고 있습니다. JSON 객체에는 '이름'과 '이메일'이라는 두 개의 키-값 쌍이 있습니다. `JSON.SET` 명령은 이 JSON 개체를 Redis에 `user:id1234` 키가 있는 해시로 저장하는 데 사용됩니다.

Redis에서 JSON 개체를 검색하려면 `JSON.GET` 명령을 사용할 수 있습니다. 다음 예는 `JSON.GET` 명령을 사용하여 이전에 저장한 JSON 개체를 검색하는 방법을 보여줍니다.

```{python}
JSON.GET user:id1234
```

위의 예에서 `JSON.GET` 명령은 이전에 저장한 JSON 개체를 검색하는 데 사용됩니다. 명령의 출력은 문자열로 된 JSON 개체입니다.

### JSON 배열

JSON 배열은 정렬된 값 목록입니다. Redis JSON에서 JSON 배열은 Redis 목록으로 저장됩니다. JSON 배열의 각 값은 Redis 목록의 요소로 저장됩니다.

Redis에 JSON 배열을 저장하려면 `JSON.SET` 명령을 사용할 수 있습니다. 다음 예제는 `JSON.SET` 명령을 사용하여 Redis에 JSON 배열을 저장하는 방법을 보여줍니다.

```{python}
JSON.SET users '["John Doe","Jane Doe","Bob Smith"]'
```

위의 예에서는 Redis의 사용자 목록을 나타내는 JSON 배열을 저장하고 있습니다. JSON 배열에는 `John Doe`, `Jane Doe` 및 `Bob Smith`의 세 가지 값이 있습니다. `JSON.SET` 명령은 이 JSON 배열을 Redis에 `users` 키가 있는 목록으로 저장하는 데 사용됩니다.

Redis에서 JSON 배열을 검색하려면 `JSON.GET` 명령을 사용할 수 있습니다. 다음 예는 `JSON.GET` 명령을 사용하여 이전에 저장한 JSON 배열을 검색하는 방법을 보여줍니다.

```{python}
JSON.GET users
```

위의 예에서 `JSON.GET` 명령은 이전에 저장한 JSON 배열을 검색하는 데 사용됩니다. 명령의 출력은 문자열로 된 JSON 배열입니다.

## Redis JSON 데이터 구조 쿼리

Redis JSON은 Redis에서 JSON 데이터 구조를 쿼리하는 데 사용할 수 있는 일련의 명령을 제공합니다. 이러한 명령을 사용하면 JSON 데이터 구조에서 특정 값을 검색하고 검색할 수 있습니다.

### JSON.GET

`JSON.GET` 명령은 Redis에서 JSON 객체 또는 JSON 배열을 검색하는 데 사용할 수 있습니다. 이 명령은 키를 인수로 사용하고 JSON 데이터 구조를 문자열로 반환합니다.

### JSON.MGET

'JSON.MGET' 명령을 사용하여 Redis에서 여러 JSON 개체 또는 JSON 배열을 검색할 수 있습니다. 이 명령은 여러 키를 인수로 사용하고 JSON 데이터 구조를 문자열 배열로 반환합니다.

### JSON.유형

'JSON.TYPE' 명령은 Redis에서 JSON 데이터 구조의 유형을 결정하는 데 사용할 수 있습니다. 이 명령은 키를 인수로 사용하고 JSON 데이터 구조의 유형을 문자열(`object` 또는 `array`)로 반환합니다.

### JSON.NUMBEROF

'JSON.NUMBEROF' 명령은 Redis에서 JSON 배열의 요소 수를 검색하는 데 사용할 수 있습니다. 이 명령은 키를 인수로 사용하고 요소 수를 정수로 반환합니다.

### JSON.ARRINDEX

`JSON.ARRINDEX` 명령은 Redis에서 JSON 배열의 값 인덱스를 검색하는 데 사용할 수 있습니다. 이 명령은 키, 값 및 선택적 시작 인덱스를 인수로 사용하고 값의 인덱스를 정수로 반환합니다.

### JSON.OBJKEYS

`JSON.OBJKEYS` 명령은 Redis에서 JSON 개체의 키를 검색하는 데 사용할 수 있습니다. 이 명령은 키를 인수로 사용하고 키를 문자열 배열로 반환합니다.

### JSON.OBJLEN

`JSON.OBJLEN` 명령은 Redis에서 JSON 개체의 필드 수를 검색하는 데 사용할 수 있습니다. 이 명령은 키를 인수로 사용하고 필드 수를 정수로 반환합니다.

### JSON.OBJKEYEXISTS

'JSON.OBJKEYEXISTS' 명령을 사용하여 Redis의 JSON 개체에 키가 있는지 확인할 수 있습니다. 이 명령은 키와 필드를 인수로 사용하고 필드가 있으면 'true'를 반환하고 그렇지 않으면 'false'를 반환합니다.

## 결론

Redis JSON은 Redis에서 JSON 데이터 구조에 대한 기본 지원을 제공하는 강력한 모듈입니다. 직렬화 또는 역직렬화하지 않고도 Redis에서 JSON 데이터를 저장하고 쿼리할 수 있습니다. Redis JSON 데이터 구조를 사용하면 JSON 데이터를 Redis에 기본 데이터 유형으로 저장할 수 있으므로 Redis에서 JSON 데이터를 쉽게 조작할 수 있습니다.

이 기사가 Redis JSON 데이터 구조와 Redis에서 JSON 데이터를 저장하고 쿼리하는 데 사용되는 방법에 대한 좋은 이해를 제공했기를 바랍니다.

## 외부 리소스

- [Redis JSON 문서](https://redislabs.com/redis-json/)
- [Redis JSON API 참조](https://oss.redislabs.com/redisjson/commands/)
- [레디스 문서](https://redis.io/documentation)