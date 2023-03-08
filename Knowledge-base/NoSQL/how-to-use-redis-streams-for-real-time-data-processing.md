---
title: 실시간 데이터 처리를 위해 Redis Streams를 사용하는 방법
description: 
published: true
date: 2023-03-05T21:32:35.328Z
tags: 
editor: markdown
dateCreated: 2023-03-05T21:32:33.955Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Use Redis Streams for Real-Time Data Processing***English** document is available*](/en/Knowledge-base/NoSQL/how-to-use-redis-streams-for-real-time-data-processing)
{.links-list}



Redis Streams는 스트리밍 데이터를 위한 실시간 처리 솔루션을 제공하는 Redis의 내장 데이터 구조입니다. 이를 통해 개발자는 데이터가 도착하면 이를 처리하고 분석할 수 있는 실시간 애플리케이션을 구축할 수 있습니다. 이 기능 덕분에 Redis는 실시간 애플리케이션 구축에 널리 사용됩니다.

이 기사에서는 실시간 데이터 처리를 위해 Redis Streams를 사용하는 방법을 살펴봅니다. Redis Streams의 기본 사항, 기능 및 Redis Streams를 사용하여 실시간 애플리케이션을 구축하는 방법을 다룰 것입니다.

## Redis 스트림이 무엇인가요?

Redis Streams는 데이터 스트림 추상화를 제공하는 Redis의 데이터 유형입니다. 이를 통해 개발자는 실시간으로 데이터를 저장하고 처리할 수 있습니다. Redis Streams의 핵심 기능은 데이터가 도착하면 이를 처리하고 분석하는 기능입니다.

Redis Streams는 모든 유형의 데이터를 저장하고 처리하는 데 사용할 수 있습니다. 소셜 미디어 피드, 주가 및 센서 데이터와 같은 데이터를 실시간으로 처리하는 데 특히 유용합니다. Redis Streams는 채팅 애플리케이션, 실시간 분석 및 실시간 알림과 같은 실시간 애플리케이션을 구축하는 데 사용할 수 있습니다.

## Redis 스트림 기능

Redis Streams에는 강력한 실시간 처리 솔루션이 되는 몇 가지 기능이 있습니다.

#### 1. 정렬된 데이터

Redis Streams는 정렬된 데이터를 제공합니다. 즉, 메시지가 수신된 순서대로 저장됩니다. 이는 특정 순서로 데이터를 처리해야 하는 실시간 애플리케이션에 특히 유용합니다.

#### 2. 멱등성 처리

Redis Streams는 멱등적 처리를 지원합니다. 즉, 결과에 영향을 주지 않고 메시지를 여러 번 처리할 수 있습니다. 이는 네트워크 지연 또는 기타 문제로 인해 메시지가 두 번 이상 처리될 수 있는 상황에 유용합니다.

#### 3. 소비자 그룹

Redis Streams는 여러 소비자가 동일한 스트림에서 데이터를 읽을 수 있도록 하는 소비자 그룹을 지원합니다. 이는 부하 분산 및 장애 조치 시나리오에 특히 유용합니다.

#### 4. 배압

Redis Streams는 배압을 제공합니다. 즉, 소비자가 따라갈 수 없으면 생산자가 느려집니다. 이를 통해 시스템 과부하를 방지하고 데이터를 적시에 처리할 수 있습니다.

## Redis 스트림 명령

Redis Streams에는 스트림과 상호 작용하는 데 사용할 수 있는 몇 가지 명령이 있습니다. 다음은 가장 일반적으로 사용되는 명령 중 일부입니다.

#### 1. XADD

XADD 명령은 스트림에 데이터를 추가하는 데 사용됩니다. 스트림 이름과 하나 이상의 키-값 쌍을 인수로 사용합니다. 키는 필드 이름을 나타내고 값은 필드 값을 나타냅니다.

```redis
XADD mystream * field1 value1 field2 value2
```

* 인수는 고유한 메시지 ID를 생성하는 데 사용됩니다.

#### 2. XREAD

XREAD 명령은 스트림에서 데이터를 읽는 데 사용됩니다. 스트림 이름과 하나 이상의 ID를 인수로 사용합니다. ID는 스트림에서 읽은 마지막 메시지 ID를 나타냅니다.

```redis
XREAD COUNT 10 STREAMS mystream 0
```

이 명령은 mystream 스트림에서 마지막 10개의 메시지를 읽습니다.

#### 3. 엑스그룹

XGROUP 명령은 소비자 그룹을 만들고 관리하는 데 사용됩니다. 스트림 이름과 그룹 이름을 인수로 사용합니다.

```redis
XGROUP CREATE mystream mygroup 0
```

이 명령은 mystream 스트림에 대해 mygroup이라는 새 소비자 그룹을 생성합니다.

#### 4. XREADGROUP

XREADGROUP 명령은 소비자 그룹에서 데이터를 읽는 데 사용됩니다. 그룹 이름, 소비자 이름 및 하나 이상의 ID를 인수로 사용합니다.

```redis
XREADGROUP GROUP mygroup myconsumer COUNT 10 STREAMS mystream >
```

이 명령은 mygroup 소비자 그룹에 대한 mystream 스트림에서 마지막 10개 메시지를 읽습니다.

#### 5. XACK

XACK 명령은 소비자가 메시지를 처리했음을 확인하는 데 사용됩니다. 스트림 이름, 그룹 이름 및 하나 이상의 ID를 인수로 사용합니다.

```redis
XACK mystream mygroup 12345-0
```

이 명령은 ID가 12345-0인 메시지가 mygroup 소비자 그룹에 의해 처리되었음을 확인합니다.

## 실제 사례

Redis Streams가 실시간 데이터 처리에 어떻게 사용될 수 있는지에 대한 실제 예를 살펴보겠습니다.

수백만 명의 사용자가 있는 소셜 미디어 플랫폼이 있다고 가정합니다. 우리는 사용자가 새로운 메시지, 좋아요 또는 댓글을 받을 때 사용자에게 알리는 실시간 알림 시스템을 구축하려고 합니다.

Redis Streams를 사용하여 사용자 알림을 실시간으로 저장하고 처리할 수 있습니다. 각 사용자에게는 고유한 스트림이 있으며 알림이 도착하면 스트림에 알림이 추가됩니다.

사용자가 로그인하면 스트림에 대한 소비자 그룹을 만들 수 있습니다. 이 그룹은 사용자의 스트림에서 알림을 읽고 실시간으로 사용자에게 보냅니다.

소비자가 알림을 처리하면 XACK 명령을 사용하여 알림이 처리되었음을 확인할 수 있습니다. 이렇게 하면 알림이 사용자에게 두 번 이상 전송되지 않습니다.

## 결론

Redis Streams는 채팅 애플리케이션, 실시간 분석 및 실시간 알림과 같은 실시간 애플리케이션을 구축하는 데 사용할 수 있는 강력한 실시간 처리 솔루션입니다. 정렬된 데이터, 멱등성 처리, 소비자 그룹 및 배압을 제공합니다. Redis Streams에는 스트림과 상호 작용하는 데 사용할 수 있는 몇 가지 명령이 있습니다.

이 기사에서는 실시간 데이터 처리를 위해 Redis Streams를 사용하는 방법을 살펴보았습니다. Redis Streams의 기본 사항, 기능 및 Redis Streams를 사용하여 실시간 애플리케이션을 구축하는 방법을 다루었습니다. Redis Streams는 실시간 애플리케이션을 구축하는 모든 개발자에게 유용한 도구입니다.

## 외부 리소스

- [Redis Streams 문서](https://redis.io/topics/streams-intro)
- [실시간 데이터 처리를 위한 Redis Streams](https://www.twilio.com/blog/redis-streams-for-real-time-data-processing)
- [Redis Streams: 상위 수준 개요](https://towardsdatascience.com/redis-streams-a-high-level-overview-2c9eef5a6fe7)