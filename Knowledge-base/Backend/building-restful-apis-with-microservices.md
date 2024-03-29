---
title: 마이크로서비스로 RESTful API 구축
description: 
published: true
date: 2023-02-01T00:43:26.671Z
tags: 
editor: markdown
dateCreated: 2023-02-01T00:43:25.091Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Building RESTful APIs with Microservices***English** version of this document is available*](/en/Knowledge-base/Backend/building-restful-apis-with-microservices)
{.links-list}



# 마이크로서비스로 RESTful API 구축

마이크로서비스는 RESTful API 구축에 널리 사용되는 접근 방식입니다. 독립적으로 배포하고 확장할 수 있는 작고 독립된 단위입니다. 따라서 모듈식이며 확장 가능한 API를 구축하는 데 이상적입니다.

이 기사에서는 마이크로 서비스로 RESTful API를 구축하는 방법을 살펴보겠습니다. 마이크로서비스 사용의 이점부터 살펴보겠습니다. 그런 다음 마이크로서비스를 설계하고 구축하는 방법을 살펴보겠습니다. 또한 마이크로서비스를 구축할 때 직면할 수 있는 몇 가지 문제에 대해서도 살펴보겠습니다.

## 마이크로서비스의 이점

마이크로서비스를 사용하면 많은 이점이 있습니다. 여기에는 다음이 포함됩니다.

- 모듈성: 마이크로서비스는 작고 독립적인 단위입니다. 이렇게 하면 모놀리식 API를 더 작고 관리하기 쉬운 조각으로 쉽게 나눌 수 있습니다.

- 확장성: 마이크로서비스는 독립적으로 확장될 수 있습니다. 이를 통해 API의 다른 부분을 독립적으로 확장할 수 있습니다.

- 유연성: 마이크로서비스는 모든 프로그래밍 언어로 작성할 수 있습니다. 이를 통해 각 마이크로 서비스에 적합한 언어를 선택할 수 있습니다.

- 탄력성: 마이크로서비스는 여러 서버에 배포할 수 있습니다. 이렇게 하면 API가 오류에 더 탄력적으로 대처할 수 있습니다.

- 민첩성: 마이크로서비스를 독립적으로 배포할 수 있습니다. 이렇게 하면 API가 더 민첩해지고 새로운 기능을 빠르게 배포할 수 있습니다.

## 마이크로서비스 설계

마이크로서비스를 설계할 때 염두에 두어야 할 몇 가지 사항이 있습니다. 첫째, 각 마이크로 서비스에는 단일 책임이 있어야 합니다. 즉, 각 마이크로 서비스에는 하나의 작업만 있어야 합니다. 예를 들어 인증 처리용 마이크로서비스 하나와 사용자 데이터 처리용 마이크로서비스가 있을 수 있습니다.

둘째, 마이크로서비스는 느슨하게 결합되어야 합니다. 즉, 각 마이크로서비스는 서로 독립적이어야 합니다. 이를 통해 다른 마이크로서비스에 영향을 주지 않고 하나의 마이크로서비스를 쉽게 변경하거나 교체할 수 있습니다.

셋째, 마이크로서비스는 상태 비저장이어야 합니다. 이는 각 요청이 서로 독립적이어야 함을 의미합니다. 이렇게 하면 API를 쉽게 확장할 수 있습니다.

넷째, API 게이트웨이를 사용해야 합니다. 이것은 모든 마이크로 서비스에 대한 단일 진입점입니다. API 게이트웨이는 요청을 적절한 마이크로서비스로 라우팅합니다. 이렇게 하면 API가 더 안전하고 확장 가능해집니다.

마지막으로 분산 추적 시스템을 사용해야 합니다. 이를 통해 마이크로서비스를 통과하는 요청을 추적할 수 있습니다. 이는 API 디버깅 및 모니터링에 유용합니다.

## 마이크로서비스 구축

마이크로서비스를 구축하는 방법에는 여러 가지가 있습니다. 이 섹션에서는 널리 사용되는 두 가지 접근 방식을 살펴보겠습니다.

### 모놀리식 접근 방식

모놀리식 접근 방식은 마이크로서비스를 구축하는 전통적인 방식입니다. 이 접근 방식에서는 모든 마이크로 서비스가 단일 프로젝트에 구축됩니다. 그런 다음 이 프로젝트는 서버에 배포됩니다.

이 접근 방식에는 몇 가지 이점이 있습니다. 첫째, 시작하기 쉽습니다. 둘째, 모든 마이크로서비스가 함께 배포되므로 서로 쉽게 통신할 수 있습니다.

그러나 이 방법에는 몇 가지 단점이 있습니다. 첫째, 확장이 어렵다. 둘째, 다른 마이크로서비스에 영향을 미치지 않고 하나의 마이크로서비스를 변경하거나 교체하는 것은 어렵습니다.

### 마이크로서비스 접근 방식

마이크로서비스 접근 방식은 마이크로서비스를 구축하는 새로운 방법입니다. 이 접근 방식에서 각 마이크로 서비스는 자체 프로젝트에 구축됩니다. 그런 다음 이 프로젝트는 서버에 배포됩니다.

이 접근 방식에는 몇 가지 이점이 있습니다. 첫째, 확장이 쉽다. 둘째, 다른 마이크로서비스에 영향을 주지 않고 하나의 마이크로서비스를 쉽게 변경하거나 교체할 수 있습니다.

그러나 이 방법에는 몇 가지 단점이 있습니다. 첫째, 시작하기가 더 어렵습니다. 둘째, 모든 마이크로서비스는 독립적으로 배포되므로 서로 쉽게 통신할 수 없습니다.

## 마이크로서비스의 과제

마이크로서비스를 구축할 때 직면할 수 있는 몇 가지 문제가 있습니다.

### 의사소통

하나의 도전은 의사 소통입니다. 마이크로서비스는 독립적으로 배포되므로 서로 쉽게 통신할 수 없습니다. 이로 인해 마이크로 서비스 간에 데이터를 공유하기 어려울 수 있습니다.

이 문제를 극복하기 위해 메시지 대기열을 사용할 수 있습니다. 메시지 큐는 마이크로서비스가 서로 비동기식으로 통신할 수 있게 해주는 시스템입니다. 이는 마이크로서비스가 응답을 기다리지 않고 서로에게 메시지를 보낼 수 있음을 의미합니다.

### 조정

또 다른 과제는 조정입니다. 마이크로서비스는 독립적으로 배포되므로 서로 조정해야 합니다. 각 마이크로 서비스에는 고유한 코드베이스와 배포 프로세스가 있으므로 이는 어려울 수 있습니다.

이 문제를 극복하기 위해 분산 추적 시스템을 사용할 수 있습니다. 분산 추적 시스템을 사용하면 마이크로서비스를 통과하는 요청을 추적할 수 있습니다. 이는 API 디버깅 및 모니터링에 유용합니다.

### 배포

마지막으로 배포가 어려울 수 있습니다. 마이크로서비스는 독립적으로 배포되므로 각 마이크로서비스를 별도로 배포해야 합니다. 이 작업은 시간이 오래 걸리고 오류가 발생하기 쉽습니다.

이 문제를 극복하기 위해 연속 배포 시스템을 사용할 수 있습니다. 지속적 배포 시스템은 마이크로서비스 배포 프로세스를 자동화합니다. 이를 통해 마이크로서비스를 빠르고 안정적으로 배포하는 것이 더 쉬워집니다.