---
title: HTTP 3.0 with QUIC (HTTP 1.x / 2.0 과 비교)
description: 
published: true
date: 2023-04-19T05:35:30.498Z
tags: http, quic
editor: markdown
dateCreated: 2023-04-19T05:35:30.498Z
---

HTTP/3.0은 인터넷에서 데이터를 전송하는 프로토콜 중 가장 최신 기술 중 하나입니다. HTTP/3.0은 QUIC (Quick UDP Internet Connections) 프로토콜을 기반으로 하며, 이전 버전의 HTTP/1.x 및 HTTP/2.0과는 차별화된 기술적 특징을 가지고 있습니다.

이번 글에서는 HTTP/3.0과 QUIC에 대해 알아보고, HTTP/1.x 및 HTTP/2.0과 비교하여 어떤 차이점이 있는지 살펴보겠습니다.

## HTTP/3.0과 QUIC
HTTP/3.0은 QUIC 프로토콜을 기반으로 하며, UDP를 사용합니다. QUIC은 TCP와 UDP를 결합한 하이브리드 프로토콜입니다. QUIC은 TCP의 신뢰성과 연결 설정 기능과 UDP의 빠른 전송 속도를 결합하여, HTTP/3.0의 빠른 전송과 안정성을 보장합니다.

HTTP/3.0에서는 데이터를 전송하는 방식이 기존 버전과는 다릅니다. HTTP/3.0에서는 Stream과 Datagram을 사용하여 데이터를 전송합니다. Stream은 연결 상태를 유지하며 여러 개의 요청과 응답을 처리하며, Datagram은 연결 상태와 무관하게 작은 데이터를 처리합니다. 이렇게 Stream과 Datagram을 함께 사용하면, 데이터 전송 효율을 높이고, HOLB 문제를 회피할 수 있습니다.

HTTP/3.0에서는 헤더 압축 기술도 변경되었습니다. HTTP/2.0에서는 HPACK 압축 방식을 사용했지만, HTTP/3.0에서는 QPACK 압축 방식을 사용합니다. QPACK은 HPACK보다 더 효율적인 압축 기술을 제공하며, 빠른 전송을 가능하게 합니다.

> **QUIC (Quick UDP Internet Connections)**
> 
> HTTP/3.0은 QUIC (Quick UDP Internet Connections) 프로토콜을 기반으로 하며, 이전 버전의 HTTP/1.x 및 HTTP/2.0과는 차별화된 기술적 특징을 가지고 있습니다. QUIC은 TCP와 UDP를 결합한 하이브리드 프로토콜로, UDP를 사용하기 때문에 TCP의 지연 문제와 패킷 손실 문제를 회피할 수 있습니다.
> 
> QUIC은 기존 TCP 연결 설정 과정에서 발생하는 3-way handshake를 회피하여 연결 설정 시간을 단축시킵니다. 또한, QUIC은 연결 설정과 데이터 전송을 동시에 처리하여, 데이터 전송 속도를 높입니다. QUIC은 HTTP/3.0에서 데이터 전송을 위해 사용됩니다.
> 
> QUIC에서는 Stream과 Datagram을 사용하여 데이터를 전송합니다. Stream은 연결 상태를 유지하며 여러 개의 요청과 응답을 처리하며, Datagram은 연결 상태와 무관하게 작은 데이터를 처리합니다. 이렇게 Stream과 Datagram을 함께 사용하면, 데이터 전송 효율을 높이고, HOLB (Head-of-Line Blocking) 문제를 회피할 수 있습니다. 또한, QUIC은 헤더 압축 기술로 HPACK 대신 QPACK 압축 방식을 사용하여, 빠른 전송을 가능하게 합니다.
> ```mermaid
> sequenceDiagram
>     participant Client
>     participant Server
> 
>     Client->>Server: QUIC Client Initial (ClientHello)
>     Server->>Client: QUIC Server Initial (ServerHello, EncryptedExtensions, Certificate, CertificateVerify, Finished)
>     Client->>Server: QUIC Client Finished (Finished)
>     Client->>Server: QUIC STREAM frames (Request)
>     Server->>Client: QUIC STREAM frames (Response)
> ```
> 
> QUIC은 UDP를 사용하기 때문에, 일부 네트워크 장비에서는 UDP 패킷을 차단할 수 있습니다. 이러한 경우에는, HTTP/3.0을 사용하는 클라이언트와 서버가 QUIC-over-TLS를 사용하여, UDP를 TCP로 감싸고 TLS 암호화를 적용하는 방식으로 패킷 차단 문제를 회피할 수 있습니다.
> 
> HTTP/3.0과 QUIC은 인터넷에서 데이터를 전송하는 최신 기술 중 하나입니다. HTTP/3.0은 QUIC 프로토콜을 기반으로 하며, 이전 버전의 HTTP/1.x 및 HTTP/2.0과는 차별화된 기술적 특징을 가지고 있습니다. QUIC은 UDP를 사용하여 TCP의 지연 문제와 패킷 손실 문제를 회피하고, 연결 설정과 데이터 전송을 동시에 처리하여 데이터 전송 속도를 높입니다. 또한, Stream과 Datagram을 함께 사용하여 데이터 전송 효율을 높이고, QPACK 압축 방식을 사용하여 빠른 전송을 가능하게 합니다. 따라서, HTTP/3.0과 QUIC은 더욱 빠른 데이터 전송 속도와 안정성을 제공합니다.
> 
> 하지만, 아직까지 HTTP/3.0을 지원하는 클라이언트와 서버가 많이 보급되어 있지 않기 때문에, 호환성 문제가 발생할 수 있습니다. 또한, 일부 네트워크 장비에서는 UDP 패킷을 차단할 수 있기 때문에, QUIC-over-TLS를 사용하여 패킷 차단 문제를 회피해야 합니다.
> 
> 따라서, 개발자들은 HTTP/3.0과 QUIC에 대한 이해를 바탕으로 서비스를 구현하고, 최신 버전의 웹 서버와 브라우저를 사용하여 빠른 데이터 전송과 안정성을 제공하는 최신 기술을 활용해야 합니다. 또한, HTTP/3.0과 QUIC이 지속적으로 발전하고 있기 때문에, 개발자들은 최신 기술 동향을 살펴보고, 적극적으로 적용해 나가야 합니다.
{.is-info}


## HTTP/3.0과 HTTP/2.0, HTTP/1.x 비교

HTTP/3.0과 HTTP/2.0, HTTP/1.x의 가장 큰 차이점은 전송 프로토콜입니다. HTTP/1.x 및 HTTP/2.0은 TCP를 기반으로 하며, HTTP/2.0은 다중화(multiplexing)를 지원하여 여러 개의 요청과 응답을 처리할 수 있습니다. 이에 반해, HTTP/3.0은 QUIC을 기반으로 하며, Stream과 Datagram을 함께 사용하여 데이터를 전송합니다.

HTTP/3.0에서는 HOLB 문제를 회피할 수 있으며, 기존 버전보다 더욱 빠른 데이터 전송 속도와 안정성을 제공합니다. 또한, UDP를 사용하기 때문에 TCP의 지연 문제와 패킷 손실 문제를 회피할 수 있습니다.

또한, HTTP/3.0에서는 QPACK 압축 방식을 사용하여, 데이터 전송 효율을 높였습니다. HTTP/2.0에서 사용하는 HPACK보다 더욱 효율적인 압축 기술을 제공합니다.

하지만, HTTP/3.0을 지원하는 클라이언트와 서버가 아직까지 많이 보급되지 않았기 때문에, 호환성 문제가 발생할 수 있습니다. 또한, 일부 네트워크 장비에서는 HTTP/3.0을 지원하지 않을 수 있습니다.

## HTTP/3.0을 사용하는 방법

HTTP/3.0을 사용하려면, 다음과 같은 작업이 필요합니다.

### 서버와 클라이언트에서 HTTP/3.0을 지원하는지 확인
HTTP/3.0을 사용하려면, 서버와 클라이언트 모두가 HTTP/3.0을 지원해야 합니다. 따라서, HTTP/3.0을 사용하려면, 서버와 클라이언트 모두가 HTTP/3.0을 지원하는지 확인해야 합니다.

### 최신 버전의 웹 서버 사용
HTTP/3.0을 지원하는 웹 서버를 사용해야 합니다. 현재는 Apache, Nginx, Caddy, LiteSpeed 등 다양한 웹 서버가 HTTP/3.0을 지원하고 있습니다.

### 최신 버전의 브라우저 사용
HTTP/3.0을 지원하는 브라우저를 사용해야 합니다. 현재는 Chrome, Firefox, Opera, Edge 등 다양한 브라우저가 HTTP/3.0을 지원하고 있습니다.

### HTTPS 사용
HTTP/3.0은 HTTPS 프로토콜을 사용합니다. 따라서, HTTP/3.0을 사용하려면, HTTPS를 사용해야 합니다.

## 결론

HTTP/3.0은 최신 기술인 QUIC 프로토콜을 기반으로 하며, 이전 버전과는 차별화된 기술적 특징을 가지고 있습니다. HTTP/3.0은 빠른 데이터 전송 속도와 안정성을 제공하며, QPACK 압축 방식을 사용하여 데이터 전송 효율을 높였습니다.

하지만, 아직까지 HTTP/3.0을 지원하는 클라이언트와 서버가 많이 보급되어 있지 않기 때문에, 호환성 문제가 발생할 수 있습니다. 따라서, HTTP /3.0을 사용하기 전에, 서버와 클라이언트가 HTTP/3.0을 지원하는지 확인하고, 최신 버전의 웹 서버와 브라우저를 사용해야 합니다. 또한, HTTPS 프로토콜을 사용해야 하며, 일부 네트워크 장비에서는 HTTP/3.0을 지원하지 않을 수 있습니다.

HTTP/3.0은 지속적으로 발전하고 있으며, 앞으로 더 많은 웹 서비스에서 사용될 것으로 예상됩니다. 따라서, 개발자들은 HTTP/3.0의 기술적 특징과 사용 방법을 숙지하고, 서비스에 적용하여 빠른 데이터 전송과 안정성을 제공하는 최신 기술을 활용해야 합니다.