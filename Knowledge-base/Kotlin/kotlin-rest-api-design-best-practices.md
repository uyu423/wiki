---
title: Kotlin REST API 설계: 모범 사례
description: 
published: true
date: 2023-02-18T05:06:14.997Z
tags: 
editor: markdown
dateCreated: 2023-02-18T05:06:13.660Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin REST API Design: Best Practices***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-rest-api-design-best-practices)
{.links-list}


# Kotlin REST API 설계: 모범 사례

REST API를 설계하는 것은 어려운 작업이 될 수 있습니다. API를 설계하는 방법에는 여러 가지가 있으며 완벽한 방법은 없습니다. 그러나 효과적이고 사용하기 쉬운 Kotlin REST API를 설계하는 데 도움이 되는 몇 가지 모범 사례가 있습니다.

## API 설계

Kotlin REST API를 설계할 때 염두에 두어야 할 몇 가지 사항이 있습니다. 먼저 API가 반환할 데이터를 결정해야 합니다. 이 데이터는 JSON, XML 또는 기타 형식의 형식일 수 있습니다. 다음으로 API가 지원할 메서드를 결정해야 합니다. 가장 일반적인 방법은 GET, POST, PUT 및 DELETE입니다. 마지막으로 API의 URL 구조를 결정해야 합니다.

## 데이터 반환

Kotlin REST API에서 데이터를 반환할 때 적절한 데이터 형식을 사용하는 것이 중요합니다. JSON은 REST API의 가장 일반적인 데이터 형식입니다. 사람이 읽을 수 있고 파싱하기 쉽습니다. XML은 널리 사용되는 또 다른 데이터 형식이지만 구문 분석하기가 더 어려울 수 있습니다. 애플리케이션에 가장 적합한 데이터 형식을 선택하십시오.

## 지원 방법

Kotlin REST API는 GET, POST, PUT 및 DELETE와 같은 가장 일반적인 HTTP 메서드를 지원해야 합니다. GET은 서버에서 데이터를 검색하는 데 사용됩니다. POST는 서버에서 데이터를 생성하는 데 사용됩니다. PUT은 서버의 데이터를 업데이트하는 데 사용됩니다. DELETE는 서버의 데이터를 삭제하는 데 사용됩니다.

## URL 구조

Kotlin REST API에는 잘 정의된 URL 구조가 있어야 합니다. 가장 일반적인 URL 구조는 /{resource}/{id}입니다. 예를 들어 /users/1은 ID가 1인 사용자를 검색합니다. /users는 모든 사용자를 검색합니다. /users/1/friends는 ID가 1인 사용자의 모든 친구를 검색합니다.

## 외부 리소스

https://kotlinlang.org/docs/reference/http-clients.html
https://ktor.io/
https://javadoc.io/doc/com.github.kittinunf.fuel/fuel/latest/index.html