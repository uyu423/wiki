---
title: Event-Driven Architecture
description: 
published: true
date: 2023-03-02T08:22:35.635Z
tags: 
editor: markdown
dateCreated: 2023-03-02T08:22:28.531Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Event-Driven Architecture***English** document is available*](/en/Knowledge-base/Dictionary/event-driven-architecture)
{.links-list}
# 이벤트 기반 아키텍처

## 개요

EDA(Event-Driven Architecture)는 이벤트를 사용하여 시스템의 서로 다른 구성 요소 간의 통신을 가능하게 하는 소프트웨어 아키텍처 패턴입니다. EDA에서 이벤트는 시스템 상태의 변경 또는 하나 이상의 구성 요소에서 응답을 트리거할 수 있는 중요한 사건으로 정의됩니다. EDA는 확장 가능하고 유연한 방식으로 복잡한 시스템을 처리할 수 있는 기능으로 인해 최신 소프트웨어 개발에서 점점 인기를 얻고 있습니다.

## 설명

EDA는 시스템 구성 요소가 서로 비동기식으로 통신할 수 있도록 하는 분산 아키텍처입니다. EDA에서 이벤트는 구성 요소 간의 주요 통신 수단입니다. 이벤트는 시스템의 모든 구성 요소에서 생성할 수 있으며 이벤트를 구독한 다른 구성 요소에서 사용할 수 있습니다.

EDA는 세 가지 구성 요소로 구성됩니다.

1. **이벤트 생산자:** 이벤트를 생성하는 구성 요소입니다.
2. **이벤트 소비자:** 이벤트를 처리하는 구성 요소입니다.
3. **이벤트 브로커:** 생산자와 소비자 사이에서 중재자 역할을 하는 구성 요소입니다. 생산자로부터 이벤트를 받아 소비자에게 전달합니다.

Event Broker는 메시지 큐 또는 게시-구독 시스템을 사용하여 구현할 수 있습니다. 메시지 큐에서 이벤트는 큐에 저장되고 FIFO(First-In-First-Out) 순서로 소비자에게 전달됩니다. 게시-구독 시스템에서 이벤트는 이벤트를 구독한 모든 소비자에게 브로드캐스트됩니다.

EDA는 서비스 지향 아키텍처(SOA) 또는 모놀리식 아키텍처와 같은 기존 아키텍처에 비해 몇 가지 장점이 있습니다. EDA는 구성 요소 간의 느슨한 결합을 가능하게 합니다. 즉, 시스템의 나머지 부분에 영향을 주지 않고 구성 요소를 독립적으로 개발하고 배포할 수 있습니다. EDA는 구성 요소가 이벤트를 비동기식으로 처리할 수 있도록 하여 시스템의 처리량을 향상시키므로 확장성이 매우 뛰어납니다.

## 역사

EDA는 수십 년 동안 사용되어 왔지만 2000년대 초반 이벤트 기반 미들웨어의 부상과 함께 인기를 얻었습니다. IBM의 WebSphere MQ와 Microsoft의 MSMQ(Message Queuing)는 EDA의 초기 구현 중 일부였습니다. 클라우드 컴퓨팅 및 마이크로서비스 아키텍처의 출현과 함께 EDA는 분산 환경에서 복잡한 시스템을 처리할 수 있는 기능으로 인해 훨씬 더 대중화되었습니다.

## 특징

EDA에는 최신 소프트웨어 개발에 널리 사용되는 몇 가지 주요 기능이 있습니다.

1. **비동기식 통신:** EDA를 사용하면 구성 요소가 비동기식으로 통신할 수 있으므로 시스템의 처리량과 확장성이 향상됩니다.
2. **느슨한 결합:** EDA는 구성 요소 간의 느슨한 결합을 가능하게 합니다. 즉, 시스템의 나머지 부분에 영향을 주지 않고 구성 요소를 독립적으로 개발하고 배포할 수 있습니다.
3. **내결함성:** EDA는 구성 요소가 이벤트를 비동기적으로 처리할 수 있도록 허용하여 내결함성을 지원합니다. 구성 요소가 이벤트를 처리하지 못하는 경우 이벤트를 다시 시도하거나 다른 구성 요소로 전달할 수 있습니다.
4. **이벤트 기반 처리:** EDA는 이벤트 기반 처리를 지원합니다. 즉, 구성 요소는 관련 이벤트만 처리합니다. 이렇게 하면 시스템의 효율성이 향상되고 처리 오버헤드가 줄어듭니다.

## 예

EDA를 사용하는 전자 상거래 시스템의 예를 살펴보겠습니다. 이 시스템은 제품 카탈로그, 장바구니 및 지불 게이트웨이를 포함한 여러 구성 요소로 구성됩니다.

고객이 장바구니에 제품을 추가하면 장바구니 구성 요소가 제품 세부 정보가 포함된 이벤트를 생성합니다. 이벤트는 제품 인벤토리를 업데이트하는 제품 카탈로그 구성 요소로 전달됩니다. 이벤트는 총 금액을 계산하고 결제 프로세스를 시작하는 결제 게이트웨이 구성 요소에도 전달됩니다.

이 예에서 장바구니 구성 요소는 이벤트 생산자이고 제품 카탈로그 및 지불 게이트웨이 구성 요소는 이벤트 소비자입니다. 이벤트 브로커는 적절한 소비자에게 이벤트를 전달할 책임이 있습니다.

## 장점과 단점

다른 소프트웨어 아키텍처 패턴과 마찬가지로 EDA에도 장단점이 있습니다.

### 장점

1. **확장성:** EDA를 사용하면 구성 요소가 이벤트를 비동기적으로 처리할 수 있으므로 시스템의 확장성이 향상됩니다.
2. **유연성:** EDA는 구성 요소 간의 느슨한 결합을 가능하게 합니다. 즉, 시스템의 나머지 부분에 영향을 주지 않고 구성 요소를 독립적으로 개발하고 배포할 수 있습니다.
3. **내결함성:** EDA는 구성 요소가 이벤트를 비동기적으로 처리할 수 있도록 허용하여 내결함성을 지원합니다. 구성 요소가 이벤트를 처리하지 못하는 경우 이벤트를 다시 시도하거나 다른 구성 요소로 전달할 수 있습니다.

### 단점

1. **복잡성:** EDA는 분산 특성으로 인해 구현 및 유지 관리가 복잡할 수 있습니다.
2. **대기 시간:** EDA는 구성 요소 간의 비동기 통신으로 인해 시스템에 대기 시간을 도입할 수 있습니다.
3. **디버깅:** EDA 시스템 디버깅은 아키텍처의 분산 특성으로 인해 어려울 수 있습니다.

## 논란

특정 시나리오에서 EDA 사용에 대해 약간의 논란이 있습니다. 일부에서는 EDA가 단순한 시스템에 불필요한 복잡성과 대기 시간을 도입할 수 있다고 주장합니다. 다른 이들은 EDA가 실시간 처리가 필요한 시스템에 적합하지 않다고 주장합니다.

## 관련 기술

EDA는 다음을 포함하여 다른 소프트웨어 아키텍처 패턴과 밀접한 관련이 있습니다.

1. **마이크로서비스 아키텍처:** 마이크로서비스 아키텍처는 작고 독립적인 서비스의 개발 및 배포를 가능하게 하는 분산 아키텍처 패턴입니다.
2. **서비스 지향 아키텍처(SOA):** SOA는 표준화된 프로토콜을 사용하여 서로 통신하는 서비스의 개발 및 배포를 가능하게 하는 분산 아키텍처 패턴입니다.
3. **이벤트 소싱:** 이벤트 소싱은 이벤트 기반 아키텍처를 사용하여 시스템 상태를 일련의 이벤트로 저장하는 기술입니다.

## 여담

EDA는 확장 가능하고 유연한 방식으로 복잡한 시스템을 처리할 수 있는 기능으로 인해 최신 소프트웨어 개발에서 점점 인기를 얻고 있습니다. EDA는 구성 요소 간의 느슨한 결합을 가능하게 합니다. 즉, 시스템의 나머지 부분에 영향을 주지 않고 구성 요소를 독립적으로 개발하고 배포할 수 있습니다. EDA는 구성 요소가 이벤트를 비동기식으로 처리할 수 있도록 하여 시스템의 처리량을 향상시키므로 확장성이 매우 뛰어납니다.

그러나 EDA는 분산 특성으로 인해 구현 및 유지 관리가 복잡할 수 있습니다. EDA 시스템 디버깅은 아키텍처의 분산 특성으로 인해 어려울 수 있습니다. EDA는 구성 요소 간의 비동기 통신으로 인해 시스템에 대기 시간을 도입할 수도 있습니다.

단점에도 불구하고 EDA는 확장 가능하고 유연한 방식으로 복잡한 시스템을 개발할 수 있는 강력한 아키텍처 패턴입니다.