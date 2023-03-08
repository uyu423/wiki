---
title: 057: 서비스 작업자와 함께 Nest.js 사용
description: 
published: true
date: 2023-02-15T20:32:42.846Z
tags: 
editor: markdown
dateCreated: 2023-02-15T20:32:35.146Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [057: Using Nest.js with Service Workers***English** document is available*](/en/Knowledge-base/Nest-js/Learning/057-using-nest-js-with-service-workers)
{.links-list}


# 서비스 워커와 함께 Nest.js 사용

서비스 워커는 웹 애플리케이션의 성능을 크게 향상시킬 수 있는 강력한 도구입니다. 그러나 숙련된 개발자도 실수할 수 있는 몇 가지 주의 사항이 있습니다. 이 게시물에서는 서비스 작업자와 함께 Nest.js를 사용하여 이러한 함정을 피하는 방법을 살펴보겠습니다.

## 서비스 워커란?

서비스 작업자는 웹 브라우저의 백그라운드에서 실행되고 네트워크 요청을 가로채는 스크립트입니다. 이를 통해 오프라인 사용을 위한 캐시 리소스와 같은 작업을 수행하거나 네트워크 상태에 따라 다른 콘텐츠를 제공할 수 있습니다.

## Nest.js가 무엇인가요?

Nest.js는 JavaScript를 사용하여 서버측 애플리케이션을 구축하기 위한 프레임워크입니다. Express 웹 프레임워크 위에 구축되었으며 TypeScript를 사용하여 유형 안전성을 제공합니다.

## 서비스 작업자와 함께 Nest.js 사용

서비스 작업자와 함께 Nest.js를 사용하는 것은 2단계 프로세스입니다. 먼저 Nest.js에 Service Worker 스크립트를 등록해야 합니다. 이는 `app.module.ts` 파일에서 수행할 수 있습니다.

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { ServiceWorkerModule } from '@nestjs/service-worker';

@Module({
  imports: [
    ServiceWorkerModule.register('/ngsw-worker.js'),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

두 번째 단계는 프로젝트의 루트에 `ngsw-worker.js` 파일을 생성하는 것입니다. 이 파일에는 Service Worker 코드가 포함되어 있으며 Nest.js에서 제공됩니다.

```javascript
// This is the code for the Service Worker

self.addEventListener('fetch', event => {
  // This is where you can handle network requests
  // and serve different content based on the network conditions
});
```

이제 서비스 작업자와 함께 Nest.js를 사용하는 방법에 대한 기본적인 이해가 있으므로 서비스 작업자가 제공할 수 있는 몇 가지 이점을 살펴보겠습니다.

## 서비스 워커의 이점

서비스 작업자는 오프라인 지원, 백그라운드 데이터 동기화 및 푸시 알림을 포함하여 웹 애플리케이션에 다양한 이점을 제공할 수 있습니다.

### 오프라인 지원

서비스 워커의 가장 일반적인 사용 사례 중 하나는 웹 애플리케이션에 대한 오프라인 지원을 제공하는 것입니다. 이는 서비스 워커의 'fetch' 이벤트 핸들러에서 리소스를 캐싱하여 달성할 수 있습니다.

```javascript
// This is the code for the Service Worker

self.addEventListener('fetch', event => {
  // Try to fetch the resource from the network first
  event.respondWith(
    fetch(event.request).catch(() => {
      // If the network request fails, try to get the resource from the cache
      return caches.match(event.request);
    })
  );
});
```

### 백그라운드 데이터 동기화

서비스 워커의 또 다른 일반적인 사용 사례는 백그라운드 데이터 동기화를 수행하는 것입니다. 이는 원격 서버의 데이터로 로컬 데이터베이스를 업데이트하는 것과 같은 작업에 유용할 수 있습니다.

```javascript
// This is the code for the Service Worker

self.addEventListener('sync', event => {
  // This is where you can perform background data synchronization
});
```

### 푸시 알림

서비스 워커를 사용하여 사용자에게 푸시 알림을 보낼 수도 있습니다. 이는 경고 또는 업데이트와 같은 항목에 유용할 수 있습니다.

```javascript
// This is the code for the Service Worker

self.addEventListener('push', event => {
  // This is where you can send push notifications to users
});
```

## 서비스 워커의 함정

많은 이점에도 불구하고 Service Worker에는 숙련된 개발자도 실수할 수 있는 몇 가지 주의 사항이 있습니다.

### 보안

서비스 워커의 가장 큰 관심사 중 하나는 보안입니다. 서비스 워커는 네트워크 요청에 액세스할 수 있으므로 중간자 공격을 수행하는 데 사용될 수 있습니다.

이 위험을 완화하려면 신뢰할 수 있는 소스의 서비스 워커만 등록하는 것이 중요합니다. Nest.js의 경우 이는 Nest.js에서 제공하는 서비스 워커만 등록한다는 의미입니다.

### 캐싱

Service Workers의 또 다른 잠재적 함정은 캐싱입니다. 서비스 워커를 사용하여 리소스를 캐싱할 때 올바른 캐싱 헤더를 설정하는 것이 중요합니다. 그렇지 않으면 리소스가 올바르게 캐시되지 않거나 너무 오랫동안 캐시될 수 있습니다.

```javascript
// This is the code for the Service Worker

self.addEventListener('fetch', event => {
  // Try to fetch the resource from the network first
  event.respondWith(
    fetch(event.request).then(response => {
      // If the network request succeeds, cache the response
      return caches.open(CACHE_NAME).then(cache => {
        cache.put(event.request, response.clone());
        return response;
      });
    }).catch(() => {
      // If the network request fails, try to get the resource from the cache
      return caches.match(event.request);
    })
  );
});
```

## 결론

이 게시물에서는 서비스 작업자와 함께 Nest.js를 사용하는 방법을 살펴보았습니다. 또한 Service Worker가 제공할 수 있는 몇 가지 이점과 주의해야 할 몇 가지 위험 요소도 확인했습니다.

Service Workers에 대해 자세히 알아보려면 다음 리소스를 확인하는 것이 좋습니다.

- [Service Workers: 소개](https://developers.google.com/web/fundamentals/primers/service-workers)
- [서비스 워커 사용하기](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers)
- [서비스 작업자 수명 주기](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers# the_serviceworker_lifecycle)