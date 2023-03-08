---
title: HTTP 콘텐츠 협상: 서로 다른 클라이언트에 서로 다른 콘텐츠를 제공하는 방법
description: 
published: true
date: 2023-03-08T00:32:35.084Z
tags: 
editor: markdown
dateCreated: 2023-03-08T00:32:35.084Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [HTTP Content Negotiation: How to Serve Different Content for Different Clients***English** document is available*](/en/Knowledge-base/Network/http-content-negotiation-how-to-serve-different-content-for-different-clients)
{.links-list}



HTTP 콘텐츠 협상: 서로 다른 클라이언트에 서로 다른 콘텐츠를 제공하는 방법

개발자로서 올바른 클라이언트에게 올바른 유형의 콘텐츠를 제공하는 것이 중요합니다. 여기에서 HTTP 콘텐츠 협상이 유용합니다. HTTP 콘텐츠 협상은 여러 표현을 사용할 수 있을 때 리소스의 가장 적절한 표현을 선택하는 프로세스입니다. 이를 통해 개발자는 클라이언트의 요구 사항, 기능 및 기본 설정에 따라 다양한 유형의 콘텐츠(예: HTML, JSON, XML)를 제공할 수 있습니다.

## HTTP 콘텐츠 협상 이해

HTTP 콘텐츠 협상에는 클라이언트, 서버 및 리소스의 세 가지 구성 요소가 포함됩니다. 클라이언트가 서버에 리소스를 요청할 때 Accept 헤더 필드가 포함된 HTTP 요청 메시지를 보냅니다. Accept 헤더 필드는 클라이언트가 처리할 수 있는 MIME 유형을 나열합니다. 그러면 서버는 요청을 검사하고 Accept 헤더 필드를 기반으로 리소스의 가장 적절한 표현을 선택합니다.

콘텐츠 협상에는 클라이언트 중심과 서버 중심의 두 가지 유형이 있습니다. 클라이언트 중심 콘텐츠 협상에서 클라이언트는 선호하는 표현 유형을 지정하고 서버는 가장 적절한 표현으로 응답합니다. 서버 중심 콘텐츠 협상에서 서버는 클라이언트의 기능과 선호도에 따라 가장 적절한 표현을 선택합니다.

## HTTP 콘텐츠 협상 구현

HTTP 콘텐츠 협상을 구현하려면 개발자는 서버측 및 클라이언트측 기술을 조합하여 사용해야 합니다. 다음은 개발자가 고려할 수 있는 몇 가지 접근 방식입니다.

### URL 기반 콘텐츠 협상 사용

콘텐츠 협상을 구현하는 한 가지 방법은 URL 기반 콘텐츠 협상을 사용하는 것입니다. 이 방법에는 동일한 리소스의 다른 표현을 가리키는 여러 URL을 만드는 작업이 포함됩니다. 예를 들어 HTML 및 JSON 형식으로 모두 표현할 수 있는 리소스가 있다고 가정합니다. 이 경우 두 개의 URL을 만들 수 있습니다. 하나는 HTML 표현을 가리키는 것이고 다른 하나는 JSON 표현을 가리키는 것입니다.

그러나 이 접근 방식은 URL 확산으로 이어져 URL을 관리하고 유지하기 어렵게 만들 수 있습니다.

### 쿼리 기반 콘텐츠 협상 사용

콘텐츠 협상을 구현하는 또 다른 방법은 쿼리 기반 콘텐츠 협상을 사용하는 것입니다. 이 방법은 표시 유형을 지정하기 위해 쿼리 매개변수를 URL에 추가하는 것과 관련됩니다. 예를 들어 HTML 및 JSON 형식으로 모두 표현할 수 있는 리소스가 있다고 가정합니다. 이 경우 URL에 조회 매개변수를 추가하여 표시 유형을 지정할 수 있습니다.

```{Python}
http://example.com/resource?id=123&format=json
```

이 접근 방식은 개발자가 여러 URL을 생성하지 않고도 표현 유형을 지정할 수 있기 때문에 URL 기반 콘텐츠 협상보다 더 유연합니다. 그러나 이 접근 방식은 URL을 더 길고 읽기 어렵게 만들 수 있습니다.

### 헤더 기반 콘텐츠 협상 사용

콘텐츠 협상을 구현하는 가장 일반적인 방법은 헤더 기반 콘텐츠 협상을 사용하는 것입니다. 이 방법은 Accept 헤더 필드를 사용하여 표시 유형을 지정하는 것과 관련됩니다. 서버는 Accept 헤더 필드를 검사하고 가장 적절한 표현을 선택합니다.

다음은 Python에서 `requests` 라이브러리와 함께 헤더 기반 콘텐츠 협상을 사용하는 방법의 예입니다.

```{Python}
import requests

url = "http://example.com/resource"
headers = {'Accept': 'application/json'}
response = requests.get(url, headers=headers)
```

이 예에서 `Accept` 헤더 필드는 `application/json`으로 설정되어 클라이언트가 JSON 표현을 선호함을 나타냅니다. 서버는 `Accept` 헤더 필드를 검사하고 JSON 표현으로 응답합니다.

## HTTP 콘텐츠 협상을 위한 모범 사례

다음은 HTTP 콘텐츠 협상을 구현할 때 개발자가 따라야 하는 몇 가지 모범 사례입니다.

### 기본 표현 제공

항상 리소스에 대한 기본 표현을 제공하십시오. 기본 표현은 콘텐츠 협상을 지원하지 않는 클라이언트가 리소스에 계속 액세스할 수 있도록 합니다.

### 표준 MIME 유형 따르기

새 MIME 유형을 정의할 때는 항상 표준 MIME 유형을 따르십시오. 표준 MIME 유형은 클라이언트와 서버가 표현 형식을 이해할 수 있도록 합니다.

### 오류 응답 처리

개발자는 서버가 요청된 표현을 제공할 수 없을 때 오류 응답을 처리해야 합니다. 예를 들어 클라이언트가 지원되지 않는 MIME 유형을 요청하면 서버는 406 Not Acceptable 상태 코드로 응답해야 합니다.

## 결론

HTTP 콘텐츠 협상은 웹 개발의 중요한 측면입니다. 이를 통해 개발자는 클라이언트의 요구 사항, 기능 및 기본 설정에 따라 다양한 유형의 콘텐츠를 제공할 수 있습니다. 개발자는 서버측 및 클라이언트측 기술을 조합하여 콘텐츠 협상을 구현할 수 있습니다. 그러나 개발자는 구현이 강력하고 신뢰할 수 있도록 모범 사례를 따라야 합니다.

## 외부 리소스

- [HTTP 콘텐츠 협상 - MDN 웹 문서](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation)
- [콘텐츠 협상 - REST API 튜토리얼](https://restfulapi.net/content-negotiation/)
- [HTTP 콘텐츠 협상: 종합 가이드 - DZone](https://dzone.com/articles/http-content-negotiation-comprehensive-guide)