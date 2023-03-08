---
title: HTTP 헤더: 웹 요청 및 응답의 메타데이터 이해
description: 
published: true
date: 2023-03-07T23:32:43.880Z
tags: 
editor: markdown
dateCreated: 2023-03-07T23:32:36.410Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [HTTP Headers: Understanding the Metadata of Web Requests and Responses***English** document is available*](/en/Knowledge-base/Network/http-headers-understanding-the-metadata-of-web-requests-and-responses)
{.links-list}

HTTP 헤더: 웹 요청 및 응답의 메타데이터 이해

HTTP(Hypertext Transfer Protocol)는 World Wide Web을 위한 데이터 통신의 기반입니다. 인터넷을 통해 데이터를 보내고 받는 표준화된 방법을 제공합니다. HTTP 헤더는 요청 또는 응답에 대한 다양한 메타데이터를 전달하는 이 통신 프로토콜의 필수 부분입니다.

HTTP 헤더에는 콘텐츠 유형, 캐싱 지침, 인증 자격 증명 등과 같이 전송 중인 데이터에 대한 추가 정보가 포함되어 있습니다. HTTP 헤더를 이해하는 것은 웹 응용 프로그램 문제를 해결하고 웹 사이트 성능을 최적화하는 데 도움이 될 수 있으므로 웹 개발자에게 매우 중요합니다.

이 기사에서는 HTTP 헤더, 유형 및 웹 개발에서의 용도에 대해 자세히 살펴봅니다.

### HTTP 헤더란 무엇입니까?

HTTP 헤더는 HTTP 요청 또는 응답 메시지의 시작 부분에 첨부되는 추가 정보입니다. 콘텐츠 유형, 캐싱 지침, 인증 자격 증명 등과 같이 전송되는 데이터에 대한 메타데이터를 제공합니다.

HTTP 헤더는 요청 헤더와 응답 헤더의 두 가지 범주로 나뉩니다.

#### 요청 헤더

요청 헤더는 HTTP 요청 메시지의 일부로 클라이언트에서 서버로 전송됩니다. 여기에는 전송되는 데이터 유형, 사용자 에이전트 및 쿠키와 같은 클라이언트 요청에 대한 메타데이터가 포함됩니다.

다음은 몇 가지 일반적인 요청 헤더입니다.

- Accept: 이 헤더는 클라이언트가 응답으로 기대하는 데이터 유형을 지정합니다. 예를 들어 ```Accept: application/json```은 클라이언트가 응답으로 JSON 데이터를 기대함을 나타냅니다.
- User-Agent: 이 헤더는 브라우저 유형 및 버전과 같은 요청을 하는 클라이언트를 식별합니다.
- Referer: 이 헤더는 클라이언트가 요청하도록 이끈 페이지의 URL을 제공합니다.
- 쿠키: 이 헤더에는 요청과 관련된 모든 쿠키가 포함됩니다.

#### 응답 헤더

응답 헤더는 HTTP 응답 메시지의 일부로 서버에서 클라이언트로 전송됩니다. 여기에는 콘텐츠 유형, 캐싱 지침 및 쿠키와 같은 서버 응답에 대한 메타데이터가 포함됩니다.

다음은 몇 가지 일반적인 응답 헤더입니다.

- Content-Type: 이 헤더는 응답으로 전송되는 데이터 유형을 지정합니다. 예를 들어 ```Content-Type: text/html```은 서버가 HTML 문서를 보내고 있음을 나타냅니다.
- Cache-Control: 이 헤더는 클라이언트가 응답을 캐시하는 방법을 지정합니다. 예를 들어 ```Cache-Control: max-age=3600```은 클라이언트가 한 시간 동안 응답을 캐시해야 함을 나타냅니다.
- Set-Cookie: 이 헤더는 클라이언트의 브라우저에 쿠키를 설정합니다.

### HTTP 헤더를 보는 방법?

HTTP 헤더는 Chrome 개발자 도구 또는 Firefox 개발자 도구와 같은 브라우저 개발자 도구를 사용하여 볼 수 있습니다.

Chrome 개발자 도구를 사용하여 HTTP 헤더를 보는 방법은 다음과 같습니다.

1. 웹 페이지의 아무 곳이나 마우스 오른쪽 버튼으로 클릭하고 검사를 선택하여 Chrome 개발자 도구를 엽니다.
2. 네트워크 탭을 클릭합니다.
3. 웹 페이지를 새로 고칩니다.
4. 목록에서 요청을 클릭합니다.
5. 헤더 탭 아래에 헤더가 표시됩니다.

Firefox 개발자 도구를 사용하여 HTTP 헤더를 보는 방법은 다음과 같습니다.

1. Ctrl + Shift + I를 눌러 Firefox 개발자 도구를 엽니다.
2. 네트워크 탭을 클릭합니다.
3. 웹 페이지를 새로 고칩니다.
4. 목록에서 요청을 클릭합니다.
5. 헤더 탭 아래에 헤더가 표시됩니다.

### HTTP 헤더를 설정하는 방법?

HTTP 헤더는 PHP, Python 또는 Node.js와 같은 서버측 프로그래밍 언어를 사용하여 설정할 수 있습니다. 여기 몇 가지 예가 있어요.

#### PHP

```php
header('Content-Type: application/json');
header('Cache-Control: max-age=3600');
```

#### 파이썬

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello, World!', 200, {'Content-Type': 'text/plain', 'Cache-Control': 'max-age=3600'}
```

#### Node.js

```javascript
res.writeHead(200, {
    'Content-Type': 'text/plain',
    'Cache-Control': 'max-age=3600'
});
res.end('Hello, World!');
```

### 결론

HTTP 헤더는 전송되는 데이터에 대한 메타데이터를 전달하는 HTTP 프로토콜의 필수 부분입니다. HTTP 헤더를 이해하는 것은 웹 응용 프로그램 문제를 해결하고 웹 사이트 성능을 최적화하는 데 도움이 될 수 있으므로 웹 개발자에게 매우 중요합니다.

이 기사에서는 HTTP 헤더, 유형 및 웹 개발에서의 용도에 대해 자세히 살펴보았습니다. 또한 다양한 서버 측 프로그래밍 언어를 사용하여 HTTP 헤더를 보고 설정하는 방법에 대한 예제도 포함되어 있습니다.

외부 리소스:
- [MDN 웹 문서 - HTTP 헤더](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- [Google Developers - HTTP 헤더](https://developers.google.com/web/updates/2017/09/immutable-headers)