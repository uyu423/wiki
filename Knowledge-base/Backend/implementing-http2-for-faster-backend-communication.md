---
title: 더 빠른 백엔드 통신을 위한 HTTP/2 구현
description: 
published: true
date: 2023-02-15T02:17:17.761Z
tags: 
editor: markdown
dateCreated: 2023-02-15T02:17:16.210Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Implementing HTTP/2 for Faster Backend Communication***English** document is available*](/en/Knowledge-base/Backend/implementing-http2-for-faster-backend-communication)
{.links-list}


HTTP/2는 World Wide Web에서 사용되는 HTTP 네트워크 프로토콜의 주요 개정판입니다. 원래 Google에서 개발한 이전의 실험적인 SPDY 프로토콜에서 파생되었습니다. HTTP/2는 2015년 5월에 RFC 7540으로 게시되었습니다.

HTTP/2는 HTTP/1.x와 역호환되지 않으며 HTTPS가 필요합니다.

HTTP/2의 주요 목표는 전체 요청 및 응답 다중화를 활성화하여 대기 시간을 줄이고 압축 헤더를 통해 프로토콜 오버헤드를 최소화하며 요청 우선 순위 지정 및 서버 푸시에 대한 지원을 추가하는 것입니다.

HTTP/2는 텍스트가 아닌 바이너리입니다. 각 요청이 이전 요청이 완료될 때까지 기다리지 않고 단일 연결을 통해 여러 요청과 응답을 다중화합니다. 이를 통해 클라이언트와 서버 간의 보다 빠르고 효율적인 통신이 가능합니다.

HTTP/2는 또한 헤더 압축을 사용하여 HTTP/1.x보다 최대 80% 더 작은 헤더 크기를 줄입니다. 그 결과 네트워크를 통해 전송되는 데이터가 줄어들어 대기 시간이 줄어듭니다.

HTTP/2는 또한 클라이언트가 서버에서 요청을 처리해야 하는 순서를 지정할 수 있는 요청 우선 순위 지정을 지원합니다. 예를 들어 중요한 리소스를 먼저 로드하여 페이지 로딩 성능을 개선하는 데 사용할 수 있습니다.

마지막으로 HTTP/2는 서버 푸시에 대한 지원을 도입하여 클라이언트가 리소스를 요청하기도 전에 서버가 클라이언트에 필요할 것으로 예상되는 리소스를 사전에 보낼 수 있습니다. 이는 클라이언트가 필요한 모든 리소스를 가져오기 위해 서버를 여러 번 왕복할 필요가 없도록 하여 페이지 로딩 성능을 개선하는 데 사용할 수 있습니다.

 HTTP/2 구현

HTTP/2를 활용하려면 서버와 클라이언트가 모두 HTTP/2를 지원하는지 확인해야 합니다.

서버 측에서는 HTTP/2를 지원하는 웹 서버를 사용해야 합니다. 예를 들어 Apache HTTP Server는 2015년 12월에 출시된 버전 2.4.17부터 HTTP/2를 지원했습니다.

클라이언트 측에서는 HTTP/2를 지원하는 웹 브라우저를 사용해야 합니다. 예를 들어 Google Chrome, Mozilla Firefox, Microsoft Edge 및 Apple Safari를 비롯한 모든 주요 웹 브라우저는 현재 HTTP/2를 지원합니다.

서버와 클라이언트가 모두 HTTP/2를 지원하는지 확인한 후에는 웹 사이트에 액세스할 때 http:// 대신 https:// 프로토콜을 사용하여 HTTP/2를 사용할 수 있습니다. 서버는 클라이언트와 HTTP/2를 자동으로 협상하고 모든 통신은 HTTP/2를 통해 이루어집니다.

HTTPS 없이 HTTP/2를 사용하려면 일반 텍스트 TCP 연결을 통해 HTTP/2를 사용하도록 서버를 구성하면 됩니다. 그러나 이것은 HTTP/2의 많은 이점을 무효화하고 모든 클라이언트에서 지원되지 않기 때문에 일반적으로 권장되지 않습니다.

결론

HTTP/2는 HTTP/1.x에 비해 상당한 성능 향상을 제공하는 HTTP 네트워크 프로토콜의 주요 개정판입니다. HTTP/2를 활용하려면 서버와 클라이언트가 모두 HTTP/2를 지원하는지 확인해야 합니다. 이렇게 하면 웹 사이트에 액세스할 때 http:// 대신 https:// 프로토콜을 사용하여 HTTP/2를 사용할 수 있습니다.