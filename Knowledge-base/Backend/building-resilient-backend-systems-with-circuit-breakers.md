---
title: 회로 차단기로 탄력적인 백엔드 시스템 구축
description: 
published: true
date: 2023-02-17T18:00:53.982Z
tags: 
editor: markdown
dateCreated: 2023-01-29T20:54:00.034Z
---

- [Building Resilient Backend Systems with Circuit Breakers***English** version of this document is available*](/en/Knowledge-base/Backend/building-resilient-backend-systems-with-circuit-breakers)
{.links-list}


# 서킷 브레이커로 탄력적인 백엔드 시스템 구축

이 게시물에서는 회로 차단기를 사용하여 보다 탄력적인 백엔드 시스템을 구축하는 방법을 살펴보겠습니다. 먼저 회로 차단기가 무엇이고 어떻게 작동하는지 정의합니다. 그런 다음 간단한 Node.js 애플리케이션에서 회로 차단기를 사용하는 방법을 살펴보겠습니다.

## 서킷 브레이커란?

회로 차단기는 시스템의 복원력을 높이는 데 사용되는 소프트웨어 설계 패턴입니다. 시스템을 사용할 수 없거나 응답하지 않는 경우를 감지하는 메커니즘을 제공하고 이 경우 빠르고 정상적으로 실패함으로써 이를 수행합니다.

회로 차단기의 기본 개념은 계단식 오류를 방지할 수 있다는 것입니다. 시스템의 한 부분을 사용할 수 없는 경우 회로 차단기는 시스템의 다른 부분이 액세스를 시도하는 것을 방지하여 해당 부분도 사용할 수 없게 되는 것을 방지할 수 있습니다.

## 회로 차단기는 어떻게 작동합니까?

회로 차단기는 '닫힘', '열림' 및 '반열림'의 세 가지 상태가 있습니다.

'닫힌' 상태에서 회로 차단기는 요청이 백엔드 시스템을 통과하도록 허용합니다. 백엔드 시스템을 사용할 수 없거나 응답하지 않으면 회로 차단기가 '열림' 상태로 전환됩니다.

'개방' 상태에서 회로 차단기는 어떤 요청도 통과하도록 허용하지 않습니다. 이는 백엔드 시스템이 과부하되는 것을 방지하기 위한 것입니다. 일정 시간이 지나면 회로 차단기가 '반개방' 상태로 전환됩니다.

'half-open' 상태에서 회로 차단기는 제한된 수의 요청이 통과하도록 허용합니다. 이는 백엔드 시스템을 복구할 수 있도록 하기 위한 것입니다. 백엔드 시스템을 여전히 사용할 수 없거나 응답하지 않으면 회로 차단기가 다시 '열림' 상태로 전환됩니다.

## Node.js에서 회로 차단기 사용

간단한 Node.js 애플리케이션에서 회로 차단기를 사용하는 방법을 살펴보겠습니다. 우리는 `opossum` 라이브러리를 사용할 것입니다.

먼저 `opossum` 라이브러리를 설치해야 합니다.

```
npm install opossum
```

다음으로 라이브러리를 요구해야 합니다.

```javascript
const opossum = require('opossum');
```

이제 회로 차단기를 만들 수 있습니다.

```javascript
const circuitBreaker = new opossum.CircuitBreaker(function () {
  // This is the function that will be called when the circuit breaker is `closed`
  // It should return a promise that resolves when the backend system is available
  // and rejects when the backend system is unavailable
});
```

이제 `circuitBreaker` 개체를 사용하여 백엔드 시스템에 요청할 수 있습니다.

```javascript
circuitBreaker.fire()
  .then(function (result) {
    // The request was successful
  })
  .catch(function (err) {
    // The request failed
  });
```

백엔드 시스템을 사용할 수 없거나 응답하지 않는 경우 'fire' 메서드는 거부된 약속을 반환하고 'catch' 핸들러가 실행됩니다.

## 결론

이 게시물에서는 서킷 브레이커를 사용하여 보다 탄력적인 백엔드 시스템을 구축하는 방법을 살펴보았습니다. 회로 차단기가 작동하는 방식과 간단한 Node.js 애플리케이션에서 회로 차단기를 사용하는 방법을 살펴보았습니다.