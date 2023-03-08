---
title: Node.js 및 Redis: 캐싱 및 세션 관리에 대한 실습 가이드
description: 
published: true
date: 2023-01-31T05:36:53.780Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:36:52.028Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Node.js and Redis: A Hands-On Guide to Caching and Session Management***English** version of this document is available*](/en/Knowledge-base/Nodejs/node-js-and-redis-a-hands-on-guide-to-caching-and-session-management)
{.links-list}


# Node.js 및 Redis: 캐싱 및 세션 관리에 대한 실습 가이드

이 기사에서는 Node.js 및 Redis를 사용하여 데이터를 캐시하고 세션을 관리하는 방법을 살펴보겠습니다. 다음 주제를 다룹니다.

* 캐싱이란?
* 레디스란?
* Node.js와 Redis를 함께 사용하는 이유는 무엇입니까?
* Redis로 Node.js에서 데이터를 캐싱하는 방법
* Redis로 Node.js에서 세션을 관리하는 방법

## 캐싱이란?

캐싱은 원래 데이터 저장소보다 더 빠르게 액세스할 수 있는 위치에 자주 액세스하는 데이터를 저장하는 기술입니다. 데이터를 캐싱하면 데이터 저장소에 액세스하는 데 소요되는 시간을 줄여 애플리케이션의 성능을 향상시킬 수 있습니다.

캐싱에는 클라이언트 측 캐싱과 서버 측 캐싱의 두 가지 유형이 있습니다. 클라이언트 측 캐싱은 브라우저 캐시와 같은 클라이언트 시스템에 데이터를 저장합니다. 서버 측 캐싱은 서버에 데이터를 저장합니다.

이 기사에서는 Redis를 사용한 서버 측 캐싱에 중점을 둘 것입니다.

## 레디스란?

Redis는 데이터베이스, 캐시 또는 메시지 브로커로 사용할 수 있는 오픈 소스 메모리 내 데이터 저장소입니다. Redis는 C로 작성되었으며 Node.js를 포함한 여러 프로그래밍 언어를 지원합니다.

Redis는 키-값 저장소입니다. 즉, 키-값 쌍의 형태로 데이터를 저장합니다. 키를 사용하여 값을 검색할 수 있습니다. Redis는 문자열, 목록, 세트 및 해시를 포함한 다양한 데이터 유형을 지원합니다.

## Node.js와 Redis를 함께 사용하는 이유는 무엇인가요?

Node.js는 확장 가능한 서버측 애플리케이션을 구축하는 데 사용되는 JavaScript 런타임 환경입니다. Node.js는 빠르고 효율적이므로 데이터 집약적인 애플리케이션을 구축하는 데 적합합니다.

Redis는 Node.js 애플리케이션과 함께 사용하기에 적합한 빠르고 유연하며 강력한 데이터 저장소입니다. Redis는 데이터베이스, 캐시 또는 메시지 브로커로 사용할 수 있으며 Node.js를 포함한 여러 프로그래밍 언어를 지원합니다.

Node.js와 Redis는 빠르고 효율적이기 때문에 데이터 집약적인 애플리케이션을 구축하는 데 적합합니다.

## Redis로 Node.js에서 데이터를 캐싱하는 방법

이 섹션에서는 Redis를 사용하여 Node.js에서 데이터를 캐시하는 방법을 살펴보겠습니다. 다음 주제를 다룹니다.

* Node.js 프로젝트 설정
* Redis 서버에 연결
* 캐시 클라이언트 생성
* 캐시에 데이터 추가
* 캐시에서 데이터 가져오기
* 캐시에서 데이터 삭제

### Node.js 프로젝트 설정

먼저 Node.js 프로젝트를 설정해야 합니다. 프로젝트의 새 디렉터리를 만든 다음 프로젝트 디렉터리에 `app.js`라는 파일을 만듭니다.

`app.js` 파일에는 Redis 모듈이 필요합니다. Redis 서버에 대한 연결도 설정합니다.

```javascript
var redis = require("redis");
var client = redis.createClient();
```

### Redis 서버에 연결

다음으로 Redis 서버에 연결해야 합니다. Redis 모듈의 `createClient` 메서드를 호출하여 이를 수행합니다.

```javascript
var redis = require("redis");
var client = redis.createClient();
```

`createClient` 메서드는 `host` 및 `port`의 두 가지 인수를 허용합니다. `host` 인수는 Redis 서버의 호스트 이름 또는 IP 주소이고 `port` 인수는 Redis 서버의 포트 번호입니다.

로컬 머신에서 Redis를 실행 중인 경우 `host` 및 `port`에 기본값을 사용할 수 있습니다.

```javascript
var redis = require("redis");
var client = redis.createClient();
```

### 캐시 클라이언트 생성

이제 Redis 서버에 연결했으므로 캐시 클라이언트를 생성할 수 있습니다. Redis 모듈의 `createClient` 메서드를 호출하여 이를 수행합니다.

```javascript
var redis = require("redis");
var client = redis.createClient();

var cache = redis.createClient();
```

`createClient` 메서드는 `host` 및 `port`의 두 가지 인수를 허용합니다. `host` 인수는 Redis 서버의 호스트 이름 또는 IP 주소이고 `port` 인수는 Redis 서버의 포트 번호입니다.

로컬 머신에서 Redis를 실행 중인 경우 `host` 및 `port`에 기본값을 사용할 수 있습니다.

```javascript
var redis = require("redis");
var client = redis.createClient();

var cache = redis.createClient();
```

### 캐시에 데이터 추가

캐시 클라이언트가 있으면 캐시에 데이터를 추가할 수 있습니다. 캐시 클라이언트의 `set` 메서드를 호출하여 이를 수행합니다.

`set` 메서드는 `key`, `value` 및 `callback`의 세 가지 인수를 허용합니다. 'key' 인수는 캐시 항목의 키이고, 'value' 인수는 캐시 항목의 값이며, 'callback' 인수는 데이터가 캐시에 추가되었을 때 호출되는 함수입니다.

```javascript
var redis = require("redis");
var client = redis.createClient();

var cache = redis.createClient();

cache.set("key", "value", function(err, data) {
  if (err) {
    console.log(err);
  } else {
    console.log(data);
  }
});
```

위의 예에서는 캐시에 키-값 쌍을 추가했습니다. 키는 '키'이고 값은 '값'입니다.

### 캐시에서 데이터 검색

이제 캐시에 데이터를 추가했으므로 캐시 클라이언트의 `get` 메서드를 호출하여 데이터를 검색할 수 있습니다.

`get` 메서드는 `key`와 `callback`의 두 가지 인수를 허용합니다. `key` 인수는 캐시 항목의 키이고 `callback` 인수는 데이터가 캐시에서 검색될 때 호출되는 함수입니다.

```javascript
var redis = require("redis");
var client = redis.createClient();

var cache = redis.createClient();

cache.get("key", function(err, data) {
  if (err) {
    console.log(err);
  } else {
    console.log(data);
  }
});
```

위의 예에서는 캐시에서 'key' 키에 대한 데이터를 검색했습니다.

### 캐시에서 데이터 삭제

캐시 클라이언트의 `del` 메서드를 호출하여 캐시에서 데이터를 삭제할 수 있습니다.

`del` 메서드는 `key`와 `callback`의 두 가지 인수를 허용합니다. `key` 인수는 캐시 항목의 키이고 `callback` 인수는 데이터가 캐시에서 삭제되었을 때 호출되는 함수입니다.

```javascript
var redis = require("redis");
var client = redis.createClient();

var cache = redis.createClient();

cache.del("key", function(err, data) {
  if (err) {
    console.log(err);
  } else {
    console.log(data);
  }
});
```

위의 예에서는 캐시에서 'key' 키에 대한 데이터를 삭제했습니다.

## Redis로 Node.js에서 세션을 관리하는 방법

이 섹션에서는 Redis를 사용하여 Node.js에서 세션을 관리하는 방법을 살펴보겠습니다. 다음 주제를 다룹니다.

* Node.js 프로젝트 설정
* Redis 서버에 연결
* 세션 스토어 생성
* 세션 저장소에 데이터 추가
* 세션 저장소에서 데이터 검색
* 세션 저장소에서 데이터 삭제

### Node.js 프로젝트 설정

먼저 Node.js 프로젝트를 설정해야 합니다. 프로젝트의 새 디렉터리를 만든 다음 프로젝트 디렉터리에 `app.js`라는 파일을 만듭니다.

`app.js` 파일에는 Redis 모듈이 필요합니다. Redis 서버에 대한 연결도 설정합니다.

```javascript
var redis = require("redis");
var client = redis.createClient();
```

### Redis 서버에 연결

다음으로 Redis 서버에 연결해야 합니다. Redis 모듈의 `createClient` 메서드를 호출하여 이를 수행합니다.

`createClient` 메서드는 `host` 및 `port`의 두 가지 인수를 허용합니다. `host` 인수는 Redis 서버의 호스트 이름 또는 IP 주소이고 `port` 인수는 Redis 서버의 포트 번호입니다.

로컬 머신에서 Redis를 실행 중인 경우 `host` 및 `port`에 기본값을 사용할 수 있습니다.

```javascript
var redis = require("redis");
var client = redis.createClient();
```

### 세션 저장소 생성

이제 Redis 서버에 연결했으므로 세션 저장소를 만들 수 있습니다. Redis 모듈의 `createClient` 메서드를 호출하여 이를 수행합니다.

`createClient` 메서드는 `host` 및 `port`의 두 가지 인수를 허용합니다. `host` 인수는 Redis 서버의 호스트 이름 또는 IP 주소이고 `port` 인수는 Redis 서버의 포트 번호입니다.

로컬 머신에서 Redis를 실행 중인 경우 `host` 및 `port`에 기본값을 사용할 수 있습니다.

```javascript
var redis = require("redis");
var client = redis.createClient();

var session = redis.createClient();
```

### 세션 저장소에 데이터 추가

이제 세션 저장소가 있으므로 저장소에 데이터를 추가할 수 있습니다. 세션 저장소의 `set` 메서드를 호출하여 이를 수행합니다.

`set` 메서드는 `key`, `value` 및 `callback`의 세 가지 인수를 허용합니다. `key` 인수는 세션 항목의 키이고 `value` 인수는 세션 항목의 값이며 `callback` 인수는 데이터가 세션 저장소에 추가되었을 때 호출되는 함수입니다.

```javascript
var redis = require("redis");
var client = redis.createClient();

var session = redis.createClient();

session.set("key", "value", function(err, data) {
  if (err) {
    console.log(err);
  } else {
    console.log(data);
  }
});
```

위의 예에서는 세션 저장소에 키-값 쌍을 추가했습니다. 키는 '키'이고 값은 '값'입니다.

### 세션 저장소에서 데이터 검색

이제 세션 저장소에 데이터를 추가했으므로 세션 저장소의 `get` 메서드를 호출하여 데이터를 검색할 수 있습니다.

`get` 메서드는 `key`와 `callback`의 두 가지 인수를 허용합니다. `key` 인수는 세션 항목의 키이고 `callback` 인수는 세션 저장소에서 데이터를 검색할 때 호출되는 함수입니다.

```javascript
var redis = require("redis");
var client = redis.createClient();

var session = redis.createClient();

session.get("key", function(err, data) {
  if (err) {
    console.log(err);
  } else {
    console.log(data);
  }
});
```

위의 예에서는 세션 저장소에서 'key' 키에 대한 데이터를 검색했습니다.

### 세션 저장소에서 데이터 삭제

세션 저장소의 `del` 메서드를 호출하여 세션 저장소에서 데이터를 삭제할 수 있습니다.

`del` 메서드는 `key`와 `callback`의 두 가지 인수를 허용합니다. `key` 인수는 세션 항목의 키이고 `callback` 인수는 세션 저장소에서 데이터가 삭제되었을 때 호출되는 함수입니다.

```javascript
var redis = require("redis");
var client = redis.createClient();

var session = redis.createClient();

session.del("key", function(err, data) {
  if (err) {
    console.log(err);
  } else {
    console.log(data);
  }
});
```

위의 예에서는 세션 저장소에서 'key' 키에 대한 데이터를 삭제했습니다.

## 결론

이 기사에서는 Node.js와 Redis를 사용하여 데이터를 캐시하고 세션을 관리하는 방법을 살펴보았습니다. Node.js 프로젝트를 설정하고, Redis 서버에 연결하고, 캐시 클라이언트와 세션 저장소를 만드는 방법을 살펴보았습니다. 또한 캐시와 세션 저장소에 데이터를 추가하고, 캐시와 세션 저장소에서 데이터를 검색하고, 캐시와 세션 저장소에서 데이터를 삭제하는 방법도 살펴보았습니다.