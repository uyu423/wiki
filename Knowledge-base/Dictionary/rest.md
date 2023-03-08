---
title: REST
description: 
published: true
date: 2023-02-17T18:09:16.928Z
tags: 
editor: markdown
dateCreated: 2023-01-30T17:17:31.226Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [REST***English** version of this document is available*](/en/Knowledge-base/Dictionary/rest)
{.links-list}


# 개요

REST(Representational State Transfer)는 웹 서비스와 같은 분산 시스템을 설계하기 위한 아키텍처 스타일입니다. 클라이언트-서버 아키텍처 및 상태 비저장 통신의 원칙을 기반으로 합니다.

# 역사

REST는 2000년 Roy Fielding이 박사 학위 논문의 일부로 처음 제안했습니다. 그는 RPC 및 SOAP와 같은 기존 아키텍처가 지나치게 복잡하고 웹이 작동하는 방식을 반영하지 않는다고 주장했습니다.

# 설명

REST는 클라이언트와 서버가 동일한 인터페이스를 사용하여 통신할 수 있다는 아이디어를 기반으로 합니다. 이 인터페이스는 웹에서 컴퓨터 간에 데이터를 교환하는 데 사용되는 프로토콜인 **HTTP**의 원칙을 기반으로 합니다. **무상태**로 설계되어 클라이언트의 각 요청이 독립적인 트랜잭션으로 처리되고 서버는 요청 간에 클라이언트에 대한 정보를 유지하지 않습니다.

REST 아키텍처의 주요 구성 요소는 **리소스**, **표현** 및 **작업**입니다. 리소스는 사용자나 책과 같은 시스템의 기본 요소입니다. 표현은 HTML 문서 또는 JSON 개체와 같이 클라이언트와 서버 간에 교환되는 데이터입니다. 작업은 리소스 생성, 업데이트 또는 삭제와 같이 리소스에서 수행할 수 있는 작업입니다.

REST는 **하이퍼미디어** 개념에 의존합니다. 이것은 서버가 응답에서 다른 관련 리소스에 대한 링크를 제공할 수 있다는 생각입니다. 예를 들어 책 요청에 대한 응답에는 저자의 프로필 페이지에 대한 링크가 포함될 수 있습니다. 이를 통해 클라이언트는 추가 요청 없이 추가 정보에 액세스할 수 있습니다.

# 여담

REST는 또한 **캐싱**을 사용할 수 있게 하여 클라이언트와 서버 간에 전송해야 하는 데이터의 양을 줄여 시스템 성능을 향상시킬 수 있습니다.

REST는 또한 **버전 관리** 개념을 지원하여 기존 클라이언트를 손상시키지 않고 새 버전의 API를 릴리스할 수 있습니다. 이는 URL에 버전 정보를 포함하고 동시에 여러 버전의 API를 지원함으로써 달성됩니다.

# 관련된 링크들
- [RESTful 웹 서비스*O'Reilly Media*](https://www.oreilly.com/library/view/restful-web-services/9780596155860/)
- [REST API 튜토리얼*REST API 튜토리얼*](https://restapitutorial.com/)
- [REST*Google 개발자 소개*](https://developers.google.com/drive/api/v3/about-rest)
{.links-list}