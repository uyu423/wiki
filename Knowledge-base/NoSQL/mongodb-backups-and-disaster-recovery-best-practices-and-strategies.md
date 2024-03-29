---
title: MongoDB 백업 및 재해 복구: 모범 사례 및 전략
description: 
published: true
date: 2023-03-03T14:32:50.473Z
tags: 
editor: markdown
dateCreated: 2023-03-03T14:32:43.314Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MongoDB Backups and Disaster Recovery: Best Practices and Strategies***English** document is available*](/en/Knowledge-base/NoSQL/mongodb-backups-and-disaster-recovery-best-practices-and-strategies)
{.links-list}


## 소개
MongoDB는 최신 애플리케이션을 위한 확장성, 성능 및 유연성을 제공하는 널리 사용되는 NoSQL 데이터베이스입니다. 그러나 다른 데이터베이스와 마찬가지로 하드웨어 오류, 소프트웨어 버그, 인적 오류 및 자연 재해로 인해 데이터 손실 및 손상에 취약합니다. 따라서 MongoDB 데이터를 보호하고 비즈니스 연속성을 보장하기 위해 백업 및 재해 복구(DR) 계획을 수립하는 것이 중요합니다. 이 기사에서는 도구, 기술 및 팁을 포함하여 MongoDB 백업 및 DR에 대한 모범 사례 및 전략에 대해 설명합니다.

## 백업 유형
백업 및 DR 전략에 대해 알아보기 전에 먼저 MongoDB가 지원하는 다양한 유형의 백업을 이해해 보겠습니다.

### 전체 백업
전체 백업은 모든 컬렉션, 인덱스 및 설정을 포함하는 MongoDB 데이터베이스의 전체 복사본입니다. 가장 포괄적이고 신뢰할 수 있는 백업 형식이지만 가장 많은 시간과 자원을 소모하기도 합니다. 전체 백업은 일반적으로 데이터의 크기와 중요도에 따라 매일 또는 매주와 같이 주기적으로 수행됩니다.

### 증분 백업
증분 백업은 마지막 전체 백업 또는 증분 백업 이후 변경된 내용만 포함하는 MongoDB 데이터베이스의 부분 복사본입니다. 특히 자주 업데이트되는 대용량 데이터베이스의 경우 백업 시간과 저장 공간을 크게 줄일 수 있습니다. 그러나 증분 백업은 일관성과 무결성을 보장하기 위해 신중한 관리와 동기화가 필요합니다.

### 특정 시점 백업
특정 시점 백업은 업무 종료 또는 주요 트랜잭션과 같은 특정 시점에 생성된 MongoDB 데이터베이스의 스냅샷입니다. 최신 버전이 아닌 특정 상태로 데이터베이스를 복원할 수 있습니다. 지정 시간 백업은 규정 또는 감사 요구 사항을 준수해야 하는 기업이나 데이터가 빠르게 변경되는 변동성 환경에서 운영되는 기업에 유용합니다.

## 백업 전략
이제 백업 유형을 알았으니 MongoDB의 백업 전략과 모범 사례를 살펴보겠습니다.

### 전용 백업 서버 사용
프로덕션 서버가 아닌 전용 백업 서버 또는 인스턴스를 사용하여 백업을 수행하는 것이 좋습니다. 이렇게 하면 백업 프로세스가 애플리케이션의 성능이나 가용성을 방해하지 않습니다. 또한 실수로 덮어쓰거나 삭제하여 데이터가 손실되거나 손상될 위험이 줄어듭니다.

### 올바른 백업 도구 선택
MongoDB는 기능, 성능 및 비용이 다른 여러 백업 도구를 제공합니다. 가장 일반적인 백업 도구는 다음과 같습니다.

- mongodump: 로컬 또는 원격 파일 시스템에 데이터베이스의 BSON 덤프를 생성하는 기본 백업 유틸리티입니다. 간단하고 무료이며 소규모 데이터베이스에 적합하지만 병렬 처리 및 압축이 제한적입니다.
- mongorestore: BSON 덤프를 MongoDB 인스턴스로 로드하는 기본 복원 유틸리티입니다. mongodump와 호환되며 --gzip, --archive 및 --oplogReplay와 같은 다양한 옵션을 지원합니다.
- MongoDB Cloud Manager: 백업 프로세스를 자동화하고 특정 시점 복구를 제공하며 다른 MongoDB 도구와 통합하는 클라우드 기반 백업 및 모니터링 서비스입니다. 확장 가능하고 안전하며 구독 기반 가격 책정 모델이 있습니다.
- 타사 백업 도구: 지속적인 백업, 글로벌 중복 제거 및 교차 플랫폼 지원과 같은 고급 기능을 제공하는 많은 타사 백업 도구가 있습니다. 인기 있는 옵션으로는 Ops Manager, Bacula, Commvault 및 Veeam이 있습니다.

필요, 예산 및 전문성에 맞는 백업 도구를 선택하십시오. 백업 빈도, 보존 기간, 백업 위치, 압축, 암호화 및 모니터링과 같은 요소를 고려하십시오.

### 백업 테스트 및 검증
백업을 생성하는 것만으로는 충분하지 않으며 백업이 완전하고 일관되며 복구 가능한지 정기적으로 검증해야 합니다. 백업 테스트에는 별도의 MongoDB 인스턴스 또는 다른 서버로 백업을 복원하고 데이터가 온전하고 사용 가능한지 확인하는 작업이 포함됩니다. 이 프로세스는 컬렉션 누락, 잘못된 인덱스 또는 데이터 손상과 같은 백업 프로세스의 모든 문제를 식별하는 데 도움이 됩니다.

### 백업을 오프사이트에 안전하게 저장
프로덕션 데이터와 동일한 서버 또는 디스크에 백업을 저장하는 것은 동일한 위협 및 취약성에 노출되기 때문에 위험합니다. 대신 물리적 또는 환경적 재해로부터 백업을 보호하기 위해 가급적이면 다른 지리적 위치에 백업을 저장합니다. 또한 암호화, 인증 및 액세스 제어를 사용하여 무단 액세스 또는 변조로부터 백업을 보호하십시오.

### 백업 및 DR 작업 자동화
수동 백업 및 DR 작업은 오류, 지연 및 인적 요인이 발생하기 쉽습니다. 따라서 스크립트, 도구 또는 서비스를 사용하여 이러한 작업을 자동화하는 것이 좋습니다. 자동화를 통해 일정 및 정책에 따라 백업이 일관되게 수행되고 중단 또는 장애 발생 시 DR 절차가 즉시 시작됩니다. 또한 자동화는 생산성을 높이고 비용을 절감하며 규정 준수를 향상시킵니다.

## 재해 복구 전략
백업 외에도 DR(재해 복구)은 MongoDB 데이터 보호 계획의 필수 구성 요소입니다. DR은 하드웨어 장애, 소프트웨어 버그, 사이버 공격 또는 자연 재해와 같은 중단 후 데이터베이스를 기능 상태로 복원하는 프로세스를 나타냅니다. 다음은 MongoDB에 대한 몇 가지 DR 전략 및 모범 사례입니다.

### RPO 및 RTO 식별
RPO(복구 지점 목표) 및 RTO(복구 시간 목표)는 재해 발생 시 허용 가능한 데이터 손실 및 가동 중지 시간을 정의하는 중요한 메트릭입니다. RPO는 백업 데이터의 최대 허용 기간을 측정하는 반면 RTO는 재해로부터 복구하는 최대 허용 시간을 측정합니다. RPO 및 RTO를 식별하면 적절한 백업 및 DR 방법을 선택하고 필요한 리소스를 할당하며 복구 작업의 우선 순위를 지정하는 데 도움이 됩니다.

### 복제 및 샤딩 사용
복제 및 샤딩은 데이터베이스의 가용성, 내구성 및 확장성을 향상시키는 두 가지 MongoDB 기능입니다. 복제는 서로 다른 서버에 여러 데이터 복사본을 생성하여 자동 장애 조치 및 복구를 가능하게 합니다. 샤딩은 데이터를 여러 샤드 또는 클러스터에 분산하여 수평 확장 및 로드 밸런싱을 허용합니다. 복제와 샤딩 모두 중복 및 분산 데이터를 제공하여 재해의 영향을 최소화하는 데 도움이 될 수 있습니다.

### DR 계획 테스트 및 검증
백업과 마찬가지로 DR 계획도 정기적으로 테스트하고 검증하여 예상대로 작동하고 RPO 및 RTO 요구 사항을 충족하는지 확인해야 합니다. DR 계획 테스트에는 서버 중단, 네트워크 오류 또는 데이터 손상과 같은 다양한 재해 시나리오를 시뮬레이션하고 복구 프로세스가 성공적이고 완료되었는지 확인하는 작업이 포함됩니다. 이 프로세스는 누락된 단계, 잘못된 종속성 또는 리소스 부족과 같은 DR 계획의 차이나 문제를 식별하는 데 도움이 됩니다.

### DR 절차 문서화 및 교육
DR 절차는 문서화되어 IT 직원, 관리자 및 비즈니스 소유자를 포함한 모든 관련 이해 관계자에게 전달되어야 합니다. 문서에는 자세한 단계, 역할 및 책임, 연락처 정보 및 에스컬레이션 절차가 포함되어야 합니다. 또한 모든 당사자가 DR 절차를 숙지하고 실제 상황에서 효과적으로 실행할 수 있도록 정기적인 교육 및 훈련을 실시해야 합니다.

## 결론
MongoDB 백업 및 재해 복구는 데이터 보호 및 비즈니스 연속성의 중요한 측면입니다. 이 문서에서 설명하는 모범 사례와 전략을 따르면 예기치 않은 이벤트가 발생하더라도 MongoDB 데이터의 가용성, 내구성 및 복구 가능성을 보장할 수 있습니다. 올바른 백업 도구를 선택하고, 백업을 정기적으로 검증하고, 백업을 오프사이트에 안전하게 저장하고, 백업 및 DR 작업을 자동화하고, RPO 및 RTO를 식별하고, 복제 및 샤딩을 사용하고, DR 계획을 테스트 및 검증하고, DR 절차를 문서화하고 교육해야 합니다.

## 외부 리소스
- [MongoDB 백업 방법](https://docs.mongodb.com/manual/core/backups/) - 백업 방법에 대한 공식 MongoDB 문서.
- [MongoDB 백업 및 복원 전략](https://www.mongodb.com/blog/post/mongodb-backup-and-restore-strategy) - MongoDB의 백업 및 복원 전략을 설명하는 블로그 게시물입니다.
- [MongoDB 재해 복구 가이드](https://www.mongodb.com/content/mongodb-disaster-recovery-guide) - MongoDB 재해 복구에 대한 포괄적인 가이드입니다.
- [MongoDB 백업 및 복구 모범 사례](https://www.percona.com/resources/technical-presentations/mongodb-backup-and-recovery-best-practices) - MongoDB 백업 및 복구 모범 사례에 대한 기술 프레젠테이션입니다.