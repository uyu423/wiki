---
title: 프런트엔드-백엔드 통신을 위한 BFF API 구축
description: 
published: true
date: 2023-02-18T13:32:39.605Z
tags: 
editor: markdown
dateCreated: 2023-02-18T13:32:38.195Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building BFF API for Frontend-Backend Communication***English** document is available*](/en/Knowledge-base/Backend/building-bff-api-for-frontend-backend-communication)
{.links-list}


# Frontend-Backend 통신을 위한 BFF API 구축

웹 애플리케이션을 구축할 때 개발자는 프런트엔드가 백엔드와 통신하는 방법을 고려해야 합니다. 대부분의 경우 이 통신은 API에 의해 처리됩니다.

API(Application Programming Interface)는 두 애플리케이션이 서로 상호 작용할 수 있는 방법을 지시하는 일련의 규칙입니다. 백엔드에서 노출되는 기능과 프런트엔드에서 액세스할 수 있는 방법을 정의합니다.

API를 구축하는 방법에는 여러 가지가 있습니다. 이 기사에서는 BFF(Backend for Frontend) API 구축에 중점을 둘 것입니다.

BFF는 프론트엔드 애플리케이션의 요구 사항을 위해 특별히 설계된 API 유형입니다. 프런트엔드와 백엔드 사이의 계층 역할을 하여 필요한 형식으로 필요한 데이터를 프런트엔드에 제공합니다.

BFF API를 구축하는 것은 웹 애플리케이션의 성능을 개선하고 개발 프로세스를 더 간단하게 만드는 좋은 방법이 될 수 있습니다. 이 기사에서는 BFF API 사용의 이점에 대해 논의하고 Node.js 프레임워크를 사용하여 빌드하는 방법을 보여줍니다.

## BFF API란 무엇인가요?

BFF API는 프론트엔드 애플리케이션의 요구 사항을 위해 특별히 설계된 API 유형입니다. 프런트엔드와 백엔드 사이의 계층 역할을 하여 필요한 형식으로 필요한 데이터를 프런트엔드에 제공합니다.

BFF API는 일반적으로 기존 API보다 훨씬 간단합니다. 일반적으로 마이크로서비스 아키텍처를 사용하여 구축되므로 높은 수준의 유연성과 사용자 정의가 가능합니다.

## BFF API 사용의 이점

BFF API를 사용하면 다음과 같은 많은 이점이 있습니다.

- 향상된 성능: BFF API는 기존 API보다 프런트엔드와 백엔드 간에 더 빠르고 안정적인 연결을 제공할 수 있습니다.

- 간단한 개발: BFF API는 기존 API보다 개발 및 테스트가 더 쉬울 수 있습니다.

- 더 많은 제어: BFF API를 사용하면 프런트엔드가 백엔드와 상호 작용하는 방식을 더 많이 제어할 수 있습니다.

## BFF API 구축 방법

BFF API 구축은 비교적 간단한 프로세스입니다. 이 섹션에서는 Node.js 기반 BFF API 구축과 관련된 단계를 안내합니다.

### 1단계: 백엔드 선택

BFF API 구축의 첫 번째 단계는 백엔드를 선택하는 것입니다. 이 예에서는 Node.js를 사용합니다.

Node.js는 마이크로서비스 구축에 적합한 널리 사용되는 JavaScript 기반 백엔드 프레임워크입니다. 가볍고 효율적이며 크고 활동적인 커뮤니티가 있습니다.

### 2단계: 프런트엔드 선택

다음 단계는 프런트엔드를 선택하는 것입니다. 이 예에서는 React를 사용합니다.

React는 인기 있는 JavaScript 기반 프런트엔드 프레임워크로 단일 페이지 애플리케이션을 구축하는 데 매우 적합합니다. 빠르고 효율적이며 개발을 더 간단하게 만드는 선언적 프로그래밍 모델을 제공합니다.

### 3단계: 백엔드 서비스 생성

다음 단계는 백엔드 서비스를 만드는 것입니다. 이 서비스는 백엔드에서 데이터를 가져와 프런트엔드에 노출하는 일을 담당합니다.

Node.js에서 백엔드 서비스는 일반적으로 Express를 사용하여 구축됩니다. Express는 웹 애플리케이션을 쉽게 구축할 수 있게 해주는 널리 사용되는 Node.js 웹 프레임워크입니다.

이 예에서는 `/api/data`에서 `GET` 엔드포인트를 노출하는 간단한 Express 기반 백엔드 서비스를 생성합니다. 이 끝점은 프런트엔드에서 사용할 데이터가 포함된 JSON 개체를 반환합니다.

```javascript
const express = require('express');
const app = express();

app.get('/api/data', (req, res) => {
  const data = {
    message: 'Hello from the backend!'
  };

  res.json(data);
});

app.listen(3000, () => {
  console.log('Example app listening on port 3000!');
});
```

### 4단계: 프런트엔드 서비스 만들기

다음 단계는 프런트엔드 서비스를 만드는 것입니다. 이 서비스는 백엔드에서 데이터를 가져와서 페이지에 렌더링하는 역할을 합니다.

React에서 프런트엔드 서비스는 일반적으로 React Router를 사용하여 구축됩니다. React Router는 단일 페이지 애플리케이션을 쉽게 구축할 수 있게 해주는 인기 있는 React 라우팅 라이브러리입니다.

이 예에서는 백엔드에서 가져온 데이터가 포함된 페이지를 렌더링하는 간단한 React Router 기반 프런트엔드 서비스를 생성합니다.

```javascript
import React from 'react';
import { render } from 'react-dom';
import {BrowserRouter as Router, Route} from 'react-router-dom';

const App = () => (
  <Router>
    <Route path="/api/data" component={DataPage} />
  </Router>
);

const DataPage = () => (
  <div>
    <h1>Hello from the frontend!</h1>
  </div>
);

render(<App />, document.getElementById('root'));
```

### 5단계: 백엔드 및 프런트엔드 서비스 연결

다음 단계는 백엔드와 프런트엔드 서비스를 연결하는 것입니다. 이 예에서는 간단한 Node.js 프록시를 사용하여 이 작업을 수행합니다.

Node.js 프록시는 프런트엔드에서 백엔드로 요청을 라우팅하는 데 사용할 수 있는 미들웨어 유형입니다. 프런트엔드 코드를 수정하지 않고도 백엔드와 프런트엔드를 연결하는 간단하고 효율적인 방법입니다.

이 예에서는 `http-proxy-middleware` 패키지를 사용하여 프록시를 생성합니다. 이 패키지를 사용하면 프런트엔드 `/api/data` 엔드포인트에서 백엔드 `/api/data` 엔드포인트로 요청을 라우팅할 수 있습니다.

```javascript
const express = require('express');
const proxy = require('http-proxy-middleware');

const app = express();

app.use(
  '/api/data',
  proxy({
    target: 'http://localhost:3000',
    changeOrigin: true
  })
);

app.listen(4000, () => {
  console.log('Proxy app listening on port 4000!');
});
```

### 6단계: 애플리케이션 테스트

마지막 단계는 애플리케이션을 테스트하는 것입니다. 이 예에서는 `curl` 명령을 사용하여 프런트엔드 `/api/data` 엔드포인트에 요청을 보냅니다.

모든 것이 올바르게 작동하면 백엔드 `/api/data` 엔드포인트에서 가져온 데이터가 표시되어야 합니다.

```
$ curl http://localhost:4000/api/data
{"message":"Hello from the backend!"}
```

## 결론

이 기사에서는 BFF API 사용의 이점에 대해 논의하고 Node.js 프레임워크를 사용하여 빌드하는 방법을 보여주었습니다.

BFF API를 구축하는 것은 웹 애플리케이션의 성능을 개선하고 개발 프로세스를 더 간단하게 만드는 좋은 방법이 될 수 있습니다. 웹 애플리케이션을 구축하는 경우 BFF API 사용을 고려하는 것이 좋습니다.