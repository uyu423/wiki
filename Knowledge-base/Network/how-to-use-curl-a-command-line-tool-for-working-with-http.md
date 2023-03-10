---
title: cURL 사용 방법: HTTP 작업을 위한 명령줄 도구
description: 
published: true
date: 2023-03-10T05:32:45.332Z
tags: 
editor: markdown
dateCreated: 2023-03-10T05:32:45.332Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Use cURL: A Command-Line Tool for Working with HTTP***English** document is available*](/en/Knowledge-base/Network/how-to-use-curl-a-command-line-tool-for-working-with-http)
{.links-list}

## 소개

HTTP로 작업하는 경우 cURL에 대해 들어봤을 것입니다. 그러나 cURL이 정확히 무엇입니까? 지원되는 많은 프로토콜 중 하나를 사용하여 서버에서 또는 서버로 데이터를 전송할 수 있는 명령줄 도구입니다. 이 문서에서는 cURL을 효과적으로 사용하여 HTTP 작업을 수행하는 방법을 살펴보겠습니다.

## cURL 설치

cURL을 사용하기 전에 cURL이 설치되어 있는지 확인하십시오. Unix 기반 시스템을 사용하는 경우 cURL이 이미 설치되어 있을 수 있습니다. 확인하려면 터미널을 열고 다음을 입력하십시오.

```bash
curl --version
```

응답으로 버전 번호를 받으면 cURL이 이미 설치된 것입니다. 그렇지 않은 경우 시스템의 패키지 관리자를 사용하여 설치할 수 있습니다. 예를 들어 Ubuntu에서 다음을 실행할 수 있습니다.

```bash
sudo apt-get install curl
```

다른 운영 체제의 경우 설치 지침은 cURL 설명서를 참조하십시오.

## 기본 사용법

cURL이 설치되면 이를 사용하여 HTTP와 상호 작용할 수 있습니다. 간단한 예부터 시작하겠습니다.

```bash
curl https://www.example.com
```

이 명령은 https://www.example.com에 HTTP GET 요청을 보내고 터미널에 응답을 표시합니다.

기본적으로 cURL은 GET 요청을 보내지만 `-X` 플래그를 사용하여 다른 HTTP 메서드를 지정할 수 있습니다. 예를 들어 POST 요청을 보내려면 다음을 사용합니다.

```bash
curl -X POST https://www.example.com
```

## 헤더 작업

HTTP 헤더는 요청 또는 응답에 대한 추가 정보를 제공합니다. cURL을 사용하여 `-H` 플래그를 사용하여 요청에 헤더를 추가할 수 있습니다.

```bash
curl -H "Authorization: Bearer <token>" https://api.example.com
```

이 명령은 전달자 토큰을 사용하여 요청에 `Authorization` 헤더를 추가합니다.

`-i` 플래그를 사용하여 응답의 헤더를 볼 수도 있습니다.

```bash
curl -i https://www.example.com
```

이 명령은 응답 본문 외에 응답 헤더를 표시합니다.

## 데이터 처리

cURL을 사용하면 다양한 방법을 사용하여 요청과 함께 데이터를 보낼 수 있습니다.

### URL 인코딩 데이터

URL 인코딩 형식으로 데이터를 보내려면 `-d` 플래그를 사용하십시오.

```bash
curl -d "name=John&age=30" https://api.example.com
```

이 명령은 URL 인코딩 데이터 `name=John&age=30`과 함께 POST 요청을 보냅니다.

### JSON 데이터

JSON 형식으로 데이터를 보내려면 콘텐츠 유형 헤더와 함께 `-d` 플래그를 사용하십시오.

```bash
curl -H "Content-Type: application/json" -d '{"name":"John","age":30}' https://api.example.com
```

이 명령은 JSON 데이터 `{"name":"John","age":30}`과 함께 POST 요청을 보냅니다.

### 양식 데이터

양식 형식으로 데이터를 보내려면 `-F` 플래그를 사용하십시오.

```bash
curl -F "name=John" -F "age=30" https://api.example.com
```

이 명령은 데이터 `name=John&age=30` 형식의 POST 요청을 보냅니다.

## 응답 처리

cURL은 응답을 처리하기 위한 몇 가지 옵션을 제공합니다.

### 응답 저장

파일에 대한 응답을 저장하려면 `-o` 플래그를 사용하십시오.

```bash
curl -o response.txt https://www.example.com
```

이 명령은 응답을 `response.txt`라는 파일에 저장합니다.

### 다음 리디렉션

기본적으로 cURL은 리디렉션을 따르지 않습니다. 다음 경로 재지정을 활성화하려면 `-L` 플래그를 사용하십시오.

```bash
curl -L https://www.example.com
```

이 명령은 모든 리디렉션을 따르고 최종 응답을 표시합니다.

## 결론

cURL은 HTTP 작업을 위한 강력한 도구로 다양한 기능과 옵션을 제공합니다. 이 문서에서는 요청 전송, 헤더 및 데이터 작업, 응답 처리를 포함하여 cURL 사용의 기본 사항 중 일부를 다뤘습니다. 이러한 기술을 통해 cURL을 사용하여 광범위한 HTTP 관련 작업을 처리할 수 있어야 합니다.

## 외부 리소스

- [cURL 문서](https://curl.se/docs/)
- [HTTP 헤더 - MDN 웹 문서](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- [HTTP 방법 - MDN 웹 문서](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)