---
title: AWS Fargate: 인프라 관리 없이 컨테이너 실행
description: 
published: true
date: 2023-02-19T04:32:19.081Z
tags: 
editor: markdown
dateCreated: 2023-02-19T04:32:17.672Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS Fargate: Running Containers without Managing Infrastructure***English** document is available*](/en/Knowledge-base/Cloud/aws-fargate-running-containers-without-managing-infrastructure)
{.links-list}


# AWS Fargate: 인프라 관리 없이 컨테이너 실행

AWS Fargate는 Amazon Elastic Container Service(ECS) 및 Amazon Elastic Container Service for Kubernetes(EKS)와 함께 작동하는 컨테이너용 서버리스 컴퓨팅 엔진입니다. Fargate를 사용하면 서버 인프라에 대해 걱정할 필요 없이 컨테이너화된 애플리케이션을 쉽게 실행하고 관리할 수 있습니다.

Fargate를 사용하면 더 이상 서버를 프로비저닝 또는 관리하고 운영 체제를 설치 및 유지 관리하거나 소프트웨어를 패치 및 업데이트할 필요가 없습니다. Fargate는 서버 유형 및 크기를 선택하거나 클러스터를 확장할 시기를 결정하거나 클러스터 활용을 최적화할 필요가 없습니다. 즉, 애플리케이션 구축 및 실행에 집중하고 AWS가 인프라에 대해 걱정할 수 있습니다.

Fargate는 현재 모든 상용 AWS 리전에서 사용할 수 있습니다.


## Fargate는 어떻게 작동합니까?

Fargate는 성능 및 보안에 최적화된 목적에 맞게 구축된 ENI(탄력적 네트워크 인터페이스)에서 컨테이너를 실행합니다. 컨테이너는 격리된 보안 그룹에서 실행되며 ENI를 사용하여 서로 통신할 수 있습니다.

Fargate는 두 가지 시작 유형을 제공합니다.

- Fargate 시작 유형 – 이 시작 유형을 사용하면 서버 또는 클러스터를 관리할 필요 없이 컨테이너를 실행할 수 있습니다. 작업에 필요한 CPU 및 메모리 리소스의 양만 지정하면 됩니다.
- EC2 시작 유형 – 이 시작 유형을 사용하면 Amazon EC2 인스턴스에서 컨테이너를 시작할 수 있습니다. ECS 또는 EKS 클러스터의 일부인 기존 Amazon EC2 인스턴스에서 Fargate 작업을 시작할 수 있습니다.

## Fargate를 사용하면 어떤 이점이 있습니까?

Fargate는 다음과 같은 여러 이점을 제공합니다.

- 서버나 클러스터를 관리할 필요가 없습니다 – Fargate를 사용하면 더 이상 서버를 프로비저닝하거나 관리할 필요가 없습니다. 즉, 애플리케이션 구축 및 실행에 집중하고 AWS가 인프라에 대해 걱정할 수 있습니다.
- 사용하기 쉬움 – Fargate는 사용하기 쉽습니다. 작업에 필요한 CPU 및 메모리 리소스의 양을 지정하기만 하면 Fargate가 기본 인프라를 프로비저닝하고 작업을 실행합니다.
- 유연성 – Fargate는 Fargate와 EC2의 두 가지 시작 유형을 제공합니다. Fargate 시작 유형을 사용하면 서버나 클러스터를 관리할 필요 없이 컨테이너를 실행할 수 있습니다. EC2 시작 유형을 사용하면 ECS 또는 EKS 클러스터의 일부인 기존 Amazon EC2 인스턴스에서 Fargate 작업을 시작할 수 있습니다.
- 보안 – Fargate는 격리된 보안 그룹에서 컨테이너를 실행하고 ENI를 사용하여 서로 통신할 수 있습니다.
- 확장 가능 – Fargate를 사용하면 애플리케이션을 쉽게 확장할 수 있습니다. 원하는 작업 수를 지정하기만 하면 Fargate가 필요에 따라 애플리케이션을 확장하거나 축소합니다.
- 모든 상용 AWS 리전에서 사용 가능 – Fargate는 모든 상용 AWS 리전에서 사용할 수 있습니다.