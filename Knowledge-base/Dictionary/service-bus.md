---
title: Service Bus
description: 
published: true
date: 2023-03-04T14:32:43.030Z
tags: 
editor: markdown
dateCreated: 2023-03-04T14:32:35.811Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Service Bus***English** document is available*](/en/Knowledge-base/Dictionary/service-bus)
{.links-list}


# 서비스 버스

## 개요

서비스 버스는 서로 다른 애플리케이션, 서비스 및 시스템 간의 통신을 가능하게 하는 메시징 인프라입니다. 메시지를 비동기식으로 교환하는 신뢰할 수 있고 확장 가능한 방법을 제공하여 발신자와 수신자를 서로 분리합니다. 서비스 버스는 애플리케이션의 서로 다른 구성 요소가 서로 통신해야 하는 분산 컴퓨팅 환경에서 사용됩니다.

## 설명

서비스 버스는 서로 다른 애플리케이션 간의 통신을 용이하게 하는 미들웨어입니다. 발신자로부터 메시지를 수신하고 적절한 수신자에게 라우팅하는 메시지 브로커 역할을 합니다. 발신자와 수신자는 서로 다른 응용 프로그램이거나 동일한 응용 프로그램의 다른 구성 요소일 수 있습니다.

Service Bus는 메시지를 비동기식으로 교환하는 방법을 제공합니다. 즉, 보낸 사람과 받는 사람이 동시에 사용 가능할 필요가 없습니다. 발신자는 서비스 버스에 메시지를 보내고 응답을 기다리지 않고 작업을 계속할 수 있습니다. 서비스 버스는 메시지를 저장했다가 사용 가능해지면 수신자에게 전달합니다. 이렇게 하면 발신자와 수신자가 서로 분리되어 시스템이 더 유연하고 확장 가능해집니다.

Service Bus는 메시지 큐잉, 메시지 라우팅 및 메시지 변환과 같은 기능도 제공합니다. 메시지 큐잉을 사용하면 수신자가 메시지를 처리할 때까지 메시지를 큐에 저장할 수 있습니다. 메시지 라우팅을 사용하면 콘텐츠 또는 기타 기준에 따라 적절한 수신자에게 메시지를 보낼 수 있습니다. 메시지 변환을 통해 메시지를 한 형식에서 다른 형식으로 변환할 수 있으므로 서로 다른 메시지 형식을 사용하는 시스템 간의 통신이 가능합니다.

서비스 버스는 JMS, AMQP 또는 MQTT와 같은 다양한 기술을 사용하여 구현할 수 있습니다. Microsoft Azure Service Bus 및 Amazon Web Services(AWS) SQS(Simple Queue Service)는 서비스 버스 구현의 인기 있는 예입니다.

## 역사

서비스 버스의 개념은 오랫동안 존재해 왔습니다. 분산 컴퓨팅 초기에는 MOM(메시지 지향 미들웨어)을 사용하여 서로 다른 애플리케이션 간의 통신을 용이하게 했습니다. MOM은 메시지 대기열, 메시지 라우팅 및 메시지 변환과 같은 기능을 제공했습니다.

웹 서비스 및 서비스 지향 아키텍처(SOA)의 출현과 함께 서비스 버스의 개념이 발전했습니다. SOA는 네트워크를 통해 액세스할 수 있는 독립적인 모듈식 구성 요소인 서비스라는 개념을 도입했습니다. 서비스 버스는 서로 다른 서비스 간의 통신을 가능하게 하는 SOA의 필수 구성 요소가 되었습니다.

## 특징

서비스 버스는 다음 기능을 제공합니다.

- 비동기 메시징: 발신자와 수신자를 동시에 사용할 필요 없이 통신할 수 있습니다.
- 메시지 큐잉: 메시지가 수신자에 의해 처리될 때까지 큐에 메시지를 저장합니다.
- 메시지 라우팅: 콘텐츠 또는 기타 기준에 따라 적절한 수신자에게 메시지를 보냅니다.
- 메시지 변환: 메시지를 한 형식에서 다른 형식으로 변환하여 서로 다른 메시지 형식을 사용하는 시스템 간의 통신을 가능하게 합니다.
- 확장성: 시스템에서 많은 수의 메시지와 사용자를 처리할 수 있습니다.
- 신뢰성: 발신자 또는 수신자가 일시적으로 사용할 수 없는 경우에도 메시지가 수신자에게 전달되도록 합니다.
- 보안 : 안전한 통신을 위해 인증, 권한 부여, 암호화 등의 기능을 제공합니다.

## 예

주문이 배송될 때 고객에게 알려야 하는 전자 상거래 웹 사이트가 있다고 가정합니다. 서비스 버스를 사용하여 이 기능을 구현할 수 있습니다. 고객이 주문하면 웹 사이트는 주문 세부 정보와 고객의 이메일 주소가 포함된 메시지를 서비스 버스에 보냅니다. 서비스 버스는 메시지를 대기열에 저장하고 주문이 배송되면 고객에게 알림 이메일을 보냅니다. 이메일 서비스는 대기열에서 메시지를 검색하고 이메일을 고객에게 보냅니다.

## 장점과 단점

장점:

- 발신자와 수신자를 분리하여 시스템을 보다 유연하고 확장 가능하게 만듭니다.
- 비동기 메시징을 활성화하여 성능과 응답성을 향상시킵니다.
- 서로 다른 응용 프로그램 간의 통신을 단순화하는 메시지 큐잉, 메시지 라우팅 및 메시지 변환과 같은 기능을 제공합니다.
- 발신인 또는 수신인이 일시적으로 사용할 수 없는 경우에도 메시지가 전달되도록 하여 신뢰성을 향상시킵니다.
- 인증, 권한 부여, 암호화 등의 보안 기능을 제공합니다.

단점:

- 서비스 버스는 시스템에 복잡성을 추가하여 추가 인프라 및 유지 관리가 필요합니다.
- 서비스 버스는 성능에 영향을 미칠 수 있는 대기 시간 및 오버헤드를 도입할 수 있습니다.
- 서비스 버스는 전체 시스템에 영향을 미칠 수 있는 단일 장애 지점이 될 수 있습니다.

## 논란

서비스 버스를 둘러싼 논란은 없습니다.

## 관련 기술

서비스 버스는 다음 기술과 관련이 있습니다.

- 메시지 지향 미들웨어(MOM): 서비스 버스와 유사한 기능을 제공하여 서로 다른 애플리케이션 간의 통신을 가능하게 합니다.
- ESB(엔터프라이즈 서비스 버스): 프로토콜 변환, 서비스 오케스트레이션 및 서비스 조정과 같은 추가 기능을 제공합니다.
- 웹 서비스: SOAP 및 REST와 같은 표준화된 프로토콜을 사용하여 서로 다른 애플리케이션 간의 통신을 가능하게 합니다.

## 여담

서비스 버스는 최신 분산 컴퓨팅 시스템의 필수 구성 요소입니다. 서로 다른 애플리케이션, 서비스 및 시스템 간의 통신을 가능하게 하여 시스템을 보다 유연하고 확장 가능하게 만듭니다. Service Bus는 메시지 대기열, 메시지 라우팅 및 메시지 변환과 같은 기능을 제공하여 서로 다른 애플리케이션 간의 통신을 단순화합니다. 서비스 버스는 전자 상거래, 금융, 의료 및 운송과 같은 다양한 산업에서 사용됩니다.

## 기타

서비스 버스는 최신 분산 컴퓨팅 시스템의 중요한 구성 요소입니다. 서로 다른 애플리케이션, 서비스 및 시스템 간의 통신을 가능하게 하여 시스템을 보다 유연하고 확장 가능하게 만듭니다. Service Bus는 메시지 대기열, 메시지 라우팅 및 메시지 변환과 같은 기능을 제공하여 서로 다른 애플리케이션 간의 통신을 단순화합니다. 서비스 버스는 전자 상거래, 금융, 의료 및 운송과 같은 다양한 산업에서 사용됩니다.