---
title: 보안 API 액세스를 위한 CORS(Cross-Origin Resource Sharing) 활성화
description: 
published: true
date: 2023-02-05T01:17:32.821Z
tags: 
editor: markdown
dateCreated: 2023-02-05T01:17:31.135Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Enabling Cross-Origin Resource Sharing (CORS) for Secure API Access***English** document is available*](/en/Knowledge-base/Backend/enabling-cross-origin-resource-sharing-cors-for-secure-api-access)
{.links-list}


# 보안 API 액세스를 위한 CORS(Cross-Origin Resource Sharing) 활성화

## 소개

간단히 말해서 CORS(Cross-Origin Resource Sharing)는 웹 페이지의 제한된 리소스가 첫 번째 리소스가 제공되는 도메인 외부의 다른 도메인에서 요청될 수 있도록 허용하는 메커니즘입니다. 웹 페이지는 원본 간 이미지, 스타일시트, 스크립트, iframe 및 비디오를 자유롭게 포함할 수 있습니다.

브라우저가 출처 간 요청을 하려면 웹 애플리케이션에서 먼저 CORS를 활성화해야 합니다. 동일한 출처 요청, 즉 페이지 자체와 동일한 도메인, 프로토콜 및 포트 번호에 대한 요청에는 CORS를 활성화할 필요가 없습니다.

## CORS 작동 방식

브라우저가 교차 출처 요청을 할 때 브라우저는 `Origin` 헤더와 함께 서버에 요청을 보냅니다. 'Origin' 헤더는 요청의 출처, 즉 요청이 시작된 도메인, 프로토콜 및 포트 번호를 나타냅니다.

그런 다음 서버는 'Origin' 헤더를 기반으로 요청을 허용하거나 차단하도록 선택할 수 있습니다. 서버가 요청을 허용하면 응답에 'Access-Control-Allow-Origin' 헤더를 설정합니다. `Access-Control-Allow-Origin` 헤더의 값은 특정 출처(예: `https://example.com`), 와일드카드(`*`) 또는 `null`일 수 있습니다.

응답에 'Access-Control-Allow-Origin' 헤더가 없거나 해당 값이 유효한 출처가 아닌 경우 브라우저는 응답을 차단합니다.

## CORS가 중요한 이유

CORS가 없으면 원본 간 요청이 브라우저에 의해 차단됩니다. 이것은 악의적인 스크립트가 API에 대한 무단 요청을 하지 못하도록 방지하기 때문에 중요합니다.

## CORS 활성화

### 'Access-Control-Allow-Origin' 헤더 설정

'Access-Control-Allow-Origin' 헤더는 브라우저에 요청이 시작된 출처의 교차 출처 요청을 허용해야 하는지 여부를 알려줍니다.

서버의 HTTP 응답에서 `Access-Control-Allow-Origin` 헤더를 설정할 수 있습니다. 헤더 값은 특정 출처(예: `https://example.com`), 와일드카드(`*`) 또는 `null`일 수 있습니다.

모든 출처의 교차 출처 요청을 허용하려면 `Access-Control-Allow-Origin` 헤더를 `*`로 설정할 수 있습니다.

```
Access-Control-Allow-Origin: *
```

특정 오리진의 교차 오리진 요청을 허용하려면 'Access-Control-Allow-Origin' 헤더를 요청 오리진으로 설정할 수 있습니다.

```
Access-Control-Allow-Origin: https://example.com
```

여러 오리진의 교차 오리진 요청을 허용하려면 'Access-Control-Allow-Origin' 헤더를 쉼표로 구분된 오리진 목록으로 설정할 수 있습니다.

```
Access-Control-Allow-Origin: https://example.com,https://example.org
```

특정 출처를 제외한 모든 출처의 교차 출처 요청을 허용하려면 `Access-Control-Allow-Origin` 헤더를 `*`로, `Access-Control-Expose-Headers` 헤더를 `Origin`으로 설정하면 됩니다. `.

```
Access-Control-Allow-Origin: *
Access-Control-Expose-Headers: Origin
```

### 'Access-Control-Allow-Credentials' 헤더 설정

'Access-Control-Allow-Credentials' 헤더는 원본 간 요청과 함께 쿠키를 보내야 하는지 여부를 브라우저에 알려줍니다.

쿠키가 교차 출처 요청과 함께 전송되도록 허용하려면 `Access-Control-Allow-Credentials` 헤더를 `true`로 설정할 수 있습니다.

```
Access-Control-Allow-Credentials: true
```

특정 오리진에서 교차 오리진 요청과 함께 쿠키를 보낼 수 있도록 하려면 'Access-Control-Allow-Origin' 헤더를 요청 오리진으로 설정하고 'Access-Control-Allow-Credentials' 헤더를 `true`로 설정합니다.

```
Access-Control-Allow-Origin: https://example.com
Access-Control-Allow-Credentials: true
```

### `Access-Control-Expose-Headers` 헤더 설정

'Access-Control-Expose-Headers' 헤더는 클라이언트에 노출되도록 허용해야 하는 헤더를 브라우저에 알려줍니다.

교차 출처 요청이 모든 헤더를 노출하도록 허용하려면 `Access-Control-Expose-Headers` 헤더를 `*`로 설정할 수 있습니다.

```
Access-Control-Expose-Headers: *
```

교차 출처 요청이 특정 헤더를 노출하도록 허용하려면 'Access-Control-Expose-Headers' 헤더를 허용하려는 헤더로 설정할 수 있습니다.

```
Access-Control-Expose-Headers: Content-Type
```

교차 출처 요청이 여러 헤더를 노출하도록 허용하려면 `Access-Control-Expose-Headers` 헤더를 쉼표로 구분된 헤더 목록으로 설정할 수 있습니다.

```
Access-Control-Expose-Headers: Content-Type,X-Custom-Header
```

## 사전 요청

일부 교차 출처 요청은 사전 처리됩니다. 프리플라이트 요청은 `OPTIONS` HTTP 메서드로 만들어지고 `Origin` 헤더가 있는 요청입니다.

브라우저는 서버가 원본 간 요청을 허용하는지 확인하기 위해 프리플라이트 요청을 서버로 보냅니다. 서버는 실행 전 요청을 허용하거나 차단하도록 선택할 수 있습니다.

서버가 실행 전 요청을 허용하면 응답에 'Access-Control-Allow-Methods' 헤더를 설정합니다. 'Access-Control-Allow-Methods' 헤더의 값은 서버가 허용하는 쉼표로 구분된 HTTP 메서드 목록입니다.

서버가 실행 전 요청을 허용하고 요청 방법이 `GET`, `HEAD` 또는 `POST`인 경우 서버는 응답에 `Access-Control-Allow-Headers` 헤더를 설정합니다. 'Access-Control-Allow-Headers' 헤더의 값은 서버가 허용하는 쉼표로 구분된 HTTP 헤더 목록입니다.

## CORS 및 보안

CORS는 악의적인 요청으로부터 API를 보호하는 데 사용할 수 있는 보안 메커니즘입니다. CORS를 활성화하면 API에 교차 출처 요청을 할 수 있는 출처를 지정할 수 있습니다.

## 결론

이 기사에서는 CORS가 무엇인지, 어떻게 작동하는지, 왜 중요한지 다루었습니다. 서버에서 CORS를 활성화하는 방법도 보여주었습니다.