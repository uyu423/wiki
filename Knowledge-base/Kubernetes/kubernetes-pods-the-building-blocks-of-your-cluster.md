---
title: Kubernetes 포드: 클러스터의 빌딩 블록
description: 
published: true
date: 2023-02-17T18:05:33.541Z
tags: 
editor: markdown
dateCreated: 2023-01-30T14:32:40.133Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kubernetes Pods: The Building Blocks of Your Cluster***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-pods-the-building-blocks-of-your-cluster)
{.links-list}



# Kubernetes 포드: 클러스터의 빌딩 블록

Kubernetes 포드는 Kubernetes 클러스터에서 배포 가능한 가장 작은 단위이며 클러스터의 빌딩 블록입니다. 포드는 임시적이므로 지정된 시간에 실행된다는 보장이 없으며 필요에 따라 삭제하고 다시 만들 수 있습니다.

Pod는 Kubernetes 컨트롤 플레인에 의해 관리되며 사용자도 모르는 사이에 충돌 및 다시 시작될 수 있습니다. 이것이 Kubernetes 사용의 이점 중 하나입니다. 클러스터의 개별 시스템을 추상화하면 전체 클러스터를 단일 엔터티로 취급할 수 있습니다.

포드에는 하나 이상의 컨테이너가 포함되어 있으며 애플리케이션, 데이터베이스 또는 Kubernetes 클러스터에서 실행해야 하는 기타 항목을 호스팅하는 데 사용할 수 있습니다. Pod는 항상 동일한 노드에 배치되고 공동 예약되므로 볼륨 및 네트워크 인터페이스와 같은 리소스를 공유할 수 있습니다.

포드를 생성할 때 컨테이너 이미지 및 필요한 구성을 포함하여 포드에 대해 원하는 상태를 지정해야 합니다. 그런 다음 Kubernetes는 포드를 원하는 상태로 유지합니다.

Pod는 Kubernetes의 기본 배포 단위이며 일반적으로 상태 비저장 애플리케이션을 호스팅하는 데 사용됩니다. Kubernetes에서 상태 저장 애플리케이션을 실행해야 하는 경우 StatefulSet를 사용해야 합니다.

## 파드 생성

`kubectl` 명령줄 도구를 사용하여 포드를 만들거나 매니페스트 파일을 사용할 수 있습니다.

### `kubectl` 사용

`kubectl`을 사용하여 포드를 생성하려면 `run` 명령을 사용할 수 있습니다. 예를 들어 `nginx` 컨테이너 이미지를 실행할 포드를 생성하려면 다음 명령을 사용할 수 있습니다.

```
kubectl run nginx --image=nginx
```

그러면 단일 `nginx` 컨테이너가 있는 포드가 생성됩니다. 여러 컨테이너로 포드를 생성하려면 `run-container` 명령을 사용할 수 있습니다.

```
kubectl run-container nginx-container --image=nginx --image=mysql
```

### 매니페스트 파일 사용

또는 `Pod` 매니페스트 파일을 생성하고 `kubectl` `create` 명령을 사용하여 포드를 생성할 수 있습니다. 예를 들어 다음 매니페스트 파일은 단일 `nginx` 컨테이너가 있는 포드를 생성합니다.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx
```

그런 다음 다음 명령을 실행하여 포드를 생성할 수 있습니다.

```
kubectl create -f nginx.yaml
```

## 포드 삭제

포드는 `kubectl` `delete` 명령을 사용하여 삭제할 수 있습니다. 예를 들어 이전 섹션에서 생성한 `nginx` 포드를 삭제하려면 다음 명령을 사용할 수 있습니다.

```
kubectl delete pod nginx
```

## 포드 상태

포드는 다음 상태 중 하나일 수 있습니다.

- **Pending**: 포드가 생성되었지만 하나 이상의 컨테이너가 시작되지 않았습니다.
- **실행 중**: 포드와 모든 컨테이너가 실행 중입니다.
- **Succeeded**: Pod가 작업을 성공적으로 완료했으며 모든 컨테이너가 `Exited` 상태입니다.
- **Failed**: Pod가 실패했고 모든 컨테이너가 `Exited` 상태입니다.
- **알 수 없음**: 포드의 상태를 확인할 수 없습니다.

## 결론

Kubernetes 포드는 클러스터의 빌딩 블록이며 애플리케이션, 데이터베이스 또는 Kubernetes 클러스터에서 실행해야 하는 기타 항목을 호스팅하는 데 사용됩니다. Pod는 항상 동일한 노드에 배치되고 공동 예약되므로 볼륨 및 네트워크 인터페이스와 같은 리소스를 공유할 수 있습니다.

포드를 생성할 때 컨테이너 이미지 및 필요한 구성을 포함하여 포드에 대해 원하는 상태를 지정해야 합니다. 그런 다음 Kubernetes는 포드를 원하는 상태로 유지합니다.

Pod는 Kubernetes의 기본 배포 단위이며 일반적으로 상태 비저장 애플리케이션을 호스팅하는 데 사용됩니다. Kubernetes에서 상태 저장 애플리케이션을 실행해야 하는 경우 StatefulSet를 사용해야 합니다.