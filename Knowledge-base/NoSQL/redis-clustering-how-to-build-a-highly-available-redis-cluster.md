---
title: Redis 클러스터링: 고가용성 Redis 클러스터 구축 방법
description: 
published: true
date: 2023-03-03T11:32:41.918Z
tags: 
editor: markdown
dateCreated: 2023-03-03T11:32:41.918Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Redis Clustering: How to Build a Highly Available Redis Cluster***English** document is available*](/en/Knowledge-base/NoSQL/redis-clustering-how-to-build-a-highly-available-redis-cluster)
{.links-list}


Redis 클러스터링: 고가용성 Redis 클러스터 구축 방법

Redis는 캐싱, 세션 관리 및 게시/구독 메시징에 사용되는 인기 있는 오픈 소스 메모리 내 데이터 저장소입니다. Redis는 고성능, 확장성 및 가용성을 제공하도록 설계되어 최신 웹 애플리케이션 구축에 이상적인 선택입니다. 그러나 Redis에 저장되는 데이터의 양이 증가함에 따라 고가용성과 성능을 보장하기 위해 여러 노드에 걸쳐 Redis를 수평으로 확장해야 합니다. Redis 클러스터링이 필요한 곳입니다.

Redis 클러스터링은 가용성이 높고 내결함성이 뛰어난 Redis 클러스터를 제공하기 위해 함께 작동하는 여러 Redis 노드를 설정하는 프로세스입니다. 이 기사에서는 다음 항목을 포함하여 고가용성 Redis 클러스터를 구축하는 데 필요한 단계를 살펴봅니다.

- Redis 클러스터링 이해
- Redis 클러스터 설정
- Redis 클러스터에서 노드 추가 및 제거
- Redis 클러스터 모니터링
- Redis 클러스터 문제 해결

## Redis 클러스터링 이해

Redis 클러스터링은 여러 Redis 노드가 클러스터라고 하는 단일 논리 단위로 함께 작동할 수 있도록 하는 분산 시스템입니다. Redis 클러스터는 하나 이상의 마스터 노드와 하나 이상의 복제본 노드로 구성됩니다. 마스터 노드는 Redis 클러스터에 대한 읽기 및 쓰기 요청 처리를 담당하고 복제본 노드는 마스터 노드의 데이터 복제를 담당합니다.

Redis 클러스터링은 샤딩이라는 프로세스를 사용하여 Redis 클러스터 전체에 데이터를 분산합니다. 샤딩은 데이터를 여러 샤드로 분할한 다음 마스터 및 복제본 노드에 분산하는 작업을 포함합니다. 각 샤드는 해당 샤드에 대한 읽기 및 쓰기 요청을 처리하는 특정 마스터 노드에 할당됩니다. 복제본 노드는 고가용성과 내결함성을 보장하기 위해 마스터 노드의 데이터를 복제하는 역할을 합니다.

## Redis 클러스터 설정

Redis 클러스터를 설정하려면 Redis 노드가 3개 이상 있어야 합니다. 요구 사항에 따라 동일한 시스템 또는 다른 시스템에서 Redis 노드를 설정할 수 있습니다. 다음은 Redis 클러스터를 설정하는 데 필요한 단계입니다.

1. 각 노드에 Redis 설치: 운영 체제의 패키지 관리자를 사용하거나 Redis 웹 사이트에서 소스 코드를 다운로드하고 컴파일하여 각 노드에 Redis를 설치할 수 있습니다.

2. 각 노드에서 Redis 구성: 각 노드에 Redis를 설치했으면 각 노드에서 Redis를 구성해야 합니다. Redis 설치 디렉터리에 있는 redis.conf 파일을 편집하여 Redis를 구성할 수 있습니다.

3. 각 노드에서 Redis 시작: 각 노드에서 Redis를 구성했으면 ```redis-server /path/to/redis.conf``` 명령을 사용하여 각 노드에서 Redis를 시작할 수 있습니다. 동일한 구성 파일을 사용하여 각 노드에서 Redis를 시작해야 합니다.

4. Redis 클러스터 생성: 각 노드에서 Redis를 시작했으면 Redis에 포함된 ```redis-trib.rb``` 스크립트를 사용하여 Redis 클러스터를 생성할 수 있습니다. ```redis-trib.rb``` 스크립트는 Redis 클러스터에서 노드를 생성, 추가 및 제거하는 데 사용됩니다.

다음 명령을 사용하여 Redis 클러스터를 생성할 수 있습니다.

```
redis-trib.rb create --replicas 1 node1:6379 node2:6379 node3:6379 node4:6379 node5:6379 node6:6379
```

위 명령에서 ```--replicas 1```은 각 마스터 노드에 하나의 복제본 노드가 있어야 함을 지정합니다. ```node1:6379``` ~ ```node6:6379```는 각 Redis 노드의 IP 주소와 포트 번호를 지정합니다.

## Redis 클러스터에서 노드 추가 및 제거

Redis 클러스터를 만든 후에는 필요에 따라 클러스터에서 노드를 추가하거나 제거할 수 있습니다. Redis 클러스터에 노드를 추가하려면 다음 단계를 따라야 합니다.

1. 새 노드에 Redis 설치 및 구성: 이전 섹션에서 설명한 대로 새 노드에 Redis를 설치하고 구성해야 합니다.

2. 새 노드를 클러스터에 가입: ```redis-trib.rb``` 스크립트를 사용하여 새 노드를 클러스터에 가입할 수 있습니다. 다음 명령을 사용하여 새 노드를 클러스터에 가입시킬 수 있습니다.

```
redis-trib.rb add-node --slave new_node:6379 existing_node:6379
```

위 명령에서 ```--slave```는 새 노드가 복제본 노드여야 함을 지정하고 ```new_node:6379``` 및 ```existing_node:6379```는 IP 주소를 지정하고 각각 새 노드와 기존 노드의 포트 번호입니다.

Redis 클러스터에서 노드를 제거하려면 다음 명령을 사용할 수 있습니다.

```
redis-trib.rb del-node node1:6379 <node-id>
```

위의 명령에서 ```node1:6379```는 Redis 클러스터에 있는 모든 노드의 IP 주소와 포트 번호를 지정하고 ```<node-id>```는 원하는 노드의 ID를 지정합니다. 제거하다. Redis 클러스터의 모든 노드에서 다음 명령을 실행하여 노드의 ID를 가져올 수 있습니다.

```
redis-cli cluster nodes
```

## Redis 클러스터 모니터링

Redis 클러스터를 설정한 후에는 클러스터가 원활하게 실행되고 있는지 모니터링하는 것이 중요합니다. Redis는 다음을 포함하여 Redis 클러스터를 모니터링하는 데 사용할 수 있는 여러 도구와 명령을 제공합니다.

- ```redis-cli info```: 이 명령은 메모리 사용량, CPU 사용량 및 네트워크 트래픽을 포함하여 Redis 클러스터에 대한 정보를 제공합니다.

- ```redis-cli cluster info```: 이 명령은 마스터 및 복제본 노드 수, 클러스터에 저장된 키 수, 노드 간 키 배포를 포함하여 Redis 클러스터에 대한 정보를 제공합니다.

- ```redis-cli cluster nodes```: 이 명령은 클러스터에 있는 각 노드의 IP 주소, 포트 번호 및 ID를 포함하여 Redis 클러스터에 대한 정보를 제공합니다.

- Redis Sentinel: Redis Sentinel은 Redis 클러스터를 모니터링하고 현재 마스터 노드에 장애가 발생할 경우 자동으로 새 마스터 노드로 장애 조치하는 데 사용할 수 있는 Companion 서비스입니다. Sentinel을 사용하여 복제본 노드의 상태를 모니터링하고 데이터를 올바르게 복제하고 있는지 확인할 수도 있습니다.

## Redis 클러스터 문제 해결

Redis 클러스터에 문제가 발생하면 문제를 해결하기 위해 취할 수 있는 몇 가지 단계가 있습니다. Redis 클러스터링과 관련된 몇 가지 일반적인 문제는 다음과 같습니다.

- 노드 실패: Redis 노드가 실패하면 ```redis-trib.rb``` 스크립트를 사용하여 실패한 노드를 클러스터에서 제거하고 새 노드로 교체해야 합니다.

- 네트워크 문제: Redis 노드 간에 네트워크 문제가 있는 경우 네트워크 구성을 조사하고 Redis 노드가 서로 통신할 수 있는지 확인해야 합니다.

- 데이터 일관성 문제: 마스터 노드와 레플리카 노드 간에 데이터 일관성 문제가 있는 경우 네트워크 구성을 조사하고 레플리카 노드가 데이터를 올바르게 복제하고 있는지 확인해야 합니다.

## 결론

Redis 클러스터링은 고가용성 및 내결함성 Redis 클러스터를 구축하기 위한 필수 도구입니다. Redis 클러스터를 설정하고 이 문서에 설명된 모범 사례를 따르면 Redis 클러스터가 원활하게 실행되고 최신 웹 애플리케이션의 요구 사항을 처리할 수 있습니다.

## 외부 리소스

- [레디스 문서](https://redis.io/documentation)
- [레디스 클러스터 튜토리얼](https://redis.io/topics/cluster-tutorial)
- [Scaling a Redis Cluster with Sentinel](https://www.digitalocean.com/community/tutorials/how-to-configure-a-redis-cluster-on-ubuntu-16-04# step-3-%E2 %80%94-scaling-a-redis-cluster-with-sentinel)