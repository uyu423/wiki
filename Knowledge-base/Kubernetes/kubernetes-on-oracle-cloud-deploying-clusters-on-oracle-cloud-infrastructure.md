---
title: Oracle Cloud의 Kubernetes: Oracle Cloud Infrastructure에 클러스터 배포
description: 
published: true
date: 2023-02-01T11:57:50.415Z
tags: 
editor: markdown
dateCreated: 2023-02-01T11:57:46.960Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Kubernetes on Oracle Cloud: Deploying Clusters on Oracle Cloud Infrastructure***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-oracle-cloud-deploying-clusters-on-oracle-cloud-infrastructure)
{.links-list}


# Oracle Cloud의 Kubernetes: Oracle Cloud Infrastructure에 클러스터 배포

Kubernetes는 컨테이너화된 애플리케이션을 대규모로 배포하고 관리하는 데 사용할 수 있는 인기 있는 오픈 소스 컨테이너 오케스트레이션 플랫폼입니다. OCI(Oracle Cloud Infrastructure)는 컴퓨팅, 스토리지 및 네트워킹을 비롯한 다양한 서비스를 제공하는 클라우드 컴퓨팅 플랫폼입니다.

이 문서에서는 Oracle Cloud Infrastructure에 Kubernetes 클러스터를 배포하는 방법을 보여줍니다. 다음 주제를 다룹니다.

- Oracle Cloud Infrastructure 계정 생성
- Kubernetes 클러스터 생성
- Kubernetes 클러스터에 샘플 애플리케이션 배포

## Oracle Cloud Infrastructure 계정 생성

Oracle Cloud Infrastructure 계정이 없는 경우 무료로 만들 수 있습니다. 계정을 만들려면:

1. [Oracle Cloud Infrastructure 가입 페이지](https://cloud.oracle.com/en_US/tryit)로 이동합니다.
2. 정보를 입력하고 **계정 만들기**를 클릭합니다.
3. 지침에 따라 계정을 확인합니다.

계정이 확인되면 [Oracle Cloud Infrastructure 콘솔](https://console.us-ashburn-1.oraclecloud.com/a/billing)에 로그인할 수 있습니다.

## 쿠버네티스 클러스터 만들기

 Kubernetes용 Oracle Cloud Infrastructure Container Engine은 Oracle Cloud Infrastructure에서 Kubernetes 클러스터를 쉽게 배포하고 관리할 수 있는 관리 서비스입니다. Kubernetes용 Container Engine을 사용하면 몇 분 안에 Kubernetes 클러스터를 생성할 수 있습니다.

Kubernetes 클러스터를 생성하려면:

1. [Oracle Cloud Infrastructure 콘솔](https://console.us-ashburn-1.oraclecloud.com/a/billing)에 로그인합니다.
2. 탐색 메뉴에서 **컨테이너**를 클릭한 다음 **컨테이너 클러스터**를 클릭합니다.
3. **클러스터 생성**을 클릭합니다.
4. 다음 정보를 입력합니다.

- **이름**: 클러스터의 이름을 입력합니다.
- **Kubernetes 버전**: 사용하려는 Kubernetes 버전을 선택합니다.
- **네트워크 옵션**:
  - **가상 클라우드 네트워크**: 새로운 가상 클라우드 네트워크를 생성하거나 기존 네트워크를 선택합니다.
  - **서브넷**: 새 서브넷을 생성하거나 기존 서브넷을 선택합니다.
  - **공개 IP 주소**: 새로운 공인 IP 주소를 생성하거나 기존 주소를 선택합니다.
- **노드 풀**:
  - **이름**: 노드 풀의 이름을 입력합니다.
  - **Kubernetes 버전**: 사용하려는 Kubernetes 버전을 선택합니다.
  - **이미지 유형**: 사용하려는 이미지 유형을 선택합니다.
  - **도형**: 사용하려는 도형을 선택합니다.
  - **초기 노드**: 생성할 노드 수를 입력합니다.
  - **Max Nodes**: 허용할 최대 노드 수를 입력합니다.
  - **최소 노드**: 허용할 최소 노드 수를 입력합니다.
- **스토리지 옵션**:
  - **스토리지 클래스**: 사용하려는 스토리지 클래스를 선택합니다.
  - **크기(GB)**: 사용하려는 저장소의 크기를 입력합니다.
- **노드 메타데이터**:
  - **라벨**: 사용하려는 라벨을 입력합니다.
  - **주석**: 사용하려는 주석을 입력합니다.
- **Node Taints**: 사용하려는 오염을 입력합니다.
- **서비스 계정**: 사용하려는 서비스 계정을 입력합니다.
- **RBAC**: 사용하려는 RBAC 옵션을 선택합니다.

5. **클러스터 생성**을 클릭합니다.

클러스터가 생성되는 데 몇 분 정도 걸립니다. 클러스터가 실행되면 **클러스터 보기**를 클릭하여 클러스터 세부 정보를 볼 수 있습니다.

## Kubernetes 클러스터에 샘플 애플리케이션 배포

이제 Kubernetes 클러스터가 실행 중이므로 클러스터에 샘플 애플리케이션을 배포할 수 있습니다. 샘플 애플리케이션을 배포하려면:

1. [Oracle Cloud Infrastructure 콘솔](https://console.us-ashburn-1.oraclecloud.com/a/billing)에 로그인합니다.
2. 탐색 메뉴에서 **컨테이너**를 클릭한 다음 **컨테이너 클러스터**를 클릭합니다.
3. 애플리케이션을 배포하려는 클러스터의 이름을 클릭합니다.
4. **애플리케이션 배포**를 클릭합니다.
5. 다음 정보를 입력합니다.

- **응용 프로그램 유형**: 배포할 응용 프로그램 유형을 선택합니다.
- **애플리케이션 이름**: 애플리케이션의 이름을 입력합니다.
- **이미지 이름**: 사용하려는 이미지의 이름을 입력합니다.
- **이미지 태그**: 사용하려는 이미지의 태그를 입력하세요.
- **이미지 풀 정책**: 사용하려는 이미지 풀 정책을 선택합니다.
- **명령**: 사용하려는 명령을 입력합니다.
- **인수**: 사용할 인수를 입력합니다.
- **환경 변수**: 사용할 환경 변수를 입력합니다.
- **작업 디렉토리**: 사용할 작업 디렉토리를 입력합니다.
- **포트**: 사용할 포트를 입력하세요.
- **서비스 계정**: 사용할 서비스 계정을 입력합니다.
- **라벨**: 사용하려는 라벨을 입력합니다.
- **주석**: 사용하려는 주석을 입력합니다.
- **한도**: 사용하려는 한도를 입력합니다.
- **요청**: 사용하려는 요청을 입력합니다.

6. **배포**를 클릭합니다.

응용 프로그램을 배포하는 데 몇 분 정도 걸립니다. 응용 프로그램이 배포되면 **응용 프로그램 보기**를 클릭하여 응용 프로그램의 세부 정보를 볼 수 있습니다.

## 결론

이 기사에서는 Oracle Cloud Infrastructure에 Kubernetes 클러스터를 배포하는 방법을 설명했습니다. 또한 Kubernetes 클러스터에 샘플 애플리케이션을 배포하는 방법도 보여 주었습니다.