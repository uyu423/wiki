---
title: DigitalOcean의 Kubernetes: DigitalOcean에 클러스터 배포
description: 
published: true
date: 2023-02-17T18:02:58.697Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:26:55.615Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kubernetes on DigitalOcean: Deploying Clusters on DigitalOcean***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-digitalocean-deploying-clusters-on-digitalocean)
{.links-list}


# DigitalOcean의 Kubernetes: DigitalOcean에 클러스터 배포

Kubernetes는 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하는 오픈 소스 컨테이너 오케스트레이션 플랫폼입니다. 이식 가능하고 확장 가능하며 클러스터 관리 솔루션 구축을 위한 기반을 제공합니다.

DigitalOcean은 VPS(가상 사설 서버) 및 기타 클라우드 서비스를 제공하는 클라우드 컴퓨팅 플랫폼입니다. 웹 애플리케이션 및 마이크로 서비스를 호스팅하는 데 널리 사용되는 선택입니다.

이 문서에서는 DigitalOcean에 Kubernetes 클러스터를 배포하는 방법에 대한 개요를 제공합니다. 리소스 프로비저닝, 네트워킹 구성 및 애플리케이션 배포를 다룹니다.

## 리소스 프로비저닝

DigitalOcean은 손쉽게 리소스를 프로비저닝하고 Kubernetes 클러스터를 배포할 수 있는 Kubernetes 서비스를 제공합니다. 첫 번째 단계는 Kubernetes 클러스터를 만드는 것입니다. 이것은 제어판 또는 API를 통해 수행할 수 있습니다.

클러스터가 생성되면 클러스터에 노드를 추가해야 합니다. 노드는 수동 또는 자동으로 추가할 수 있습니다. 자동 노드 프로비저닝은 3개 이상의 노드가 있는 클러스터에서 사용할 수 있습니다.

## 네트워킹 구성

DigitalOcean의 Kubernetes 클러스터는 기본적으로 사설 네트워크와 함께 배포됩니다. 이 네트워크는 공용 인터넷과 격리되어 있으며 클러스터 내에서만 액세스할 수 있습니다.

인터넷에서 서비스에 액세스하려면 게이트웨이를 구성해야 합니다. 이는 Kubernetes 대시보드 또는 API를 통해 수행할 수 있습니다.

온프레미스 서비스에 액세스해야 하는 경우 VPN을 구성해야 합니다. DigitalOcean은 온프레미스 리소스에 연결하는 데 사용할 수 있는 IPsec VPN 서비스를 제공합니다.

## 애플리케이션 배포

Kubernetes 클러스터에 애플리케이션을 배포하려면 배포를 생성해야 합니다. 이는 Kubernetes 대시보드 또는 API를 통해 수행할 수 있습니다.

배포가 생성되면 사용할 컨테이너 이미지와 노출할 포트를 지정해야 합니다. 환경 변수 및 기타 옵션을 지정할 수도 있습니다.

배치가 생성된 후 서비스를 생성해야 합니다. 이렇게 하면 배포가 외부 세계에 노출됩니다. Kubernetes 대시보드 또는 API를 통해 서비스를 생성할 수 있습니다.

서비스가 생성되면 서비스 유형(LoadBalancer, ClusterIP 또는 NodePort)과 노출할 포트를 지정해야 합니다. 서비스 이름과 같은 다른 옵션을 지정할 수도 있습니다.

## 결론

이 기사에서는 DigitalOcean에서 Kubernetes 클러스터를 배포하는 기본 사항을 다뤘습니다. 리소스를 프로비저닝하고, 네트워킹을 구성하고, 애플리케이션을 배포하는 방법을 보여주었습니다.