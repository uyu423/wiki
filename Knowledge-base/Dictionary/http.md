---
title: HTTP
description: 
published: true
date: 2023-03-08T19:32:54.530Z
tags: 
editor: markdown
dateCreated: 2023-03-08T19:32:54.530Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [HTTP***English** document is available*](/en/Knowledge-base/Dictionary/http)
{.links-list}



# HTTP

## 개요

HTTP(Hypertext Transfer Protocol)는 웹 서버와 웹 클라이언트 간의 통신에 사용되는 프로토콜입니다. World Wide Web을 위한 데이터 통신의 기반입니다.

## 설명

HTTP는 클라이언트가 서버에 요청을 보내고 서버가 메시지로 응답하는 요청-응답 프로토콜입니다. 클라이언트는 일반적으로 웹 브라우저이고 서버는 웹 서버이지만 다른 유형의 클라이언트 및 서버도 사용할 수 있습니다.

HTTP는 클라이언트가 서버에 요청을 시작하고 서버가 요청에 응답하는 클라이언트-서버 모델을 사용합니다. 클라이언트는 요청 라인, 헤더 및 선택적 메시지 본문을 포함하는 요청 메시지를 보냅니다. 서버는 상태 표시줄, 헤더 및 선택적 메시지 본문으로 응답합니다.

HTTP는 상태 비저장입니다. 즉, 각 요청은 이전 요청과 독립적입니다. 이를 통해 여러 클라이언트가 서로 간섭하지 않고 서버와 통신할 수 있습니다.

HTTP는 클라이언트가 서버에 요청을 보내고 서버가 메시지로 응답하는 요청-응답 모델을 기반으로 합니다. 클라이언트는 일반적으로 웹 브라우저이고 서버는 웹 서버이지만 다른 유형의 클라이언트 및 서버도 사용할 수 있습니다.

HTTP는 클라이언트가 서버에 요청을 시작하고 서버가 요청에 응답하는 클라이언트-서버 모델을 사용합니다. 클라이언트는 요청 라인, 헤더 및 선택적 메시지 본문을 포함하는 요청 메시지를 보냅니다. 서버는 상태 표시줄, 헤더 및 선택적 메시지 본문으로 응답합니다.

HTTP는 상태 비저장입니다. 즉, 각 요청은 이전 요청과 독립적입니다. 이를 통해 여러 클라이언트가 서로 간섭하지 않고 서버와 통신할 수 있습니다.

## 역사

HTTP는 1991년 World Wide Web을 발명한 Tim Berners-Lee에 의해 처음 소개되었습니다. HTTP의 첫 번째 버전인 HTTP/0.9는 GET 요청만 지원하고 헤더를 포함하지 않는 단순한 프로토콜이었습니다. HTTP/1.0은 1996년에 출시되었으며 헤더, 캐싱 및 기타 기능에 대한 지원을 포함했습니다. HTTP/1.1은 1999년에 출시되었으며 오늘날 가장 널리 사용되는 HTTP 버전입니다. HTTP/2는 2015년에 출시되었으며 다중화, 서버 푸시 및 기타 기능에 대한 지원을 포함합니다.

## 특징

HTTP에는 웹 통신에 유용한 몇 가지 기능이 있습니다.

- **요청-응답 모델:** HTTP는 요청-응답 모델을 사용합니다. 즉, 클라이언트가 서버에 요청을 보내고 서버는 메시지로 응답합니다.

- **상태 비저장:** HTTP는 상태 비저장입니다. 즉, 각 요청은 이전 요청과 독립적입니다. 이를 통해 여러 클라이언트가 서로 간섭하지 않고 서버와 통신할 수 있습니다.

- **헤더:** HTTP에는 요청 또는 응답에 대한 추가 정보를 제공하는 헤더가 포함되어 있습니다.

- **캐싱:** HTTP는 클라이언트가 응답을 저장하고 나중에 재사용할 수 있도록 하는 캐싱을 지원합니다.

- **인증:** HTTP에는 서버가 특정 리소스에 대한 액세스를 제한할 수 있는 인증 지원이 포함되어 있습니다.

## 예

다음은 HTTP 요청 및 응답의 예입니다.

```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:58.0) Gecko/20100101 Firefox/58.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://www.example.com/
Connection: keep-alive
Upgrade-Insecure-Requests: 1

HTTP/1.1 200 OK
Date: Tue, 13 Feb 2018 19:38:33 GMT
Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.2k-fips PHP/5.4.16
Last-Modified: Mon, 12 Feb 2018 21:05:56 GMT
ETag: "10c-565f6d1c7d8c0"
Accept-Ranges: bytes
Content-Length: 268
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive
Content-Type: text/html; charset=UTF-8

<!DOCTYPE html>
<html>
<head>
	<title>Example Page</title>
</head>
<body>
	<h1>Welcome to the Example Page!</h1>
	<p>This is an example page.</p>
</body>
</html>
```

이 예에서 클라이언트는 "index.html" 파일에 대해 서버에 GET 요청을 보냅니다. 서버는 200 OK 상태 코드로 응답하고 응답 본문의 파일 내용을 보냅니다.

## 장점과 단점

HTTP의 장점:

- **널리 사용됨:** HTTP는 World Wide Web을 위한 데이터 통신의 기반이며 널리 사용됩니다.

- **간단함:** HTTP는 이해하고 사용하기 쉬운 간단한 프로토콜입니다.

- **유연한:** HTTP는 다양한 애플리케이션에 사용할 수 있는 유연한 프로토콜입니다.

HTTP의 단점:

- **보안:** HTTP는 보안 프로토콜이 아니며 중간자 공격과 같은 공격에 취약할 수 있습니다.

- **성능:** 특정 유형의 애플리케이션, 특히 실시간 통신이 필요한 애플리케이션의 경우 HTTP가 느릴 수 있습니다.

## 논란

보안이 부족하기 때문에 HTTP 사용에 대한 논란이 있습니다. 일부에서는 공격으로부터 보호하기 위해 데이터를 암호화하므로 대신 HTTPS(HTTP Secure)를 사용해야 한다고 주장합니다. 그러나 다른 사람들은 HTTPS가 HTTP보다 느리고 구현하기가 더 복잡할 수 있다고 주장합니다.

## 관련 기술

HTTP는 다음과 같은 여러 다른 기술과 관련이 있습니다.

- **HTTPS:** HTTPS는 공격으로부터 보호하기 위해 데이터를 암호화하는 HTTP의 보안 버전입니다.

- **웹 브라우저:** 웹 브라우저는 HTTP를 사용하여 웹 서버와 통신하는 클라이언트입니다.

- **웹 서버:** 웹 서버는 HTTP를 사용하여 클라이언트와 통신하는 서버입니다.

## 여담

HTTP/3은 현재 개발 중인 최신 버전의 HTTP입니다. 성능과 보안을 개선하도록 설계된 QUIC 프로토콜을 기반으로 합니다. HTTP/3은 HTTP/2보다 빠르고 안전할 것으로 예상됩니다.

## 기타

HTTP는 웹 통신을 위한 중요한 프로토콜이며 널리 사용됩니다. 몇 가지 제한 사항이 있지만 광범위한 응용 프로그램에 사용할 수 있는 간단하고 유연한 프로토콜입니다. 기술이 계속 발전함에 따라 HTTP는 계속해서 웹 통신의 중요한 부분이 될 것입니다.