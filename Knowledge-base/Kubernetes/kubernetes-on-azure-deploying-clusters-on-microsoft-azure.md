---
title: Azure의 Kubernetes: Microsoft Azure에 클러스터 배포
description: 
published: true
date: 2023-02-01T16:18:02.250Z
tags: 
editor: markdown
dateCreated: 2023-02-01T16:17:58.195Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Kubernetes on Azure: Deploying Clusters on Microsoft Azure***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-azure-deploying-clusters-on-microsoft-azure)
{.links-list}


# Azure의 Kubernetes: Microsoft Azure에 클러스터 배포

Kubernetes는 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하기 위한 오픈 소스 시스템입니다. 애플리케이션을 구성하는 컨테이너를 논리 단위로 그룹화하여 쉽게 관리하고 검색할 수 있습니다. Microsoft Azure는 AKS(Azure Kubernetes Service)라는 관리형 Kubernetes 서비스를 제공하여 Azure에서 생산 준비가 된 Kubernetes 클러스터를 빠르고 쉽게 배포할 수 있습니다.

이 문서에서는 AKS를 사용하여 Azure에 Kubernetes 클러스터를 배포하는 방법을 보여줍니다. 또한 간단한 애플리케이션을 클러스터에 배포하고 인터넷에 노출하는 방법도 보여줍니다.

## 전제 조건

시작하기 전에 다음이 필요합니다.

- Azure 계정. 없는 경우 무료 평가판에 등록할 수 있습니다.
- 로컬 컴퓨터에 설치된 Azure CLI.
- kubectl 명령줄 도구.

## AKS 클러스터 만들기

첫 번째 단계는 Azure CLI를 사용하여 AKS 클러스터를 만드는 것입니다. az aks create 명령을 사용하여 리소스 그룹, AKS 클러스터를 만들고 kubeconfig 파일을 생성합니다. kubeconfig 파일은 kubectl 도구에서 Kubernetes 클러스터에 연결하는 데 사용됩니다.

다음 명령을 실행하여 AKS 클러스터를 만듭니다.

```
az aks create \
  --resource-group myResourceGroup \
  --name myAKSCluster \
  --node-count 3 \
  --generate-ssh-keys
```

AKS 클러스터를 만드는 데 몇 분 정도 걸립니다. 준비가 되면 kubectl 도구를 사용하여 클러스터에 연결할 수 있습니다.

## 클러스터에 연결

AKS 클러스터에 연결하려면 Azure에서 클러스터 자격 증명을 검색하고 이를 사용하도록 kubectl을 구성해야 합니다.

다음 명령을 실행하여 자격 증명을 검색합니다.

```
az aks get-credentials \
  --resource-group myResourceGroup \
  --name myAKSCluster
```

이렇게 하면 kubeconfig 파일이 다운로드되고 컴퓨터의 기존 kubeconfig 파일과 병합됩니다.

이제 kubectl 도구를 사용하여 AKS 클러스터와 상호 작용할 수 있습니다. 다음 명령을 실행하여 클러스터의 노드 목록을 가져옵니다.

```
kubectl get nodes
```

## 애플리케이션 배포

이제 작동하는 Kubernetes 클러스터가 있으므로 여기에 애플리케이션을 배포할 수 있습니다. 이 예에서는 Node.js로 작성된 간단한 웹 애플리케이션을 배포합니다.

먼저 애플리케이션의 Docker 이미지를 생성해야 합니다. 프로젝트의 루트 디렉터리에 있는 Dockerfile을 사용하여 이미지를 빌드합니다. 다음 명령을 실행하여 이미지를 빌드합니다.

```
docker build -t my-app:v1 .
```

이미지가 빌드되면 Docker 레지스트리에 푸시할 수 있습니다. 이 예에서는 ACR(Azure Container Registry)로 푸시합니다.

먼저 ACR 인스턴스를 생성해야 합니다. 이를 위해 az acr create 명령을 사용할 수 있습니다. 다음 명령을 실행하여 ACR 인스턴스를 만듭니다.

```
az acr create \
  --resource-group myResourceGroup \
  --name myACR \
  --sku Basic
```

ACR 인스턴스가 생성되면 Docker 이미지를 여기에 푸시할 수 있습니다. 다음 명령을 실행하여 이미지를 푸시합니다.

```
docker push myacr.azurecr.io/my-app:v1
```

이제 이미지가 ACR로 푸시되었으므로 AKS 클러스터에 배포할 수 있습니다. 이를 위해 Kubernetes 배포를 사용합니다. 배포는 Pod의 복제본 집합을 관리하는 리소스입니다. Pod는 Kubernetes에서 배포의 기본 단위입니다. 동일한 호스트에 함께 배포되는 하나 이상의 컨테이너 그룹입니다.

kubectl 도구를 사용하여 배포를 생성합니다. 다음 명령어를 실행하여 배포를 만듭니다.

```
kubectl create deployment my-app --image=myacr.azurecr.io/my-app:v1
```

이렇게 하면 팟(Pod)의 복제 세트를 관리할 my-app이라는 배치가 생성됩니다. 포드는 ACR에 푸시한 my-app:v1 이미지에서 생성됩니다.

kubectl get deployments 명령을 사용하여 방금 생성한 배포를 볼 수 있습니다.

```
kubectl get deployments
```

kubectl get pods 명령을 사용하여 배포에서 관리하는 포드를 볼 수도 있습니다.

```
kubectl get pods
```

## 애플리케이션 노출

이제 애플리케이션이 배포되었으므로 사용자가 액세스할 수 있도록 애플리케이션을 인터넷에 노출해야 합니다. Kubernetes 서비스를 생성하여 이를 수행할 수 있습니다. 서비스는 Pod의 논리적 집합과 이에 액세스하는 정책을 정의하는 추상화입니다.

LoadBalancer 유형의 서비스를 생성합니다. 이렇게 하면 Azure에서 부하 분산 장치가 생성되고 my-app 배포에서 관리하는 포드에 매핑됩니다.

다음 명령을 실행하여 서비스를 생성합니다.

```
kubectl expose deployment my-app --type=LoadBalancer --port=80 --target-port=8080
```

이렇게 하면 로드 밸런서에서 포트 80을 노출하는 my-app이라는 서비스가 생성됩니다. 이 포트에 대한 트래픽은 my-app 배치에서 관리하는 팟(Pod)의 포트 8080으로 전달됩니다.

kubectl get services 명령을 사용하여 방금 생성한 서비스를 볼 수 있습니다.

```
kubectl get services
```

서비스가 생성되면 로드 밸런서가 프로비저닝되고 서비스에 공용 IP 주소가 할당되는 데 몇 분 정도 걸립니다. kubectl get services 명령을 사용하여 서비스 상태를 볼 수 있습니다.

```
kubectl get services
```

서비스가 생성되면 공인 IP 주소를 사용하여 웹 브라우저에서 애플리케이션에 액세스할 수 있습니다.

## 클러스터 삭제

AKS 클러스터가 더 이상 필요하지 않으면 이를 삭제하여 요금 발생을 중지할 수 있습니다. 클러스터를 삭제하려면 다음 명령어를 실행합니다.

```
az aks delete \
  --resource-group myResourceGroup \
  --name myAKSCluster
```

## 결론

이 문서에서는 AKS를 사용하여 Azure에 Kubernetes 클러스터를 배포하는 방법을 보여 주었습니다. 또한 간단한 애플리케이션을 클러스터에 배포하고 인터넷에 노출하는 방법도 보여 주었습니다.