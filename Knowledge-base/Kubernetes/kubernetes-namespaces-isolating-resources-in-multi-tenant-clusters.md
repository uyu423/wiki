---
title: Kubernetes 네임스페이스: 다중 테넌트 클러스터에서 리소스 격리
description: 
published: true
date: 2023-02-08T23:32:19.082Z
tags: 
editor: markdown
dateCreated: 2023-02-08T23:32:17.374Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes Namespaces: Isolating Resources in Multi-Tenant Clusters***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-namespaces-isolating-resources-in-multi-tenant-clusters)
{.links-list}


# Kubernetes 네임스페이스: 다중 테넌트 클러스터에서 리소스 격리

Kubernetes 네임스페이스는 공유 클러스터에서 리소스를 격리하는 간단하지만 강력한 방법을 제공합니다. 각 테넌트에 대해 별도의 네임스페이스를 생성하여 어떤 사용자가 어떤 리소스에 액세스할 수 있는지 제어하고 테넌트 간 리소스 가시성을 제한할 수 있습니다.

## 네임스페이스 생성

`kubectl create namespace` 명령을 실행하여 네임스페이스를 생성할 수 있습니다. 예를 들어 'acme'라는 테넌트의 네임스페이스를 만들려면 다음을 실행합니다.

```
kubectl create namespace acme
```

## 네임스페이스에 리소스 할당

네임스페이스가 생성되면 `kubectl` 명령과 함께 `--namespace` 플래그를 사용하여 리소스를 할당할 수 있습니다. 예를 들어 `acme` 네임스페이스에 포드를 생성하려면 다음을 실행합니다.

```
kubectl create pod --namespace acme ...
```

## 네임스페이스에서 리소스 보기

기본적으로 `kubectl` 명령은 `default` 네임스페이스의 리소스만 표시합니다. 다른 네임스페이스의 리소스를 보려면 `kubectl get` 명령과 함께 `--namespace` 플래그를 사용할 수 있습니다. 예를 들어 `acme` 네임스페이스의 모든 포드를 보려면 다음을 실행합니다.

```
kubectl get pods --namespace acme
```

## 네임스페이스 간 전환

특정 네임스페이스에서 명령을 자주 실행하는 경우 `kubectl config set-context` 명령을 사용하여 네임스페이스 간에 전환할 수 있습니다. 예를 들어 `acme` 네임스페이스로 전환하려면 다음을 실행합니다.

```
kubectl config set-context $(kubectl config current-context) --namespace=acme
```

## 네임스페이스 삭제

`kubectl delete namespace` 명령을 실행하여 네임스페이스를 삭제할 수 있습니다. 예를 들어 `acme` 네임스페이스를 삭제하려면 다음을 실행합니다.

```
kubectl delete namespace acme
```

## 결론

Kubernetes 네임스페이스는 공유 클러스터에서 리소스를 격리하는 간단하지만 강력한 방법을 제공합니다. 각 테넌트에 대해 별도의 네임스페이스를 생성하여 어떤 사용자가 어떤 리소스에 액세스할 수 있는지 제어하고 테넌트 간 리소스 가시성을 제한할 수 있습니다.