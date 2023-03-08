---
title: CRI-O가 포함된 Kubernetes: 대체 컨테이너 런타임으로 컨테이너 실행
description: 
published: true
date: 2023-02-14T09:32:29.308Z
tags: 
editor: markdown
dateCreated: 2023-02-14T09:32:22.070Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes with CRI-O: Running Containers with an Alternative Container Runtime***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-cri-o-running-containers-with-an-alternative-container-runtime)
{.links-list}


# CRI-O가 포함된 Kubernetes: 대체 컨테이너 런타임으로 컨테이너 실행

## 크리오란?

CRI-O는 Kubernetes를 위한 대체 컨테이너 런타임입니다. 가볍고 최소한의 공간을 차지하도록 설계되어 Kubernetes에서 컨테이너를 실행하는 데 이상적입니다. CRI-O는 OCI(Open Containers Initiative) 런타임 사양을 사용하며 Kubernetes CRI(Container Runtime Interface)와 호환됩니다.

## 쿠버네티스와 함께 CRI-O를 사용하는 이유는 무엇입니까?

Kubernetes에서 CRI-O를 사용하려는 몇 가지 이유가 있습니다.

- CRI-O는 가볍고 최소한의 공간을 차지하도록 설계되었습니다. 따라서 Kubernetes에서 컨테이너를 실행하는 데 이상적입니다.
- CRI-O는 OCI(Open Containers Initiative) 런타임 사양을 사용합니다. 이는 Kubernetes CRI(Container Runtime Interface)와 호환됨을 의미합니다.
- CRI-O는 Kubernetes 컨테이너 네트워크 인터페이스(CNI) 플러그인과 통합됩니다. 이를 통해 Kubernetes에서 실행되는 컨테이너에 대한 네트워킹을 쉽게 설정할 수 있습니다.

## Kubernetes에서 CRI-O를 사용하는 방법

쿠버네티스와 함께 CRI-O를 사용하는 것은 쉽습니다. CRI-O 컨테이너 런타임을 직접 사용하거나 CRI-O Kubernetes 통합을 사용할 수 있습니다.

### CRI-O 컨테이너 런타임 직접 사용

CRI-O 컨테이너 런타임을 직접 사용하려면 Kubernetes `kubelet`을 시작할 때 `--runtime` 플래그를 설정해야 합니다.

```
$ kubelet --runtime=cri-o
```

### CRI-O Kubernetes 통합 사용

CRI-O Kubernetes 통합을 사용하려면 Kubernetes `kubelet`을 시작할 때 `--container-runtime` 플래그를 설정해야 합니다.

```
$ kubelet --container-runtime=cri-o
```

또한 CRI-O Kubernetes 통합을 활성화하려면 `--feature-gates` 플래그를 설정해야 합니다.

```
$ kubelet --feature-gates=CRIO=true
```

## 결론

CRI-O는 Kubernetes를 위한 훌륭한 대체 컨테이너 런타임입니다. 가볍고 최소한의 공간을 차지하도록 설계되어 Kubernetes에서 컨테이너를 실행하는 데 이상적입니다. CRI-O는 OCI(Open Containers Initiative) 런타임 사양을 사용하며 Kubernetes CRI(Container Runtime Interface)와 호환됩니다. CRI-O는 Kubernetes 컨테이너 네트워크 인터페이스(CNI) 플러그인과도 통합됩니다. 이를 통해 Kubernetes에서 실행되는 컨테이너에 대한 네트워킹을 쉽게 설정할 수 있습니다.