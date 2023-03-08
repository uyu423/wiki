---
title: AWS Elastic Load Balancer: 클라우드에서 애플리케이션 확장 및 로드 밸런싱
description: 
published: true
date: 2023-02-17T18:08:53.210Z
tags: 
editor: markdown
dateCreated: 2023-01-30T17:04:36.909Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [AWS Elastic Load Balancer: Scaling and Load Balancing Applications in the Cloud***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-elastic-load-balancer-scaling-and-load-balancing-applications-in-the-cloud)
{.links-list}


# AWS Elastic Load Balancer: 클라우드에서 애플리케이션 확장 및 로드 밸런싱

ELB(Elastic Load Balancer)는 클라우드에서 애플리케이션의 확장성과 성능을 개선하는 데 도움이 되는 웹 서비스입니다. 클라우드의 여러 서버 간에 부하를 분산하고 부하에 따라 서버 수를 자동으로 늘리거나 줄일 수 있습니다. 이렇게 하면 애플리케이션의 가용성과 응답성을 개선하는 데 도움이 될 수 있습니다.

ELB는 여러 가용 영역에 있는 여러 Amazon EC2 인스턴스 간에 트래픽을 로드 밸런싱하는 데 사용할 수 있습니다. 온프레미스 리소스와 Amazon EC2 인스턴스 간의 트래픽 균형을 맞추는 데에도 사용할 수 있습니다.

## Elastic Load Balancer란 무엇입니까?

Elastic Load Balancer는 클라우드에서 애플리케이션의 확장성과 성능을 개선하는 데 도움이 되는 웹 서비스입니다. 클라우드의 여러 서버 간에 부하를 분산하고 부하에 따라 서버 수를 자동으로 늘리거나 줄일 수 있습니다. 이렇게 하면 애플리케이션의 가용성과 응답성을 개선하는 데 도움이 될 수 있습니다.

ELB는 여러 가용 영역에 있는 여러 Amazon EC2 인스턴스 간에 트래픽을 로드 밸런싱하는 데 사용할 수 있습니다. 온프레미스 리소스와 Amazon EC2 인스턴스 간의 트래픽 균형을 맞추는 데에도 사용할 수 있습니다.

## Elastic Load Balancer를 사용하면 어떤 이점이 있나요?

ELB를 사용하면 다음과 같은 많은 이점이 있습니다.

- 자동 확장: ELB는 부하에 따라 서버 수를 자동으로 늘리거나 줄일 수 있으므로 애플리케이션이 항상 적절한 용량을 갖게 됩니다.

- 고가용성: ELB는 여러 가용 영역의 여러 서버에 트래픽을 분산하므로 하나의 서버가 실패하더라도 애플리케이션을 항상 사용할 수 있습니다.

- 중앙 집중식 관리: ELB는 애플리케이션의 확장성과 성능을 관리하기 위한 중앙 제어 지점을 제공합니다.

## Elastic Load Balancer의 기능은 무엇인가요?

ELB에는 다음과 같은 기능이 있습니다.

- 동적 확장: ELB는 부하에 따라 자동으로 서버 수를 늘리거나 줄입니다.

- 고가용성: ELB는 여러 가용 영역의 여러 서버에 트래픽을 분산합니다.

- 중앙 집중식 관리: ELB는 애플리케이션의 확장성과 성능을 관리하기 위한 중앙 제어 지점을 제공합니다.

- 모니터링: ELB는 성능 문제를 해결하는 데 사용할 수 있는 모니터링 데이터를 제공합니다.

- 트래픽 라우팅: ELB는 사용자의 지리적 위치, 시간 또는 장치 유형과 같은 요소를 기반으로 트래픽을 라우팅할 수 있습니다.

- SSL 종료: ELB는 SSL 연결을 종료하고 트래픽 암호화 및 복호화 작업을 서버로 오프로드할 수 있습니다.

- 보안: ELB는 네트워크 방화벽 및 IP 주소 필터링과 같은 보안 기능을 제공할 수 있습니다.

## Elastic Load Balancer는 어떻게 작동하나요?

ELB는 클라우드에서 애플리케이션의 확장성과 성능을 향상시키는 데 도움이 되는 웹 서비스입니다. 클라우드의 여러 서버 간에 부하를 분산하고 부하에 따라 서버 수를 자동으로 늘리거나 줄일 수 있습니다. 이렇게 하면 애플리케이션의 가용성과 응답성을 개선하는 데 도움이 될 수 있습니다.

ELB는 여러 가용 영역에 있는 여러 Amazon EC2 인스턴스 간에 트래픽을 로드 밸런싱하는 데 사용할 수 있습니다. 온프레미스 리소스와 Amazon EC2 인스턴스 간의 트래픽 균형을 맞추는 데에도 사용할 수 있습니다.

## Elastic Load Balancer를 생성하려면 어떻게 해야 하나요?

AWS Management Console, AWS 명령줄 인터페이스 또는 AWS SDK를 사용하여 ELB를 생성할 수 있습니다.

## Elastic Load Balancer는 어떻게 구성하나요?

AWS Management Console, AWS 명령줄 인터페이스 또는 AWS SDK를 사용하여 ELB를 구성할 수 있습니다.

## Elastic Load Balancer를 설정하는 단계는 무엇입니까?

ELB를 설정하는 단계는 다음과 같습니다.

1. ELB 생성: AWS Management Console, AWS 명령줄 인터페이스 또는 AWS SDK를 사용하여 ELB를 생성할 수 있습니다.

2. ELB 구성: AWS Management Console, AWS 명령줄 인터페이스 또는 AWS SDK를 사용하여 ELB를 구성할 수 있습니다.

3. Amazon EC2 인스턴스 연결: AWS Management Console, AWS 명령줄 인터페이스 또는 AWS SDK를 사용하여 Amazon EC2 인스턴스를 ELB에 연결할 수 있습니다.

4. ELB 테스트: AWS Management Console, AWS 명령줄 인터페이스 또는 AWS SDK를 사용하여 ELB를 테스트할 수 있습니다.