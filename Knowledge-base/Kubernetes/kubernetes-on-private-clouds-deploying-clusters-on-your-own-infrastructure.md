---
title: 사설 클라우드의 Kubernetes: 자체 인프라에 클러스터 배포
description: 
published: true
date: 2023-02-14T07:32:42.295Z
tags: 
editor: markdown
dateCreated: 2023-02-14T07:32:40.472Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes on Private Clouds: Deploying Clusters on Your Own Infrastructure***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-private-clouds-deploying-clusters-on-your-own-infrastructure)
{.links-list}


# 프라이빗 클라우드의 쿠버네티스: 자체 인프라에 클러스터 배포

Kubernetes는 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하는 기능으로 인해 최근 몇 년 동안 인기를 얻은 오픈 소스 컨테이너 오케스트레이션 도구입니다.

Kubernetes는 AWS(Amazon Web Services), GCP(Google Cloud Platform) 및 Microsoft Azure와 같은 퍼블릭 클라우드에 배포할 수 있지만 많은 조직에서는 보안, 비용 또는 데이터 주권을 이유로 자체 프라이빗 인프라에서 Kubernetes를 실행하는 것을 선호합니다.

이 기사에서는 Kubernetes 컨테이너 오케스트레이션 도구에 대한 개요를 제공하고 온프레미스 또는 프라이빗 클라우드에 관계없이 자체 인프라에 Kubernetes 클러스터를 배포하는 방법을 보여줍니다.

## 쿠버네티스란?

Kubernetes는 컨테이너화된 워크로드 및 서비스를 관리하기 위한 이식 가능하고 확장 가능한 오픈 소스 플랫폼으로, 선언적 구성과 자동화를 모두 용이하게 합니다. 그것은 크고 빠르게 성장하는 생태계를 가지고 있습니다. Kubernetes 서비스, 지원 및 도구는 광범위하게 사용할 수 있습니다.

Kubernetes는 원래 Google에서 설계했으며 현재 Cloud Native Computing Foundation에서 유지 관리합니다.

## 쿠버네티스의 특징

Kubernetes의 주요 기능 중 일부는 다음과 같습니다.

- 컨테이너화된 애플리케이션의 자동화된 배포 및 확장
- 부하 분산 및 서비스 검색
- 스토리지 오케스트레이션
- 자가 치유
- 비밀 및 구성 관리

## 쿠버네티스의 이점

Kubernetes를 사용하면 다음과 같은 많은 이점이 있습니다.

- 효율성 향상: Kubernetes는 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하여 개발 및 운영 팀의 효율성을 높이는 데 도움을 줄 수 있습니다.
-향상된 가동 시간: Kubernetes의 자가 복구 기능은 충돌한 컨테이너를 자동으로 다시 시작하고 실패한 컨테이너를 복제하여 애플리케이션의 가동 시간을 개선하는 데 도움이 될 수 있습니다.
- 민첩성 향상: Kubernetes의 선언적 구성 및 자동화를 통해 애플리케이션을 신속하게 배포하고 업데이트할 수 있으므로 개발 프로세스의 민첩성을 높일 수 있습니다.
-운영 비용 절감: Kubernetes는 컨테이너화된 애플리케이션의 관리를 자동화하여 인프라의 운영 비용을 줄이는 데 도움을 줄 수 있습니다.

## 쿠버네티스 아키텍처

Kubernetes는 다양한 구성 요소가 포함된 복잡한 시스템입니다. 다음은 Kubernetes 아키텍처에 대한 개략적인 개요입니다.

- 마스터 노드는 Kubernetes 클러스터의 핵심입니다. 클러스터 관리 및 클러스터 상태 기록 유지를 담당합니다. 마스터 노드는 다음 구성 요소로 구성됩니다.
  - API 서버는 Kubernetes 클러스터의 통신 중심점입니다. Kubernetes API 노출 및 API 요청 처리를 담당합니다.
  - 스케줄러는 클러스터의 노드에서 실행되도록 Pod를 예약하는 역할을 합니다.
  - 컨트롤러 관리자는 클러스터 상태 관리를 담당합니다.
- 작업자 노드는 Pod가 실제로 배포되는 Kubernetes 클러스터의 노드입니다. 클러스터의 각 포드는 작업자 노드에 배포됩니다.

## 쿠버네티스 컴포넌트

Kubernetes는 여러 구성 요소로 구성되며 각 구성 요소는 Kubernetes 클러스터의 기능에서 특정한 역할을 합니다. 다음은 Kubernetes 구성 요소에 대한 간략한 개요입니다.

- API 서버는 Kubernetes 클러스터의 통신 중심점입니다. Kubernetes API 노출 및 API 요청 처리를 담당합니다.
- 스케줄러는 클러스터의 노드에서 실행되도록 Pod를 예약하는 역할을 합니다.
- 컨트롤러 관리자는 클러스터 상태 관리를 담당합니다.
- Etcd 구성 요소는 Kubernetes 클러스터의 구성 데이터 저장을 담당합니다.
- Kubelet은 Kubernetes 클러스터의 노드에서 포드 실행을 담당합니다.
- Kube-Proxy는 Kubernetes 클러스터의 올바른 포드로 트래픽을 라우팅하는 역할을 합니다.

## 자체 인프라에 Kubernetes 배포

자체 인프라에 Kubernetes를 배포하는 방법에는 여러 가지가 있습니다. 다음은 가장 널리 사용되는 방법 중 일부입니다.

- Canonical의 MicroK8s, Red Hat OpenShift 또는 VMware TKGI(Tanzu Kubernetes Grid Integrated Edition)와 같은 Kubernetes 관련 솔루션을 사용합니다.
- Hashicorp Terraform, Puppet 또는 Ansible과 같은 클라우드 독립적인 솔루션을 사용합니다.
- AWS(Amazon Web Services) CloudFormation, Google Cloud Platform(GCP) Deployment Manager 또는 ARM(Azure Resource Manager) 템플릿과 같은 클라우드별 솔루션을 사용합니다.

## 결론

Kubernetes는 개발 및 운영 팀의 효율성과 민첩성을 높이는 데 도움이 되는 강력한 컨테이너 오케스트레이션 도구입니다. Kubernetes는 AWS, GCP, Azure와 같은 퍼블릭 클라우드 또는 자체 프라이빗 인프라에 배포할 수 있습니다.

이 문서에서는 Kubernetes 컨테이너 오케스트레이션 도구에 대한 개요를 제공하고 자체 인프라에 Kubernetes 클러스터를 배포하는 방법을 보여 주었습니다.