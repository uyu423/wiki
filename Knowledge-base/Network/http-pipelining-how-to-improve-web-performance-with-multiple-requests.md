---
title: HTTP 파이프라이닝: 여러 요청으로 웹 성능을 개선하는 방법
description: 
published: true
date: 2023-03-10T06:32:44.261Z
tags: 
editor: markdown
dateCreated: 2023-03-10T06:32:44.261Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [HTTP Pipelining: How to Improve Web Performance with Multiple Requests***English** document is available*](/en/Knowledge-base/Network/http-pipelining-how-to-improve-web-performance-with-multiple-requests)
{.links-list}

HTTP 파이프라이닝: 여러 요청으로 웹 성능을 개선하는 방법

웹 애플리케이션이 더욱 복잡해짐에 따라 웹 성능을 최적화하는 것이 점점 더 중요해지고 있습니다. 이를 수행하는 한 가지 방법은 단일 연결을 통해 여러 요청을 보낼 수 있는 HTTP 파이프라이닝을 사용하는 것입니다. 이 기사에서는 HTTP 파이프라이닝이 무엇인지, 어떻게 작동하는지, 웹 애플리케이션에서 이를 구현하는 방법에 대해 알아봅니다.

## HTTP 파이프라이닝이란?

HTTP 파이프라이닝은 응답을 기다리지 않고 단일 TCP 연결을 통해 여러 HTTP 요청을 보내는 기술입니다. 이를 통해 더 빠른 데이터 전송이 가능하고 클라이언트와 서버 간의 왕복 시간으로 인한 대기 시간이 줄어듭니다.

## HTTP 파이프라이닝은 어떻게 작동합니까?

클라이언트가 HTTP 파이프라인을 사용하여 단일 연결을 통해 여러 요청을 보낼 때 서버는 이러한 요청을 수신하고 처리를 위해 대기열에 넣습니다. 그런 다음 서버는 요청이 수신된 순서대로 클라이언트에 응답을 다시 보냅니다.

HTTP 파이프라이닝은 HTTP/1.1 및 HTTP/2 프로토콜과 함께 사용할 수 있습니다. 그러나 HTTP/2가 이미 다중화를 통합하고 있다는 점은 주목할 가치가 있습니다. 즉, 단일 연결을 통해 동시에 여러 요청과 응답을 보낼 수 있습니다. 이렇게 하면 파이프라이닝 없이도 HTTP/2가 더 빨라집니다.

## HTTP 파이프라이닝 구현

웹 애플리케이션에서 HTTP 파이프라이닝을 구현하는 데 관심이 있는 경우 염두에 두어야 할 몇 가지 사항이 있습니다.

### 브라우저 호환성 확인

HTTP 파이프라이닝을 구현하기 전에 사용자가 사용 중인 브라우저가 이를 지원하는지 확인하는 것이 중요합니다. 일부 구형 브라우저는 파이프라이닝을 지원하지 않으므로 대체 솔루션을 구현하거나 파이프라이닝을 함께 사용하지 않는 것을 고려해야 할 수 있습니다.

### 서버 구성

HTTP 파이프라이닝을 활성화하려면 이를 허용하도록 서버를 구성해야 합니다. 예를 들어 Apache에서는 구성 파일에 다음 줄을 추가하여 HTTP 파이프라인을 활성화할 수 있습니다.

```
SetEnv nokeepalive ssl-unclean-shutdown \downgrade-1.0 force-response-1.0
```

### 애플리케이션 테스트

HTTP 파이프라이닝을 활성화한 후에는 웹 애플리케이션이 제대로 작동하는지 테스트하는 것이 중요합니다. cURL과 같은 도구를 사용하여 파이프라이닝이 올바르게 작동하는지 확인할 수 있습니다.

```
curl --http1.1 --no-buffer --header "Connection: keep-alive" --header "Accept-Encoding: gzip" --header "Transfer-Encoding: gzip" --header "User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36" http://example.com/index.html http://example.com/page1.html http://example.com/page2.html
```

### 다른 최적화 기술 고려

HTTP 파이프라이닝은 웹 성능을 향상시키는 효과적인 방법이 될 수 있지만 사용할 수 있는 유일한 기술은 아닙니다. 다른 최적화 기술에는 캐싱, 압축 및 서버 측 스크립팅이 포함됩니다. 최상의 결과를 얻으려면 이러한 기술을 조합하여 사용하는 것이 좋습니다.

## 결론

HTTP 파이프라이닝은 단일 연결을 통해 여러 요청을 보낼 수 있도록 하여 웹 성능을 향상시키는 데 유용한 기술입니다. 그러나 파이프라이닝을 활성화한 후 애플리케이션을 테스트하고 최상의 결과를 얻기 위해 다른 최적화 기술을 고려하는 것이 중요합니다. HTTP 파이프라이닝 및 기타 최적화 기술을 구현하여 사용자에게 더 빠르고 응답성이 뛰어난 웹 애플리케이션을 제공할 수 있습니다.

## 외부 리소스
- [HTTP 파이프라이닝 - Wikipedia](https://en.wikipedia.org/wiki/HTTP_pipelining)
- [HTTP/2 파이프라이닝의 장단점](https://blog.cloudflare.com/the-pros-and-cons-of-http2-pipelining/)
- [HTTP 파이프라이닝 - Mozilla 개발자 네트워크](https://developer.mozilla.org/en-US/docs/Web/HTTP/Connection_management_in_HTTP_1.x# HTTP_pipelining)