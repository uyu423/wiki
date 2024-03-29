---
title: 고가용성을 위한 클러스터 관리
description: 
published: true
date: 2023-02-12T20:55:24.559Z
tags: 
editor: markdown
dateCreated: 2023-02-12T20:55:22.954Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Managing Clusters for High Availability***English** document is available*](/en/Knowledge-base/Backend/managing-clusters-for-high-availability)
{.links-list}


# 고가용성을 위한 클러스터 관리

 고가용성은 합의된 수준의 운영 성능(일반적으로 가동 시간)을 정상 기간보다 더 오래 보장하는 것을 목표로 하는 시스템의 특성입니다. 고가용성을 달성하려면 종종 시스템 전체에 중복성을 배치해야 합니다. 예를 들어 구성 요소에 오류가 발생하면 시스템은 서비스 중단 없이 중복 구성 요소로 전환할 수 있습니다.

IT 시스템은 점점 미션 크리티컬해지고 있으며 하루 24시간 연중무휴로 사용할 수 있어야 합니다. 그러나 시스템이 아무리 잘 설계되고 구축되더라도 구성 요소는 언젠가는 필연적으로 실패합니다. 고가용성을 달성하는 핵심은 서비스 중단 없이 구성 요소 오류를 허용할 수 있도록 시스템을 설계하는 것입니다.

고가용성을 설계할 때 다음을 포함하여 고려해야 할 많은 요소가 있습니다.

- 하드웨어: 서버, 스토리지, 네트워킹 등
- 소프트웨어: 운영 체제, 애플리케이션, 데이터베이스 등
- 프로세스: 모니터링, 백업 및 복구 등

## 하드웨어

중복 하드웨어 구성 요소는 고가용성을 달성하는 데 핵심적인 부분입니다. 예를 들어 서버에 오류가 발생하면 시스템이 중복 서버로 전환할 수 있습니다.

일반적인 중복 하드웨어 구성 요소는 다음과 같습니다.

- 서버: 여러 서버를 사용할 수 있으며 각 서버는 시스템의 다른 구성 요소를 실행합니다. 예를 들어 한 서버는 애플리케이션을 실행하고 다른 서버는 데이터베이스를 실행할 수 있습니다.
- 스토리지: 스토리지는 여러 서버에 걸쳐 복제될 수 있습니다. 예를 들어 응용 프로그램과 데이터베이스를 서로 다른 두 서버에 저장할 수 있습니다.
- 네트워크: 여러 네트워크 연결을 사용할 수 있으며 각 연결은 다른 스위치로 실행됩니다.

## 소프트웨어

시스템의 소프트웨어 구성요소도 고가용성을 위해 설계되어야 합니다. 예를 들어 애플리케이션은 서버 오류를 정상적으로 처리하도록 설계되어야 합니다.

고가용성을 달성하기 위한 일반적인 소프트웨어 기술은 다음과 같습니다.

- 로드 밸런싱: 여러 서버를 사용할 수 있으며 각 서버는 시스템의 다른 구성 요소를 실행합니다. 예를 들어 한 서버는 애플리케이션을 실행하고 다른 서버는 데이터베이스를 실행할 수 있습니다.
- 복제: 데이터를 여러 서버에 걸쳐 복제할 수 있습니다. 예를 들어 응용 프로그램과 데이터베이스를 서로 다른 두 서버에 저장할 수 있습니다.
- 클러스터링: 여러 서버를 함께 클러스터링할 수 있으므로 한 서버가 실패하면 다른 서버가 대신할 수 있습니다.

## 프로세스

하드웨어 및 소프트웨어 구성 요소 외에도 시스템 프로세스도 고가용성을 위해 설계되어야 합니다. 예를 들어 모든 구성 요소 오류를 감지하고 신속하게 해결할 수 있도록 시스템을 모니터링해야 합니다.

고가용성을 달성하기 위한 일반적인 프로세스는 다음과 같습니다.

- 모니터링: 모든 구성 요소 오류를 신속하게 감지할 수 있도록 시스템을 모니터링해야 합니다.
- 백업 및 복구: 시스템을 정기적으로 백업해야 구성 요소가 실패할 경우 시스템을 신속하게 복구할 수 있습니다.

## 결론

고가용성을 달성하는 것은 IT 시스템의 핵심 목표입니다. 하드웨어, 소프트웨어 및 프로세스를 포함하여 고가용성을 설계할 때 고려해야 할 많은 요소가 있습니다.