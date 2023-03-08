---
title: 058: Nest.js 및 서비스 워커로 오프라인 우선 애플리케이션 구현
description: 
published: true
date: 2023-02-15T21:33:09.079Z
tags: 
editor: markdown
dateCreated: 2023-02-15T21:33:00.816Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [058: Implementing offline-first applications with Nest.js and Service Workers***English** document is available*](/en/Knowledge-base/Nest-js/Learning/058-implementing-offline-first-applications-with-nest-js-and-service-workers)
{.links-list}


058: Nest.js 및 서비스 워커로 오프라인 우선 애플리케이션 구현

서비스 워커는 웹 애플리케이션이 오프라인에서 작동하도록 만드는 강력한 도구입니다. 서비스 작업자를 사용하면 네트워크 요청을 가로채고 캐시된 응답을 제공하여 사용자가 오프라인일 때도 더 나은 경험을 제공할 수 있습니다.

이 게시물에서는 서비스 작업자를 사용하여 Nest.js 애플리케이션을 오프라인에서 작동시키는 방법을 보여줍니다. 간단한 "hello world" Nest.js 애플리케이션을 만드는 것으로 시작하겠습니다. 그런 다음 서비스 작업자를 등록하고 이를 사용하여 애플리케이션의 정적 자산을 캐시합니다. 마지막으로 서비스 워커를 사용하여 사용자가 오프라인일 때 캐시된 응답을 제공합니다.

Nest.js 애플리케이션 만들기

간단한 "hello world" Nest.js 애플리케이션을 만드는 것으로 시작하겠습니다. 먼저 app.js라는 새 파일을 만들고 다음 코드를 추가합니다.

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello, world!');
});

app.listen(3000, () => {
  console.log('Example app listening on port 3000!');
});
```

이 코드는 포트 3000에서 수신하고 "Hello, world!"로 응답하는 간단한 Express.js 애플리케이션을 만듭니다. 루트 URL을 방문할 때.

다음으로 Express.js 종속성을 설치합니다.

```
npm install --save express
```

이제 다음 명령을 실행하여 애플리케이션을 시작할 수 있습니다.

```
node app.js
```

다음 출력이 표시되어야 합니다.

```
Example app listening on port 3000!
```

이제 웹 브라우저에서 http://localhost:3000을 방문할 수 있으며 "Hello, world!" 메시지.

서비스 워커 등록

이제 기본 Nest.js 애플리케이션이 실행 중이므로 서비스 워커를 등록해 보겠습니다. 서비스 워커는 웹 애플리케이션의 기본 JavaScript 파일에 등록됩니다. 우리의 경우에는 app.js 파일입니다.

app.js 파일 하단에 다음 코드를 추가합니다.

```javascript
if ('serviceWorker' in navigator) {
  navigator.serviceWorker
    .register('/sw.js')
    .then(function() {
      console.log('Service worker registered!');
    })
    .catch(function(err) {
      console.log('Service worker registration failed: ', err);
    });
} else {
  console.log('Service workers are not supported.');
}
```

이 코드는 서비스 워커가 브라우저에서 지원되는지 확인합니다. 그렇다면 서비스 작업자 파일(sw.js)을 등록합니다. 서비스 워커가 지원되지 않으면 콘솔에 오류 메시지를 출력합니다.

다음으로 프로젝트의 루트 디렉터리에 sw.js라는 새 파일을 만듭니다. 이것은 서비스 작업자 파일입니다. sw.js 파일에 다음 코드를 추가합니다.

```javascript
self.addEventListener('install', function(event) {
  // Perform install steps
});

self.addEventListener('activate', function(event) {
  // Perform activate steps
});

self.addEventListener('fetch', function(event) {
  // Perform fetch steps
});
```

이 코드는 'install', 'activate' 및 'fetch'의 세 가지 이벤트 리스너를 설정합니다. 서비스 워커가 처음 설치될 때 'install' 이벤트가 시작됩니다. 서비스 워커가 활성화되면 '활성화' 이벤트가 시작됩니다. '가져오기' 이벤트는 네트워크 요청이 있을 때마다 발생합니다.

다음 섹션에서 이러한 각 이벤트 리스너에 코드를 추가합니다.

정적 자산 캐싱

이제 서비스 워커가 등록되었으므로 이를 사용하여 애플리케이션의 정적 자산을 캐시해 보겠습니다. 정적 자산은 이미지, CSS 파일 및 JavaScript 파일과 같이 자주 변경되지 않는 파일입니다.

먼저 'install' 이벤트 리스너에 코드를 추가해 보겠습니다. 이 코드는 서비스 작업자가 설치될 때 정적 자산을 캐시합니다.

```javascript
self.addEventListener('install', function(event) {
  event.waitUntil(
    caches.open('static-cache').then(function(cache) {
      return cache.addAll([
        '/',
        '/app.js',
        '/styles.css',
        '/images/logo.png'
      ]);
    })
  );
});
```

이 코드는 '정적 캐시'라는 캐시를 열고 나열된 파일을 캐시에 추가합니다. 'waitUntil' 메서드는 캐싱이 완료될 때까지 서비스 작업자를 활성 상태로 유지하도록 브라우저에 지시합니다.

다음으로 '활성화' 이벤트 리스너에 코드를 추가해 보겠습니다. 이 코드는 필요하지 않은 이전 캐시를 삭제합니다.

```javascript
self.addEventListener('activate', function(event) {
  event.waitUntil(
    caches.keys().then(function(cacheNames) {
      return Promise.all(
        cacheNames.filter(function(cacheName) {
          return cacheName.startsWith('static-') && cacheName != 'static-cache';
        }).map(function(cacheName) {
          return caches.delete(cacheName);
        })
      );
    })
  );
});
```

이 코드는 모든 캐시 목록을 가져오고 'static-'으로 시작하지만 'static-cache'가 아닌 캐시를 필터링하여 삭제합니다.

마지막으로 'fetch' 이벤트 리스너에 코드를 추가해 보겠습니다. 이 코드는 캐시된 응답이 있는 경우 제공하거나 네트워크에서 응답을 가져옵니다.

```javascript
self.addEventListener('fetch', function(event) {
  event.respondWith(
    caches.match(event.request).then(function(response) {
      if (response) {
        return response;
      }
      return fetch(event.request);
    })
  );
});
```

이 코드는 일치하는 요청에 대해 '정적 캐시'를 확인합니다. 일치하는 항목을 찾으면 캐시된 응답을 반환합니다. 일치하는 항목을 찾지 못하면 네트워크에서 응답을 가져옵니다.

서비스 워커 테스트

이제 서비스 워커에 코드를 추가했으므로 제대로 작동하는지 테스트해 보겠습니다.

먼저 실행 중인 경우 Nest.js 서버를 중지합니다. 그런 다음 다음 명령을 실행하여 프로덕션 모드에서 서버를 시작합니다.

```
NODE_ENV=production node app.js
```

이 명령은 NODE_ENV 환경 변수를 'production'으로 설정하고 서버를 시작합니다.

그런 다음 웹 브라우저에서 http://localhost:3000을 열고 개발자 도구를 엽니다. 'Application' 탭을 클릭하면 'Service Workers' 섹션이 표시됩니다. 서비스 워커가 등록되어 있고 '활성' 상태인지 확인해야 합니다.

이제 sw.js 파일에서 'fetch' 이벤트 리스너를 변경합니다. 예를 들어 'static-cache'를 'my-cache'로 변경할 수 있습니다. 그런 다음 파일을 저장하고 페이지를 새로 고칩니다. 서비스 워커가 '업데이트'되고 '활성화 대기 중'임을 확인할 수 있습니다.

서비스 워커가 작동하는지 테스트하려면 개발자 도구에서 '네트워크' 탭을 열고 '캐시 비활성화' 체크박스가 선택되어 있는지 확인하세요. 그런 다음 페이지를 새로 고칩니다. 서비스 워커가 캐시된 응답을 제공하고 있는지 확인해야 합니다.

sw.js 파일에서 'fetch' 이벤트 리스너를 변경하면 서비스 워커 등록을 취소하고 다시 등록해야 합니다. 이렇게 하려면 개발자 도구에서 '응용 프로그램' 탭을 열고 '등록 취소' 버튼을 클릭합니다. 그런 다음 페이지를 새로고침하면 서비스 워커가 다시 등록된 것을 볼 수 있습니다.

결론

이 게시물에서는 서비스 워커를 사용하여 Nest.js 애플리케이션을 오프라인에서 작동시키는 방법을 보여주었습니다. 간단한 "hello world" Nest.js 애플리케이션을 만드는 것으로 시작했습니다. 그런 다음 서비스 작업자를 등록하고 이를 사용하여 애플리케이션의 정적 자산을 캐시했습니다. 마지막으로 서비스 워커를 사용하여 사용자가 오프라인일 때 캐시된 응답을 제공했습니다.