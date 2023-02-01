---
title: Node.js
description: 
published: true
date: 2023-02-01T02:04:39.372Z
tags: 
editor: markdown
dateCreated: 2023-02-01T02:04:39.372Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Node.js***English** version of this document is available*](/en/Knowledge-base/Dictionary/node-js)
{.links-list}


# 개요
Node.js는 웹 브라우저 외부에서 JavaScript 코드를 실행하는 오픈 소스 크로스 플랫폼 JavaScript 런타임 환경입니다. 서버 측 및 네트워크 응용 프로그램을 만드는 데 사용됩니다. Node.js는 확장 가능한 네트워크 애플리케이션을 구축하도록 설계되었으며 웹 서버 및 네트워킹 도구를 만드는 데 자주 사용됩니다.

# 역사
Node.js는 Ryan Dahl이 2009년에 만들었습니다. 처음에는 Chrome의 V8 JavaScript 엔진에 구축된 JavaScript 런타임으로 출시되었습니다. 초기 릴리스 이후 Node.js는 가장 인기 있는 웹 개발 플랫폼 중 하나가 되었습니다.

# 설명
Node.js는 개발자가 JavaScript로 서버측 및 네트워크 애플리케이션을 작성할 수 있도록 하는 JavaScript 런타임 환경입니다. Chrome의 V8 JavaScript 엔진을 기반으로 하며 가볍고 효율적인 이벤트 중심의 비차단 I/O 모델을 사용합니다. Node.js는 확장 가능한 네트워크 애플리케이션을 구축하도록 설계되었으며 웹 서버 및 네트워킹 도구를 만드는 데 자주 사용됩니다.

# 특징
Node.js는 웹 개발을 위한 매력적인 플랫폼이 되도록 하는 몇 가지 기능이 있습니다. 오픈 소스, 크로스 플랫폼이며 크고 활발한 개발자 커뮤니티가 있습니다. 또한 가볍고 효율적인 이벤트 중심의 비차단 I/O 모델을 통해 빠르고 효율적입니다. Node.js에는 또한 애플리케이션을 쉽게 개발할 수 있게 해주는 많은 라이브러리와 모듈 세트가 있습니다.

# 예
다음은 웹 서버를 생성하는 Node.js 애플리케이션의 간단한 예입니다.

```
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

# 장점과 단점
Node.js는 웹 개발을 위한 매력적인 플랫폼이 되는 몇 가지 장점이 있습니다. 오픈 소스, 크로스 플랫폼이며 크고 활발한 개발자 커뮤니티가 있습니다. 또한 가볍고 효율적인 이벤트 중심의 비차단 I/O 모델을 통해 빠르고 효율적입니다. Node.js에는 또한 애플리케이션을 쉽게 개발할 수 있게 해주는 많은 라이브러리와 모듈 세트가 있습니다.

그러나 Node.js에도 몇 가지 단점이 있습니다. CPU를 많이 사용하는 애플리케이션에는 적합하지 않으며 디버깅하기 어려울 수 있습니다. 또한 Node.js 애플리케이션은 제대로 보호되지 않으면 보안 문제에 취약할 수 있습니다.

# 논란
Node.js는 JavaScript 언어를 사용하기 때문에 논란의 대상이 되어 왔습니다. 일부 개발자는 JavaScript가 서버 측 개발에 적합한 언어가 아니라고 주장한 반면 다른 개발자는 웹 개발에 이상적인 언어라고 주장했습니다.

# 관련 기술
Node.js는 종종 MongoDB, Express.js 및 Angular.js와 같은 다른 기술과 함께 사용됩니다. 이러한 기술을 함께 사용하여 강력한 웹 애플리케이션을 만들 수 있습니다.

# 여담
Node.js는 종종 채팅 애플리케이션 및 온라인 게임과 같은 실시간 애플리케이션을 만드는 데 사용됩니다. 또한 홈 오토메이션 시스템과 같은 사물 인터넷(IoT) 애플리케이션을 만드는 데 사용됩니다.

# 기타
Node.js는 점점 인기를 얻고 있는 웹 개발 플랫폼이며 Netflix, PayPal, Uber와 같은 많은 대기업에서 사용하고 있습니다. 또한 Atom 및 Visual Studio Code와 같은 데스크톱 응용 프로그램을 만드는 데 사용됩니다.