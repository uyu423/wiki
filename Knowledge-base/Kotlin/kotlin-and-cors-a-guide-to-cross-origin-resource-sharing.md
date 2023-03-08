---
title: Kotlin 및 CORS: 원본 간 리소스 공유 가이드
description: 
published: true
date: 2023-02-12T06:56:07.056Z
tags: 
editor: markdown
dateCreated: 2023-02-12T06:56:05.328Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and CORS: A Guide to Cross-Origin Resource Sharing***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-cors-a-guide-to-cross-origin-resource-sharing)
{.links-list}

      
Kotlin 및 CORS: 원본 간 리소스 공유 가이드

CORS(Cross-Origin Resource Sharing)는 첫 번째 리소스가 제공된 도메인 외부의 다른 도메인에서 웹 페이지의 제한된 리소스를 요청할 수 있도록 허용하는 메커니즘입니다. 웹 페이지는 원본 간 이미지, 스타일시트, 스크립트, iframe 및 비디오를 자유롭게 포함할 수 있습니다.

CORS 메커니즘은 도메인 간 HTTP 요청 및 응답에 HTTP 헤더를 추가하여 작동합니다.

## CORS는 어떻게 작동하나요?

브라우저가 서버에 요청을 보낼 때 브라우저에는 Origin 헤더가 포함됩니다. 이 헤더는 요청하는 페이지의 도메인을 나타냅니다.

그런 다음 서버는 Origin 헤더 값에 따라 요청을 허용하거나 거부하도록 선택할 수 있습니다.

서버가 요청을 허용하면 응답에 다음 헤더가 포함됩니다.
- Access-Control-Allow-Origin: 이 헤더는 서버가 원본 간 요청을 허용함을 나타냅니다.
- Access-Control-Allow-Methods: 이 헤더는 클라이언트가 사용할 수 있는 방법(예: GET, POST 등)을 나타냅니다.
- Access-Control-Allow-Headers: 이 헤더는 클라이언트가 사용할 수 있는 헤더를 나타냅니다.
- Access-Control-Expose-Headers: 이 헤더는 클라이언트가 액세스할 수 있는 헤더를 나타냅니다.

서버가 요청을 허용하지 않으면 오류를 반환합니다.

## CORS가 중요한 이유는 무엇입니까?

CORS 메커니즘은 브라우저 기반 애플리케이션이 동일한 출처 정책을 준수하면서 교차 출처 요청을 할 수 있는 방법을 제공합니다.

동일 출처 정책은 출처 간 요청을 방지하도록 설계된 보안 수단입니다. 그러나 데이터를 검색하거나 타사 서비스를 사용하기 위해 다른 도메인에 요청하는 것과 같이 원본 간 요청에 대한 많은 합법적인 용도가 있습니다.

CORS는 이러한 유형의 원본 간 요청을 허용하는 동시에 악의적인 요청에 대한 보호를 제공하는 방법을 제공합니다.

## CORS의 몇 가지 예는 무엇입니까?

다음은 CORS를 사용하는 방법에 대한 몇 가지 예입니다.

- 타사 서비스에서 데이터를 검색하기 위해 출처 간 요청을 하는 웹 페이지입니다.
- 다른 도메인에서 스크립트를 로드하기 위해 교차 출처 요청을 하는 웹 페이지입니다.
- 페이지에 포함된 iframe에 교차 출처 요청을 하는 웹 페이지입니다.

## CORS의 몇 가지 제한 사항은 무엇입니까?

CORS는 완벽한 솔루션이 아닙니다. 가장 큰 제한은 모든 브라우저에서 지원되지 않는다는 것입니다.

또한 CORS는 악의적인 요청에 의해 우회될 수 있습니다. 예를 들어 악의적인 요청은 XMLHttpRequest 개체를 사용하여 CORS 헤더 없이 원본 간 요청을 할 수 있습니다.

## CORS는 어떻게 사용하나요?

CORS를 사용하려면 CORS를 지원하는 서버를 설정해야 합니다.

 서버 설정은 이 문서의 범위를 벗어나지만 아래 리소스 섹션에서 자세한 정보를 찾을 수 있습니다.

CORS 지원 서버가 있으면 XMLHttpRequest 또는 Fetch API를 사용하여 출처 간 요청을 할 수 있습니다.

## 프리플라이트 요청이란 무엇입니까?

실행 전 요청은 원본 간 요청 전에 전송되는 HTTP 요청입니다. 프리플라이트 요청은 원본 간 요청을 안전하게 보낼 수 있는지 확인하는 데 사용됩니다.

실행 전 요청은 다음 헤더와 함께 전송됩니다.
- 원본: 요청하는 페이지의 도메인입니다.
- Access-Control-Request-Method: 교차 출처 요청에 사용될 방법(예: GET, POST 등).
- Access-Control-Request-Headers: 원본 간 요청에 사용될 헤더입니다.

그런 다음 서버는 이러한 헤더 값에 따라 요청을 허용하거나 거부하도록 선택할 수 있습니다.

서버가 요청을 허용하면 응답에 다음 헤더가 포함됩니다.
- Access-Control-Allow-Origin: 이 헤더는 서버가 원본 간 요청을 허용함을 나타냅니다.
- Access-Control-Allow-Methods: 이 헤더는 클라이언트가 사용할 수 있는 방법(예: GET, POST 등)을 나타냅니다.
- Access-Control-Allow-Headers: 이 헤더는 클라이언트가 사용할 수 있는 헤더를 나타냅니다.
- Access-Control-Max-Age: 이 헤더는 응답을 캐시할 수 있는 기간을 나타냅니다.

서버가 요청을 허용하지 않으면 오류를 반환합니다.

## 프리플라이트 요청이란 무엇입니까?

실행 전 요청은 원본 간 요청 전에 전송되는 HTTP 요청입니다. 프리플라이트 요청은 원본 간 요청을 안전하게 보낼 수 있는지 확인하는 데 사용됩니다.

실행 전 요청은 다음 헤더와 함께 전송됩니다.
- 원본: 요청하는 페이지의 도메인입니다.
- Access-Control-Request-Method: 교차 출처 요청에 사용될 방법(예: GET, POST 등).
- Access-Control-Request-Headers: 원본 간 요청에 사용될 헤더입니다.

그런 다음 서버는 이러한 헤더 값에 따라 요청을 허용하거나 거부하도록 선택할 수 있습니다.

서버가 요청을 허용하면 응답에 다음 헤더가 포함됩니다.
- Access-Control-Allow-Origin: 이 헤더는 서버가 원본 간 요청을 허용함을 나타냅니다.
- Access-Control-Allow-Methods: 이 헤더는 클라이언트가 사용할 수 있는 방법(예: GET, POST 등)을 나타냅니다.
- Access-Control-Allow-Headers: 이 헤더는 클라이언트가 사용할 수 있는 헤더를 나타냅니다.
- Access-Control-Max-Age: 이 헤더는 응답을 캐시할 수 있는 기간을 나타냅니다.

서버가 요청을 허용하지 않으면 오류를 반환합니다.

## CORS 사용에 대한 몇 가지 팁은 무엇입니까?

다음은 CORS 사용에 대한 몇 가지 팁입니다.

- XMLHttpRequest 또는 Fetch API를 사용하여 원본 간 요청을 만듭니다.
- Origin 헤더를 요청하는 페이지의 도메인으로 설정합니다.
- Access-Control-Request-Method 헤더를 교차 출처 요청에 사용할 메소드(예: GET, POST 등)로 설정합니다.
- Access-Control-Request-Headers 헤더를 원본 간 요청에 사용할 헤더로 설정합니다.
- 서버가 요청을 허용하면 응답에 Access-Control-Allow-Origin, Access-Control-Allow-Methods, Access-Control-Allow-Headers 및 Access-Control-Max-Age 헤더가 포함됩니다. .
- 서버가 요청을 허용하지 않으면 오류를 반환합니다.

## 결론

CORS는 첫 번째 리소스가 제공된 도메인 외부의 다른 도메인에서 웹 페이지의 제한된 리소스를 요청할 수 있도록 허용하는 메커니즘입니다. 웹 페이지는 원본 간 이미지, 스타일시트, 스크립트, iframe 및 비디오를 자유롭게 포함할 수 있습니다.

CORS 메커니즘은 도메인 간 HTTP 요청 및 응답에 HTTP 헤더를 추가하여 작동합니다.

브라우저가 서버에 요청을 보낼 때 브라우저에는 Origin 헤더가 포함됩니다. 이 헤더는 요청하는 페이지의 도메인을 나타냅니다.

그런 다음 서버는 Origin 헤더 값에 따라 요청을 허용하거나 거부하도록 선택할 수 있습니다.

서버가 요청을 허용하면 응답에 Access-Control-Allow-Origin, Access-Control-Allow-Methods, Access-Control-Allow-Headers 및 Access-Control-Expose-Headers 헤더가 포함됩니다.

서버가 요청을 허용하지 않으면 오류를 반환합니다.

CORS 메커니즘은 브라우저 기반 애플리케이션이 동일한 출처 정책을 준수하면서 교차 출처 요청을 할 수 있는 방법을 제공합니다.

동일 출처 정책은 출처 간 요청을 방지하도록 설계된 보안 조치입니다. 그러나 데이터를 검색하거나 타사 서비스를 사용하기 위해 다른 도메인에 요청하는 것과 같이 원본 간 요청에 대한 많은 합법적인 용도가 있습니다.

CORS는 이러한 유형의 원본 간 요청을 허용하는 동시에 악의적인 요청에 대한 보호를 제공하는 방법을 제공합니다.

CORS를 사용하려면 CORS를 지원하는 서버를 설정해야 합니다. 서버 설정은 이 문서의 범위를 벗어나지만 아래 리소스 섹션에서 자세한 정보를 찾을 수 있습니다.

CORS 지원 서버가 있으면 XMLHttpRequest 또는 Fetch API를 사용하여 출처 간 요청을 할 수 있습니다.

실행 전 요청은 원본 간 요청 전에 전송되는 HTTP 요청입니다. 프리플라이트 요청은 원본 간 요청을 안전하게 보낼 수 있는지 확인하는 데 사용됩니다.

실행 전 요청은 Origin, Access-Control-Request-Method 및 Access-Control-Request-Headers 헤더와 함께 전송됩니다.

그런 다음 서버는 이러한 헤더 값에 따라 요청을 허용하거나 거부하도록 선택할 수 있습니다.

서버가 요청을 허용하면 응답에 Access-Control-Allow-Origin, Access-Control-Allow-Methods, Access-Control-Allow-Headers 및 Access-Control-Max-Age 헤더가 포함됩니다.

서버가 요청을 허용하지 않으면 오류를 반환합니다.

다음은 CORS 사용에 대한 몇 가지 팁입니다.

- XMLHttpRequest 또는 Fetch API를 사용하여 원본 간 요청을 만듭니다.
- Origin 헤더를 요청하는 페이지의 도메인으로 설정합니다.
- Access-Control-Request-Method 헤더를 교차 출처 요청에 사용할 메소드(예: GET, POST 등)로 설정합니다.
- Access-Control-Request-Headers 헤더를 원본 간 요청에 사용할 헤더로 설정합니다.
- 서버가 요청을 허용하면 응답에 Access-Control-Allow-Origin, Access-Control-Allow-Methods, Access-Control-Allow-Headers 및 Access-Control-Max-Age 헤더가 포함됩니다. .
- 서버가 요청을 허용하지 않으면 오류를 반환합니다.