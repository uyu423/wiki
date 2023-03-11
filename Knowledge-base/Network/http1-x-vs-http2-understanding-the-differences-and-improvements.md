---
title: HTTP/1.x 대 HTTP/2: 차이점 및 개선 사항 이해
description: 
published: true
date: 2023-03-11T17:32:46.323Z
tags: 
editor: markdown
dateCreated: 2023-03-11T17:32:46.323Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [HTTP/1.x vs. HTTP/2: Understanding the Differences and Improvements***English** document is available*](/en/Knowledge-base/Network/http1-x-vs-http2-understanding-the-differences-and-improvements)
{.links-list}



HTTP/1.x 대 HTTP/2: 차이점 및 개선 사항 이해

월드 와이드 웹은 지난 10년 동안 극적으로 발전했습니다. 더 빠르고 효율적인 웹 성능에 대한 요구가 증가함에 따라 레거시 프로토콜인 HTTP/1.x를 대체하기 위해 HTTP/2가 도입되었습니다. 이 기사에서는 HTTP/1.x와 HTTP/2의 차이점과 HTTP/2가 웹 성능을 향상시키는 방법에 대해 설명합니다.

## HTTP란?

HTTP(Hypertext Transfer Protocol)는 웹 서버와 클라이언트 간의 통신에 사용되는 기본 프로토콜입니다. World Wide Web의 기반이며 클라이언트가 HTML 콘텐츠, 이미지 및 기타 리소스로 응답하도록 웹 페이지 및 서버를 요청할 수 있습니다.

## HTTP/1.x

HTTP/1.x는 20년 이상 사용된 레거시 프로토콜입니다. 리소스를 로드하기 위해 여러 연결에 의존하는 텍스트 기반 프로토콜입니다. 브라우저가 웹 페이지를 요청하면 HTML, CSS 및 JavaScript와 같은 다양한 리소스를 로드하기 위해 서버에 대한 다중 연결을 설정합니다. 이 프로세스는 "head-of-line blocking" 문제로 알려져 있으며 느리게 로드되는 리소스가 다른 리소스의 로드를 차단하여 웹 성능을 저하시킵니다.

## HTTP/2

반면 HTTP/2는 HTTP/1.x에 비해 몇 가지 주요 개선 사항을 도입한 이진 프로토콜입니다. 단일 연결을 사용하여 리소스를 로드함으로써 HOL(head-of-line) 차단 문제를 해결합니다. 이를 통해 서버는 리소스의 우선 순위를 지정하고 보다 효율적으로 로드할 수 있으므로 웹 성능이 빨라집니다. 또한 HTTP/2는 "서버 푸시"라는 기술을 사용하여 서버가 리소스를 요청하기 전에 사전에 클라이언트에 보낼 수 있습니다.

## HTTP/2의 주요 개선 사항

### 멀티플렉싱

HTTP/2를 사용하면 단일 연결을 통해 여러 요청과 응답을 보낼 수 있으므로 웹 성능이 크게 향상됩니다. HTTP/1.x에서는 서로 다른 리소스를 로드하기 위해 여러 연결이 설정되어 헤드 오브 라인 차단 문제로 인해 웹 성능이 느려졌습니다. HTTP/2를 사용하면 단일 연결을 통해 동시에 여러 요청과 응답을 보낼 수 있으므로 웹 리소스를 더 빠르고 효율적으로 로드할 수 있습니다.

### 서버 푸시

HTTP/2는 "서버 푸시"라는 기능을 도입하여 서버가 사전에 리소스를 클라이언트에 보낼 수 있도록 합니다. 이 기술을 사용하면 클라이언트가 리소스를 요청할 필요가 없으므로 웹 성능이 빨라집니다. 예를 들어 클라이언트가 이미지가 포함된 웹 페이지를 요청하는 경우 서버는 해당 이미지가 요청되기 전에 사전에 클라이언트에 보낼 수 있습니다. 이렇게 하면 여러 요청 및 응답이 필요하지 않으므로 로드 시간이 빨라집니다.

### 헤더 압축

HTTP/2는 네트워크를 통해 전송되기 전에 헤더 데이터를 압축하는 헤더 압축이라는 기술을 사용합니다. 이렇게 하면 전송해야 하는 데이터의 양이 크게 줄어들어 웹 성능이 빨라집니다. HTTP/1.x는 헤더 압축을 지원하지 않아 전송해야 하는 데이터 양이 증가하여 웹 성능이 느려졌습니다.

## HTTP/2 구현

HTTP/2를 구현하려면 웹 서버와 클라이언트가 이를 지원하는지 확인해야 합니다. 최신 웹 서버와 브라우저는 대부분 HTTP/2를 지원하므로 웹 서버와 클라이언트를 최신 버전으로 업데이트하는 것이 중요합니다. 또한 HTTP/2에는 SSL/TLS 암호화가 필요하므로 웹 서버가 유효한 SSL 인증서로 구성되어 있는지 확인해야 합니다.

다음은 NGINX 구성 파일을 사용하여 HTTP/2를 구현하는 방법의 예입니다.

```nginx
server {
  listen 443 ssl http2;
  server_name example.com;

  ssl_certificate /path/to/certificate.crt;
  ssl_certificate_key /path/to/privatekey.key;

  // Other NGINX configuration options
}
```

## 결론

HTTP/2는 HTTP/1.x에 비해 크게 개선되어 더 빠르고 효율적인 웹 성능을 제공합니다. 단일 연결을 사용하여 리소스를 로드함으로써 HTTP/2는 HOL(head-of-line) 차단 문제를 해결하고 서버가 사전에 클라이언트에 리소스를 보낼 수 있도록 합니다. 또한 HTTP/2는 헤더 압축을 사용하여 네트워크를 통해 전송되는 데이터의 양을 줄여 웹 성능을 향상시킵니다. HTTP/2를 구현하려면 웹 서버와 클라이언트가 이를 지원하는지 확인하고 SSL/TLS 암호화를 구성해야 합니다. HTTP/2를 사용하면 웹 애플리케이션의 성능을 크게 향상시킬 수 있습니다.

## 외부 리소스

- [HTTP/2 - IETF](https://tools.ietf.org/html/rfc7540)
- [HTTP/2 vs HTTP/1: 성능 분석](https://kinsta.com/blog/http2-vs-http1/)
- [HTTP/2: 인터넷의 미래](https://www.cloudflare.com/learning/http2/what-is-http2/)