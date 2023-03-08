---
title: Kubernetes 웹 UI: 대시보드로 클러스터 관리
description: 
published: true
date: 2023-02-14T02:32:33.112Z
tags: 
editor: markdown
dateCreated: 2023-02-14T02:32:25.888Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes Web UI: Managing Your Cluster with the Dashboard***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-web-ui-managing-your-cluster-with-the-dashboard)
{.links-list}


# Kubernetes 웹 UI: 대시보드로 클러스터 관리

Kubernetes는 애플리케이션과 리소스를 대규모로 관리하는 데 도움이 되는 강력한 컨테이너 오케스트레이션 도구입니다. Kubernetes 대시보드는 Kubernetes 클러스터를 관리하는 데 도움이 되는 웹 기반 UI입니다. 이 기사에서는 대시보드를 사용하여 클러스터를 관리하는 방법을 살펴보겠습니다.

## 대시보드에 액세스하기

대시보드에 액세스하려면 Kubernetes 클러스터가 실행 중이어야 합니다. Kubernetes 설명서의 지침에 따라 [로컬 클러스터 설정](https://kubernetes.io/docs/setup/learning-environment/minikube/)할 수 있습니다.

클러스터를 가동하고 실행하면 다음 명령을 실행하여 대시보드에 액세스할 수 있습니다.

```
kubectl proxy
```

이렇게 하면 Kubernetes API 서버에 대한 프록시가 시작되고 http://localhost:8001/api/v1/namespaces/kube-system/services/kubernetes-dashboard:/proxy/에서 대시보드를 사용할 수 있습니다.

## 쿠버네티스 클러스터 만들기

Kubernetes 클러스터를 생성하려면 실행 중인 Kubernetes 클러스터가 있어야 합니다. Kubernetes 설명서의 지침에 따라 [로컬 클러스터 설정](https://kubernetes.io/docs/setup/learning-environment/minikube/)할 수 있습니다.

Kubernetes 클러스터를 시작하고 실행하면 다음 명령을 실행하여 새 클러스터를 만들 수 있습니다.

```
kubectl create cluster my-cluster
```

다음 명령을 실행하여 클러스터가 생성되었는지 확인할 수 있습니다.

```
kubectl get clusters
```

## Kubernetes 클러스터 삭제

Kubernetes 클러스터를 삭제하려면 실행 중인 Kubernetes 클러스터가 있어야 합니다. Kubernetes 설명서의 지침에 따라 [로컬 클러스터 설정](https://kubernetes.io/docs/setup/learning-environment/minikube/)할 수 있습니다.

Kubernetes 클러스터가 실행 중이면 다음 명령을 실행하여 클러스터를 삭제할 수 있습니다.

```
kubectl delete cluster my-cluster
```

다음 명령을 실행하여 클러스터가 삭제되었는지 확인할 수 있습니다.

```
kubectl get clusters
```

## 노드 관리

Kubernetes 대시보드는 Kubernetes 클러스터의 노드를 관리하는 데 사용할 수 있습니다. 클러스터의 노드 목록을 보려면 왼쪽 탐색에서 "노드" 링크를 클릭하십시오. 클러스터의 모든 노드를 나열하는 페이지가 열립니다.

이 페이지에서 IP 주소, 운영 체제 및 커널 버전과 같은 각 노드에 대한 정보를 볼 수 있습니다. 노드를 삭제하거나 확장 또는 축소하는 등의 작업을 노드에서 수행할 수도 있습니다.

## 포드 관리

Kubernetes 대시보드는 Kubernetes 클러스터에서 포드를 관리하는 데 사용할 수 있습니다. 클러스터의 포드 목록을 보려면 왼쪽 탐색에서 "Pods" 링크를 클릭하십시오. 그러면 클러스터의 모든 포드를 나열하는 페이지가 열립니다.

이 페이지에서 IP 주소 및 실행 중인 노드와 같은 각 포드에 대한 정보를 볼 수 있습니다. 포드를 삭제하거나 확장 또는 축소하는 등의 작업을 포드에서 수행할 수도 있습니다.

## 배포 관리

Kubernetes 대시보드는 Kubernetes 클러스터에서 배포를 관리하는 데 사용할 수 있습니다. 클러스터의 배포 목록을 보려면 왼쪽 탐색에서 "배포" 링크를 클릭하십시오. 그러면 클러스터의 모든 배포를 나열하는 페이지가 열립니다.

이 페이지에서 배포의 일부인 복제본 및 포드 수와 같은 각 배포에 대한 정보를 볼 수 있습니다. 확장 또는 축소와 같은 배포 작업을 수행할 수도 있습니다.

## 서비스 관리

Kubernetes 대시보드는 Kubernetes 클러스터에서 서비스를 관리하는 데 사용할 수 있습니다. 클러스터의 서비스 목록을 보려면 왼쪽 탐색 메뉴에서 "서비스" 링크를 클릭하십시오. 그러면 클러스터의 모든 서비스를 나열하는 페이지가 열립니다.

이 페이지에서 서비스 유형 및 서비스의 일부인 팟(Pod)과 같은 각 서비스에 대한 정보를 볼 수 있습니다. 서비스 편집 또는 삭제와 같은 서비스 작업을 수행할 수도 있습니다.

## 결론

이 기사에서는 Kubernetes 대시보드를 사용하여 Kubernetes 클러스터를 관리하는 방법을 살펴보았습니다. 클러스터 생성 및 삭제 방법, 노드 및 포드 관리 방법, 배포 및 서비스 관리 방법을 살펴보았습니다.