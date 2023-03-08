---
title: 베어 메탈의 쿠버네티스: 물리적 서버에 클러스터 배포
description: 
published: true
date: 2023-02-14T08:33:07.664Z
tags: 
editor: markdown
dateCreated: 2023-02-14T08:33:06.018Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes on Bare Metal: Deploying Clusters on Physical Servers***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-bare-metal-deploying-clusters-on-physical-servers)
{.links-list}


# Kubernetes on Bare Metal: 물리적 서버에 클러스터 배포

오늘날 컨테이너는 애플리케이션을 패키징하고 배포하는 데 점점 더 많이 사용되고 있습니다. 이는 컨테이너가 기존 가상 머신에 비해 휴대성 향상, 더 작은 설치 공간, 더 빠른 시작 등 많은 이점을 제공하기 때문입니다.

Kubernetes는 많은 수의 컨테이너를 관리하는 데 사용할 수 있는 인기 있는 컨테이너 오케스트레이션 도구입니다. Kubernetes는 종종 클라우드 기반 솔루션과 함께 사용되지만 베어메탈 서버에도 배포할 수 있습니다.

베어메탈 서버에 Kubernetes를 배포하면 클라우드 기반 솔루션과 함께 사용하는 것보다 몇 가지 이점을 얻을 수 있습니다. 예를 들어 더 비용 효율적일 수 있고 하드웨어를 더 잘 제어할 수 있습니다.

이 기사에서는 베어메탈 서버에 Kubernetes 클러스터를 배포하는 방법을 살펴보겠습니다. 또한 이 작업을 수행할 때 직면할 수 있는 몇 가지 문제에 대해서도 살펴보겠습니다.

## 개요

시작하기 전에 이 문서에서 사용할 몇 가지 주요 개념을 간단히 살펴보겠습니다.

**Kubernetes**: Kubernetes는 많은 수의 컨테이너를 관리하는 데 사용할 수 있는 컨테이너 오케스트레이션 도구입니다.

**베어메탈 서버**: 베어메탈 서버는 가상화 계층이 없는 물리적 서버입니다.

**클러스터**: 클러스터는 애플리케이션 또는 서비스를 실행하는 데 사용되는 서버 그룹입니다.

**마스터 노드**: 마스터 노드는 Kubernetes 클러스터를 관리하는 데 사용되는 서버입니다.

**작업자 노드**: 작업자 노드는 컨테이너를 실행하는 데 사용되는 서버입니다.

## 전제 조건

시작하기 전에 다음 항목이 필요합니다.

- 베어메탈 서버 그룹입니다. 이 기사에서는 3개의 서버를 사용합니다.
- 서버가 연결될 수 있는 네트워크 스위치.
- 서버에 쿠버네티스를 설치하는 방법. 이 기사에서는 Kubernetes 설치 프로그램인 kubeadm을 사용합니다.

## 쿠버네티스 설치하기

이 섹션에서는 서버에 Kubernetes를 설치하는 방법을 살펴보겠습니다. Kubernetes 설치 프로그램인 kubeadm을 사용할 것입니다.

Kubeadm은 Kubernetes를 설치하고 구성하는 데 사용할 수 있는 도구입니다. 사용하기 쉽고 확장하기 쉽도록 설계되었습니다.

### kubeadm 설치

가장 먼저 해야 할 일은 서버에 kubeadm을 설치하는 것입니다. 다음 명령으로 이를 수행할 수 있습니다.

```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update && sudo apt-get install -y kubeadm
```

### 마스터 노드 초기화

kubeadm이 설치되면 마스터 노드를 초기화할 수 있습니다. Kubernetes 클러스터를 관리하는 데 사용할 서버입니다.

마스터 노드를 초기화하려면 kubeadm init 명령을 사용해야 합니다. 이 명령은 서버에서 Kubernetes 컨트롤 플레인을 시작합니다.

```
sudo kubeadm init
```

명령이 완료되면 다음과 같은 메시지가 표시됩니다.

```
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following commands:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

You can now join any number of machines by running the following on each node
as root:

  kubeadm join 10.0.0.1:6443 --token ahc2xf.i0f4v9f0johtr5b4 --discovery-token-ca-cert-hash sha256:7ad1f8d3c908f3f558eaebf09abf8c3bdbbebfa7a7faebcbadea1a1a7fd0c74
```

Kubernetes 클러스터를 사용하도록 서버를 구성하려면 출력에 나열된 명령을 실행해야 합니다.

### 작업자 노드 가입

이제 마스터 노드가 가동되어 실행 중이므로 작업자 노드를 클러스터에 추가할 수 있습니다. 작업자 노드는 컨테이너를 실행하는 데 사용되는 서버입니다.

클러스터에 작업자 노드를 추가하려면 kubeadm join 명령을 사용해야 합니다. 이 명령은 Kubernetes 클러스터에 서버를 추가합니다.

```
sudo kubeadm join 10.0.0.1:6443 --token ahc2xf.i0f4v9f0johtr5b4 --discovery-token-ca-cert-hash sha256:7ad1f8d3c908f3f558eaebf09abf8c3bdbbebfa7a7faebcbadea1a1a7fd0c74
```

## 클러스터 구성

이 섹션에서는 Kubernetes 클러스터를 구성하는 방법을 살펴보겠습니다.

### 마스터 노드 구성

가장 먼저 해야 할 일은 마스터 노드를 구성하는 것입니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
sudo kubectl apply -f https://git.io/weave-kube-1.6
```

이 명령은 서버에 포드 네트워크를 생성합니다. Pod 네트워크는 컨테이너를 연결하는 데 사용되는 네트워크입니다.

### 작업자 노드 구성

다음으로 작업자 노드를 구성해야 합니다. 각 작업자 노드에서 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
sudo kubectl apply -f https://git.io/weave-kube-1.6
```

이 명령은 서버에 포드 네트워크를 생성합니다. Pod 네트워크는 컨테이너를 연결하는 데 사용되는 네트워크입니다.

## 애플리케이션 배포

이 섹션에서는 애플리케이션을 Kubernetes 클러스터에 배포하는 방법을 살펴보겠습니다.

예제 디렉토리에 있는 nginx-deployment.yaml 파일을 사용할 것입니다. 이 파일에는 nginx 배포를 위한 구성이 포함되어 있습니다.

애플리케이션을 배포하려면 다음 명령을 실행해야 합니다.

```
kubectl apply -f examples/nginx-deployment.yaml
```

이 명령은 Kubernetes 클러스터에 배포를 생성합니다. 배포는 복제 세트 그룹입니다. 복제 세트는 포드 그룹입니다.

## 애플리케이션에 액세스하기

이 섹션에서는 배포한 애플리케이션에 액세스하는 방법을 살펴보겠습니다.

애플리케이션에 액세스하려면 인그레스 리소스를 생성해야 합니다. 인그레스 리소스는 트래픽을 애플리케이션으로 라우팅하는 데 사용되는 리소스입니다.

다음 명령을 실행하여 인그레스 리소스를 생성할 수 있습니다.

```
kubectl apply -f examples/nginx-ingress.yaml
```

이 명령은 Kubernetes 클러스터에 인그레스 리소스를 생성합니다.

인그레스 리소스가 생성되면 다음 URL로 이동하여 애플리케이션에 액세스할 수 있습니다.

http://<클러스터-ip>

## 클러스터 삭제

이 섹션에서는 Kubernetes 클러스터를 삭제하는 방법을 살펴보겠습니다.

클러스터를 삭제하려면 kubectl delete 명령을 사용해야 합니다. 이 명령은 클러스터의 모든 리소스를 삭제합니다.

```
kubectl delete -f examples/nginx-deployment.yaml
kubectl delete -f examples/nginx-ingress.yaml
```

## 결론

이 기사에서는 베어메탈 서버에 Kubernetes 클러스터를 배포하는 방법을 살펴보았습니다. 또한 클러스터에 애플리케이션을 배포하는 방법도 살펴보았습니다.