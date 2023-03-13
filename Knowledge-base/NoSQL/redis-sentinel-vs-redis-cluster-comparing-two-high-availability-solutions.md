---
title: Redis Sentinel과 Redis 클러스터: 두 가지 고가용성 솔루션 비교
description: 
published: true
date: 2023-03-13T12:33:07.398Z
tags: 
editor: markdown
dateCreated: 2023-03-13T12:33:07.398Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Redis Sentinel vs. Redis Cluster: Comparing Two High-Availability Solutions***English** document is available*](/en/Knowledge-base/NoSQL/redis-sentinel-vs-redis-cluster-comparing-two-high-availability-solutions)
{.links-list}



Redis Sentinel과 Redis 클러스터: 두 가지 고가용성 솔루션 비교

Redis용 고가용성 솔루션의 경우 Redis Sentinel과 Redis Cluster가 가장 많이 사용되는 두 가지 옵션입니다. 둘 다 내결함성과 자동 장애 조치를 제공하지만 서로 다른 사용 사례에 적합하도록 만드는 특성이 다릅니다. 이 기사에서는 아키텍처, 확장성, 내결함성 및 배포 용이성 측면에서 Redis Sentinel과 Redis Cluster를 비교합니다.

## 건축학

Redis Sentinel은 독립적인 Sentinel 프로세스 집합을 사용하여 Redis 인스턴스를 모니터링하고 필요한 경우 자동 장애 조치를 수행하는 고가용성 솔루션입니다. 각 Sentinel 프로세스는 별도의 시스템에서 실행되며 다른 Sentinel 프로세스와 통신하여 Redis 인스턴스의 상태에 대한 합의에 도달합니다. Redis 인스턴스에 장애가 발생하면 센티널은 장애 조치 프로세스를 시작하여 새 마스터를 선택하고 최신 데이터가 있는 복제본을 새 마스터로 승격합니다.

반면에 Redis Cluster는 여러 Redis 인스턴스에 걸쳐 데이터를 분할하는 분산 데이터베이스 시스템입니다. 클러스터의 각 Redis 인스턴스는 키스페이스의 하위 집합을 담당하며 인스턴스는 서로 통신하여 클라이언트 요청을 적절한 노드로 라우팅합니다. Redis 클러스터는 가십 프로토콜을 사용하여 클러스터 상태에 대한 정보를 전파하고 장애가 발생한 노드에 대해 새 마스터를 선택하여 자동 장애 조치를 수행합니다.

## 확장성

Redis Sentinel은 고가용성이 필요한 중소 규모의 Redis 배포에 적합합니다. 마스터-슬레이브 구성에서 여러 Redis 인스턴스를 관리하는 데 사용할 수 있지만 Sentinel 배포에서 관리할 수 있는 Redis 인스턴스의 최대 수는 10개로 제한됩니다. 이는 각 Sentinel 프로세스가 모든 Redis에 대한 연결을 유지해야 하기 때문입니다. 인스턴스 수가 증가하면 병목 현상이 발생할 수 있습니다.

반면 Redis Cluster는 수평적 확장성이 필요한 대규모 Redis 배포를 위해 설계되었습니다. 최대 1000개의 Redis 노드를 처리할 수 있으며 클러스터에 새 노드가 추가됨에 따라 선형 확장성을 제공합니다. 또한 Redis 클러스터는 클라이언트가 클러스터의 모든 노드에 연결하고 모든 키에서 읽기 및 쓰기 작업을 수행할 수 있도록 하여 읽기 및 쓰기 확장성을 지원합니다.

## 결함 허용

Redis Sentinel과 Redis Cluster는 모두 내결함성과 자동 장애 조치를 제공하지만 이를 달성하기 위한 접근 방식이 다릅니다.

Redis Sentinel은 쿼럼 기반 접근 방식을 사용하여 Redis 인스턴스가 실패한 시기를 결정합니다. 각 Sentinel 프로세스는 Redis 인스턴스를 모니터링하고 상태를 다른 Sentinel에 보고합니다. 대부분의 Sentinel이 Redis 인스턴스가 다운되었다는 데 동의하면 장애 조치 프로세스를 시작하여 새 마스터를 선택합니다. Redis Sentinel은 나머지 Redis 인스턴스가 쿼럼을 형성할 수 있는 한 여러 장애를 처리할 수 있습니다.

Redis 클러스터는 내결함성에 대해 다른 접근 방식을 사용합니다. 실패한 노드에 대한 새 마스터를 선출하기 위해 RAFT라는 합의 알고리즘을 사용합니다. Redis 노드가 실패하면 클러스터의 다른 노드가 실패를 감지하고 리더 선택 프로세스를 시작합니다. 가장 많은 표를 받은 노드가 새로운 마스터가 됩니다. Redis 클러스터는 나머지 노드가 다수를 형성할 수 있는 한 여러 장애 및 파티션을 처리할 수 있습니다.

## 배포 용이성

Redis Sentinel은 Redis Cluster에 비해 상대적으로 배포 및 관리가 쉽습니다. 최소한의 구성이 필요하며 몇 가지 간단한 명령을 사용하여 빠르게 설정할 수 있습니다. Redis Sentinel은 또한 대부분의 Redis 클라이언트와 호환되므로 기존 애플리케이션에 쉽게 통합할 수 있습니다.

반면 Redis Cluster는 Redis Sentinel보다 더 많은 구성 및 설정이 필요합니다. 내결함성을 제공하려면 최소 3개의 마스터 노드와 3개의 복제본 노드가 필요하며 노드는 중복성을 보장하기 위해 서로 다른 시스템에 분산되어야 합니다. 또한 Redis 클러스터에는 사용할 수 있는 Redis 명령에 대한 몇 가지 제한 사항이 있으므로 기존 애플리케이션을 변경해야 할 수 있습니다.

## 결론

Redis Sentinel과 Redis Cluster는 모두 Redis를 위한 고가용성 솔루션이지만 서로 다른 사용 사례에 적합하도록 만드는 특성이 다릅니다. Redis Sentinel은 고가용성이 필요한 중소 규모의 Redis 배포에 적합하고 Redis Cluster는 수평적 확장성이 필요한 대규모 Redis 배포에 적합하도록 설계되었습니다. 둘 다 내결함성과 자동 장애 조치를 제공하지만 이를 달성하는 방법은 서로 다릅니다. Redis Sentinel은 더 많은 구성과 설정이 필요한 Redis 클러스터에 비해 상대적으로 배포 및 관리가 쉽습니다.

## 외부 리소스
- [레디스 센티널 문서](https://redis.io/topics/sentinel)
- [레디스 클러스터 문서](https://redis.io/topics/cluster-tutorial)
- [Sentinel을 사용한 Redis 고가용성 vs. Redis 클러스터](https://scalegrid.io/blog/redis-high-availability-sentinel-vs-cluster/)