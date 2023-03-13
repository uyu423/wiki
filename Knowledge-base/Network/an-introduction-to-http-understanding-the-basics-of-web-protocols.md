---
title: HTTP 소개: 웹 프로토콜의 기본 이해
description: 
published: true
date: 2023-03-13T00:32:54.437Z
tags: 
editor: markdown
dateCreated: 2023-03-13T00:32:54.437Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [An Introduction to HTTP: Understanding the Basics of Web Protocols***English** document is available*](/en/Knowledge-base/Network/an-introduction-to-http-understanding-the-basics-of-web-protocols)
{.links-list}



# HTTP 소개: 웹 프로토콜의 기본 이해

HTTP(Hypertext Transfer Protocol)는 World Wide Web에서 데이터 통신의 기반입니다. 웹 서버가 웹 브라우저와 통신할 수 있도록 하는 애플리케이션 계층 프로토콜입니다. 대부분의 웹 애플리케이션이 HTTP를 기반으로 구축되기 때문에 IT 개발자에게는 HTTP를 이해하는 것이 필수적입니다. 이 기사에서는 HTTP가 무엇이며 어떻게 작동하는지 살펴보겠습니다.

## HTTP란?

HTTP는 웹 브라우저와 웹 서버가 서로에게 보내는 메시지 형식을 정의하는 프로토콜입니다. 메시지는 요청과 응답으로 구성됩니다. 요청은 웹 브라우저에서 웹 서버로 전송되고 응답은 웹 서버에서 웹 브라우저로 다시 전송됩니다. 요청과 응답은 헤더와 본문으로 구성됩니다.

헤더에는 내용 유형 및 본문 길이와 같은 메시지에 대한 메타데이터가 포함됩니다. 본문에는 HTML, CSS 또는 JavaScript와 같은 메시지의 실제 내용이 포함됩니다.

HTTP는 상태 비저장 프로토콜입니다. 즉, 각 요청 및 응답은 다른 요청 또는 응답과 독립적입니다. 이렇게 하면 각 요청을 독립적으로 처리할 수 있으므로 웹 애플리케이션을 쉽게 확장할 수 있습니다.

## HTTP는 어떻게 작동합니까?

웹 브라우저가 웹 서버에서 리소스를 요청하려는 경우 서버에 HTTP 요청을 보냅니다. 요청에는 메서드, URI 및 헤더가 포함됩니다. 메서드는 브라우저가 리소스에 대해 수행하려는 작업을 지정합니다. 가장 일반적인 방법은 서버에서 리소스를 가져오는 'GET'입니다.

URI 또는 Uniform Resource Identifier는 브라우저가 액세스하려는 리소스를 식별하는 문자열입니다. 웹 페이지, 이미지, 비디오 또는 기타 유형의 리소스가 될 수 있습니다.

헤더에는 브라우저 유형, 허용된 콘텐츠 유형 및 요청 언어와 같은 요청에 대한 메타데이터가 포함됩니다.

웹 서버가 요청을 받으면 이를 처리하고 HTTP 응답을 다시 보냅니다. 응답에는 상태 코드, 헤더 및 본문이 포함됩니다.

상태 코드는 요청이 성공했는지 여부를 나타냅니다. 가장 일반적인 상태 코드는 '200 OK'이며 이는 요청이 성공했으며 요청된 리소스가 응답에 포함되었음을 의미합니다.

헤더에는 콘텐츠 유형 및 본문 길이와 같은 응답에 대한 메타데이터가 포함됩니다.

본문에는 HTML, CSS 또는 JavaScript와 같은 응답의 실제 내용이 포함됩니다.

## HTTP 요청 및 응답 예제

HTTP 요청 및 응답의 예를 살펴보겠습니다.

**HTTP 요청:**

```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate, sdch, br
Accept-Language: en-US,en;q=0.8
```

위의 HTTP 요청은 `www.example.com` 서버의 `/index.html` 리소스에 대한 `GET` 메서드입니다. 여기에는 브라우저 유형 및 버전을 지정하는 `User-Agent` 헤더와 같은 다양한 헤더가 포함됩니다. 또한 허용되는 콘텐츠 유형을 지정하는 'Accept' 헤더도 포함합니다.

**HTTP 응답:**

```
HTTP/1.1 200 OK
Date: Sat, 29 Apr 2017 15:30:03 GMT
Server: Apache
Last-Modified: Mon, 27 Mar 2017 14:10:10 GMT
ETag: "1234567890"
Content-Type: text/html
Content-Length: 291

<!DOCTYPE html>
<html>
<head>
	<title>Example Page</title>
</head>
<body>
	<h1>Welcome to Example Page</h1>
	<p>This is an example page.</p>
</body>
</html>
```

위의 HTTP 응답에는 요청이 성공했음을 의미하는 '200 OK' 상태 코드가 있습니다. 여기에는 웹 서버 소프트웨어를 지정하는 'Server' 헤더와 같은 다양한 헤더가 포함됩니다. 또한 본문의 콘텐츠 유형을 지정하는 'Content-Type' 헤더도 포함합니다. 본문에는 제목과 제목이 있는 HTML 문서가 포함되어 있습니다.

## 결론

HTTP는 World Wide Web에서 데이터 통신의 기반입니다. 이를 통해 웹 브라우저는 웹 서버와 통신하고 리소스를 검색할 수 있습니다. 대부분의 웹 애플리케이션이 HTTP를 기반으로 구축되기 때문에 IT 개발자에게는 HTTP를 이해하는 것이 필수적입니다. HTTP 작동 방식을 이해함으로써 개발자는 강력하고 확장 가능한 웹 애플리케이션을 구축할 수 있습니다.

## 외부 리소스

- [HTTP - 위키백과](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)
- [HTTP 방법 - MDN 웹 문서](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [HTTP 응답 코드 - MDN 웹 문서](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)