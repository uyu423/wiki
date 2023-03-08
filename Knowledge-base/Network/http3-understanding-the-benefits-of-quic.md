---
title: HTTP/3: QUIC의 이점 이해
description: 
published: true
date: 2023-03-03T03:32:21.886Z
tags: 
editor: markdown
dateCreated: 2023-03-03T03:32:20.511Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [HTTP/3: Understanding the Benefits of QUIC***English** document is available*](/en/Knowledge-base/Network/http3-understanding-the-benefits-of-quic)
{.links-list}
HTTP/3: QUIC의 이점 이해

HTTP(Hypertext Transfer Protocol)는 인터넷을 통해 데이터를 전송하는 데 사용되는 기본 프로토콜입니다. HTTP의 현재 버전인 HTTP/2는 2015년에 도입되었으며 이전 버전인 HTTP/1.1에 비해 성능이 크게 향상되었습니다. 그러나 HTTP 관리를 담당하는 조직인 IETF(Internet Engineering Task Force)는 QUIC이라는 새로운 전송 프로토콜을 통합한 새로운 버전의 프로토콜인 HTTP/3을 개발하고 있습니다.

QUIC(빠른 UDP 인터넷 연결)은 Google에서 초기에 Chrome 브라우저의 성능을 개선하기 위한 방법으로 개발한 전송 계층 프로토콜입니다. 이제 개방형 표준이며 Mozilla 및 Cloudflare와 같은 다른 주요 업체에서 채택했습니다. QUIC의 목표는 대기 시간을 줄이고 인터넷 통신의 보안을 향상시키는 것입니다. 이 기사에서는 QUIC의 이점과 이를 HTTP/3에 통합하는 방법을 살펴봅니다.

## QUIC의 필요성

TCP(전송 제어 프로토콜)는 HTTP/1.1 및 HTTP/2에서 사용되는 전송 프로토콜입니다. 인터넷을 통해 안정적이고 순서가 지정된 데이터 전달을 제공하지만 몇 가지 제한 사항이 있습니다. TCP는 연결을 설정하기 위해 3방향 핸드셰이크가 필요하므로 통신에 대기 시간이 추가됩니다. 또한 TCP는 HOL(head-of-line) 차단에 취약합니다. 즉, 전송 중에 손실된 패킷은 재전송될 때까지 후속 패킷의 전달을 보류합니다. 이로 인해 페이지 로드 시간이 느려지고 사용자 경험이 저하될 수 있습니다.

반면에 UDP(User Datagram Protocol)는 신뢰성이나 순서 보장을 제공하지 않는 연결 없는 프로토콜입니다. 그러나 오버헤드가 적고 TCP보다 빠를 수 있습니다. QUIC은 UDP를 기반으로 하지만 제한 사항을 해결하기 위한 개선 사항이 포함되어 있습니다. QUIC은 TCP와 같이 안정적이고 순서가 지정된 데이터 전달을 제공하지만 3방향 핸드셰이크로 인한 대기 시간이 없습니다. 또한 패킷 수준 오류 수정을 사용하여 패킷 손실의 영향을 줄이고 HOL 차단을 방지합니다.

## QUIC의 이점

### 페이지 로드 시간 단축

QUIC은 UDP를 사용하여 더 빠른 연결을 허용하고 대기 시간을 줄이고 페이지 로드 시간을 개선합니다. QUIC의 연결 설정은 제로 왕복 시간 핸드셰이크를 사용합니다. 즉, 연결에 상당한 지연을 추가할 수 있는 3방향 핸드셰이크가 필요하지 않습니다. 따라서 QUIC은 대기 시간이 긴 연결을 사용하는 모바일 장치 및 사용자에게 특히 유리합니다.

### 향상된 보안

QUIC에는 내장 암호화가 포함되어 있어 TCP보다 더 안전합니다. 연결 설정, 헤더 및 페이로드를 포함하여 전송 중인 모든 데이터에 암호화가 적용됩니다. 이렇게 하면 중간자 공격 및 도청 가능성이 줄어듭니다.

### 패킷 손실 감소

패킷 손실은 인터넷에서 흔히 발생하는 현상이며 승인 패킷에 대한 TCP의 의존도는 패킷이 손실될 때 통신 속도를 저하시킬 수 있습니다. QUIC은 패킷 수준 오류 수정을 사용하므로 TCP보다 더 빠르게 손실된 패킷을 복구할 수 있습니다. 이렇게 하면 페이지 로드 시간에 대한 패킷 손실의 영향이 줄어들고 전반적인 성능이 향상됩니다.

### 멀티플렉싱

QUIC은 다중화를 지원하여 단일 연결을 통해 여러 개의 독립적인 데이터 스트림을 전송할 수 있습니다. 이것은 여러 요청이 동시에 전송될 수 있고 응답이 순서 없이 수신될 수 있음을 의미합니다. 이렇게 하면 여러 리소스를 다운로드하는 데 걸리는 시간을 줄여 페이지 로드 시간을 개선할 수 있습니다.

## QUIC로 HTTP/3 구현하기

HTTP/3은 기본 전송 프로토콜로 QUIC를 사용합니다. HTTP/2와 HTTP/3의 주요 차이점은 데이터가 전송되는 방식입니다. HTTP/2는 연결을 설정하기 위해 3방향 핸드셰이크가 필요한 TCP를 사용합니다. HTTP/3은 왕복 시간이 없는 핸드셰이크를 사용하는 QUIC를 사용합니다. 이는 HTTP/3이 HTTP/2보다 더 빠르게 연결을 설정할 수 있음을 의미합니다.

QUIC으로 HTTP/3을 구현하려면 서버 및 클라이언트 지원이 필요합니다. NGINX 및 Apache와 같은 많은 주요 웹 서버는 이미 HTTP/3을 지원합니다. 클라이언트 지원은 덜 광범위하지만 Chrome 및 Firefox와 같은 주요 브라우저는 HTTP/3에 대한 실험적 지원을 제공합니다.

다음은 NGINX를 사용하여 HTTP/3 서버를 구현하는 방법의 예입니다.

```nginx
http {
  listen 443 quic reuseport;
  listen [::]:443 quic reuseport;

  ssl_certificate /path/to/cert.pem;
  ssl_certificate_key /path/to/key.pem;

  location / {
    root /var/www/html;
  }
}
```

이 NGINX 구성은 QUIC를 사용하여 포트 443에서 HTTP/3 서버를 설정합니다. `ssl_certificate` 및 `ssl_certificate_key` 지시문은 서버의 SSL 인증서 및 키를 지정합니다. `location` 지시문은 서버 파일의 위치를 지정합니다.

## 결론

QUIC은 인터넷 통신의 성능과 보안을 개선하기 위해 개발된 새로운 전송 프로토콜입니다. 더 빠른 연결, 향상된 보안, 감소된 패킷 손실 및 멀티플렉싱을 제공합니다. HTTP/3은 기본 전송 프로토콜로 QUIC를 통합하고 HTTP/2에 비해 상당한 개선 사항을 제공합니다. QUIC으로 HTTP/3를 구현하려면 서버 및 클라이언트 지원이 필요하지만 업계의 주요 업체는 이미 이를 채택하고 있습니다. HTTP가 계속 발전함에 따라 개발자는 최신 프로토콜 및 표준을 최신 상태로 유지하여 애플리케이션에 대한 최상의 사용자 경험을 보장하는 것이 중요합니다.

## 외부 리소스

- [QUIC 홈페이지](https://www.chromium.org/quic)
- [HTTP/3 설명](https://http3-explained.haxx.se/)
- [NGINX HTTP/3 및 QUIC](https://www.nginx.com/blog/nginx-1-19-0-released/)
- [Mozilla의 QUIC 구현](https://blog.mozilla.org/press-uk/2021/07/29/mozilla-partners-with-cloudflare-to-improve-privacy-and-security-on-the- 편물/)