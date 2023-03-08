---
title: Redis Enterprise: 고가용성으로 클라우드에서 Redis 확장
description: 
published: true
date: 2023-03-08T09:32:41.131Z
tags: 
editor: markdown
dateCreated: 2023-03-08T09:32:41.131Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Redis Enterprise: Scaling Redis in the Cloud with High Availability***English** document is available*](/en/Knowledge-base/NoSQL/redis-enterprise-scaling-redis-in-the-cloud-with-high-availability)
{.links-list}

Redis Enterprise: 고가용성으로 클라우드에서 Redis 확장

Redis Enterprise는 고가용성, 확장성 및 성능을 제공하는 분산 인메모리 데이터베이스입니다. Redis Enterprise는 높은 처리량과 짧은 대기 시간이 필요한 중요한 애플리케이션을 지원하도록 설계되었습니다. 문자열, 해시, 목록, 세트 및 정렬된 세트를 포함한 다양한 데이터 구조를 지원합니다. Redis Enterprise는 또한 확장성이 뛰어나 개발자가 모듈을 통해 사용자 지정 기능을 추가할 수 있습니다.

Redis Enterprise는 클라우드 서비스로 제공되므로 쉽게 사용하고 확장할 수 있습니다. 이 기사에서는 Redis Enterprise를 사용하여 고가용성으로 클라우드에서 Redis를 확장하는 방법을 살펴봅니다.

## 레디스 엔터프라이즈란?

Redis Enterprise는 오픈 소스 버전에 비해 여러 가지 이점을 제공하는 Redis의 관리형 버전입니다. Redis Enterprise는 고가용성, 확장성 및 성능을 제공하도록 설계되었습니다. 또한 확장성이 뛰어나 개발자가 모듈을 통해 사용자 정의 기능을 추가할 수 있습니다.

Redis Enterprise는 Amazon Web Services(AWS), Microsoft Azure, Google Cloud Platform(GCP) 등 다양한 클라우드 플랫폼에 배포할 수 있는 클라우드 서비스로 제공됩니다. Redis Enterprise는 데이터를 사내에 보관하는 것을 선호하는 조직을 위한 온프레미스 솔루션으로도 제공됩니다.

## Redis Enterprise로 Redis 확장

Redis 확장은 메모리 내 특성으로 인해 어려울 수 있습니다. Redis와 같은 인 메모리 데이터베이스는 데이터 세트가 사용 가능한 메모리를 초과하여 커지면 메모리가 빠르게 부족해질 수 있습니다. 이것이 Redis Enterprise가 들어오는 곳입니다.

Redis Enterprise는 클라우드에서 Redis를 쉽게 확장할 수 있는 몇 가지 기능을 제공합니다. 이러한 기능에는 다음이 포함됩니다.

### 1. 샤딩

샤딩은 데이터 세트를 샤드라고 하는 더 작은 하위 집합으로 분할하는 프로세스입니다. 각 샤드를 별도의 서버에 저장할 수 있으므로 Redis Enterprise가 여러 서버에 부하를 분산할 수 있습니다. Redis Enterprise는 자동 샤딩을 지원합니다. 즉, 키의 해시를 기반으로 데이터 세트를 샤드로 자동 분할할 수 있습니다.

다음은 Redis CLI를 사용하여 Redis Enterprise에서 자동 샤딩을 활성화하는 방법의 예입니다.

```
redis-cli -h <redis-enterprise-cluster-url> -p <redis-enterprise-cluster-port> CONFIG SET hash-max-ziplist-entries 512
```

### 2. 복제

복제는 한 Redis 서버에서 다른 서버로 데이터를 복사하는 프로세스입니다. Redis Enterprise는 마스터-슬레이브 복제를 지원합니다. 즉, 하나의 Redis 서버(마스터)가 쓰기 작업을 처리하고 하나 이상의 Redis 서버(슬레이브)가 읽기 작업을 처리합니다.

다음은 Redis CLI를 사용하여 Redis Enterprise에서 복제를 활성화하는 방법의 예입니다.

```
redis-cli -h <redis-enterprise-cluster-url> -p <redis-enterprise-cluster-port> CONFIG SET slave-read-only yes
```

### 3. 자동 장애 조치

자동 장애 복구는 마스터가 실패할 경우 자동으로 슬레이브를 마스터로 승격시키는 프로세스입니다. Redis Enterprise는 자동 장애 조치를 지원합니다. 즉, 마스터가 실패할 때를 감지하고 자동으로 슬레이브를 마스터로 승격할 수 있습니다.

다음은 Redis CLI를 사용하여 Redis Enterprise에서 자동 장애 조치를 활성화하는 방법의 예입니다.

```
redis-cli -h <redis-enterprise-cluster-url> -p <redis-enterprise-cluster-port> CONFIG SET min-slaves-to-write 2
```

### 4. 탄력

탄력성은 워크로드에 따라 리소스를 동적으로 추가하거나 제거하는 기능입니다. Redis Enterprise는 탄력성을 지원합니다. 즉, 워크로드에 따라 리소스를 자동으로 추가하거나 제거할 수 있습니다.

다음은 Redis CLI를 사용하여 Redis Enterprise에서 탄력성을 활성화하는 방법의 예입니다.

```
redis-cli -h <redis-enterprise-cluster-url> -p <redis-enterprise-cluster-port> CONFIG SET maxmemory-policy allkeys-lru
```

## 결론

Redis Enterprise는 고가용성, 확장성 및 성능을 제공하는 분산 인메모리 데이터베이스입니다. Redis Enterprise는 높은 처리량과 짧은 대기 시간이 필요한 중요한 애플리케이션을 지원하도록 설계되었습니다. Redis Enterprise는 클라우드 서비스로 제공되므로 쉽게 사용하고 확장할 수 있습니다. Redis Enterprise는 샤딩, 복제, 자동 장애 조치, 탄력성을 포함하여 클라우드에서 Redis를 쉽게 확장할 수 있는 몇 가지 기능을 제공합니다.

## 외부 리소스

- [레디스 엔터프라이즈 문서](https://redislabs.com/redis-enterprise-documentation/)
- [AWS의 Redis 엔터프라이즈](https://aws.amazon.com/marketplace/pp/B0841VJ6M4)
- [Azure의 Redis Enterprise](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/redislabs.redis-enterprise)
- [GCP의 Redis Enterprise](https://cloud.google.com/marketplace/partners/redislabs/redis-enterprise)