---
title: MongoDB 복제: 데이터 가용성 및 내구성을 보장하는 방법
description: 
published: true
date: 2023-03-03T09:32:21.177Z
tags: 
editor: markdown
dateCreated: 2023-03-03T09:32:21.177Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MongoDB Replication: How to Ensure Data Availability and Durability***English** document is available*](/en/Knowledge-base/NoSQL/mongodb-replication-how-to-ensure-data-availability-and-durability)
{.links-list}


MongoDB 복제: 데이터 가용성 및 내구성을 보장하는 방법

데이터베이스 복제는 IT 개발 분야에서 중요한 주제입니다. 이를 통해 조직은 미션 크리티컬 애플리케이션에 필수적인 데이터 가용성과 내구성을 향상할 수 있습니다. 이 기사에서는 MongoDB 복제, 작동 방식, 데이터 가용성 및 내구성을 보장하는 방법에 대해 설명합니다.

### MongoDB 복제란 무엇입니까?

MongoDB 복제는 하나의 MongoDB 인스턴스에서 다른 인스턴스로 데이터를 복사하는 프로세스입니다. 여기에는 복제본 세트라고 하는 여러 서버에 MongoDB 데이터의 여러 복사본을 만드는 작업이 포함됩니다. 복제본 세트는 두 개 이상의 MongoDB 인스턴스로 구성되며, 여기서 한 인스턴스는 기본 인스턴스이고 다른 인스턴스는 보조 인스턴스입니다.

기본 인스턴스는 모든 쓰기 작업을 처리하고 보조 인스턴스는 기본 인스턴스에서 데이터를 복제합니다. MongoDB 복제는 고가용성과 자동 장애 조치를 제공합니다. 즉, 기본 인스턴스가 실패하면 보조 인스턴스 중 하나가 자동으로 기본 인스턴스가 됩니다.

### 데이터 가용성 및 내구성 보장

MongoDB 복제는 미션 크리티컬 애플리케이션에 필수적인 데이터 가용성과 내구성을 제공합니다. 다음은 이를 보장하는 몇 가지 방법입니다.

#### 1. 적절한 복제 구성 선택

MongoDB는 단일 노드, 복제 세트 및 샤드 클러스터의 세 가지 복제 구성을 제공합니다. 단일 노드 구성은 복제를 제공하지 않는 반면 복제 세트 구성은 대부분의 배포에 가장 적합합니다.

복제 세트는 자동 장애 조치, 데이터 중복성 및 고가용성을 제공합니다. 반면에 분할된 클러스터 구성은 데이터가 분할되어 여러 인스턴스에 분산되는 대규모 배포에 가장 적합합니다.

#### 2. 쓰기 문제 구성

MongoDB는 성공적인 것으로 간주되기 전에 쓰기 작업을 확인해야 하는 MongoDB 인스턴스 수를 결정하는 쓰기 문제 기능을 제공합니다. 쓰기 문제는 'w'라고 하는 특정 인스턴스 수 또는 'wtimeout'이라고 하는 특정 시간으로 설정할 수 있습니다.

쓰기 문제를 더 높은 값으로 설정하면 데이터가 성공한 것으로 간주되기 전에 더 많은 인스턴스에 기록됩니다. 그러나 쓰기 대기 시간이 증가하는 비용이 발생합니다.

#### 3. 복제 지연 모니터링

복제 지연은 기본 인스턴스에 기록되는 데이터와 보조 인스턴스에 복제되는 데이터 사이의 시간 차이입니다. 복제 지연을 모니터링하는 것은 데이터 가용성과 내구성을 보장하는 데 중요합니다.

MongoDB는 복제 지연을 확인하는 내장 명령을 제공합니다. MongoDB 셸을 사용하여 복제 지연을 확인하려면 다음 명령을 사용합니다.

```shell
db.printSlaveReplicationInfo()
```

이 명령은 데이터를 적시에 복제하는 데 사용할 수 있는 기본 인스턴스와 보조 인스턴스 간의 복제 지연을 표시합니다.

#### 4. Read Concern을 사용하여 일관성 보장

MongoDB는 읽기 작업의 일관성 수준을 결정하는 Read Concern 기능을 제공합니다. 읽기 문제는 'local', 'majority' 또는 'linearizable'로 설정할 수 있습니다.

더 높은 일관성 수준으로 읽기 문제를 설정하면 더 많은 인스턴스에서 데이터를 읽을 수 있으므로 일관성이 향상되지만 읽기 지연 시간이 증가합니다.

#### 5. 정기적인 데이터 백업

정기적으로 데이터를 백업하는 것은 데이터 가용성과 내구성을 보장하는 데 중요합니다. MongoDB는 데이터를 백업할 수 있는 내장 백업 기능을 제공합니다.

MongoDB 인스턴스를 백업하려면 다음 명령을 사용하십시오.

```shell
mongodump --host <hostname> --port <port> --out <directory>
```

이 명령은 지정된 MongoDB 인스턴스의 백업을 가져와 지정된 디렉토리에 저장합니다.

### 결론

결론적으로 MongoDB 복제는 조직이 데이터 가용성과 내구성을 향상할 수 있도록 하는 중요한 기능입니다. 적절한 복제 구성 선택, 쓰기 문제 구성, 복제 지연 모니터링, 읽기 문제를 사용한 일관성 보장, 정기적인 데이터 백업을 통해 조직은 데이터의 가용성과 내구성을 보장할 수 있습니다.

### 외부 리소스

- [MongoDB 레플리카 설정 가이드](https://docs.mongodb.com/manual/replication/)
- [MongoDB 쓰기 우려 참조](https://docs.mongodb.com/manual/reference/write-concern/)
- [MongoDB Read Concern 참조](https://docs.mongodb.com/manual/reference/read-concern/)
- [MongoDB 백업 및 복원 가이드](https://docs.mongodb.com/manual/core/backups/)