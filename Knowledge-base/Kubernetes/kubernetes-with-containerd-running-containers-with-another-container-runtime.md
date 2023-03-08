---
title: Containerd가 포함된 Kubernetes: 다른 컨테이너 런타임으로 컨테이너 실행
description: 
published: true
date: 2023-02-14T10:32:36.204Z
tags: 
editor: markdown
dateCreated: 2023-02-14T10:32:28.844Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes with Containerd: Running Containers with Another Container Runtime***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-containerd-running-containers-with-another-container-runtime)
{.links-list}


# Kubernetes with Containerd: 다른 컨테이너 런타임으로 컨테이너 실행

Kubernetes의 기본 컨테이너 런타임은 Docker이지만 Kubernetes는 다른 컨테이너 런타임과도 호환됩니다. 이 기사에서는 Containerd로 Kubernetes를 실행하는 방법을 살펴보겠습니다.

## Containerd를 사용하는 이유

Containerd는 단순성과 견고성으로 널리 알려진 업계 표준 컨테이너 런타임입니다. Docker Swarm 및 Apache Mesos와 같은 다른 컨테이너 오케스트레이션 플랫폼에서도 사용됩니다.

## 컨테이너 설치

Containerd를 설치하려면 apt 또는 yum과 같은 패키지 관리자를 사용할 수 있습니다.

```
sudo apt install containerd
```

## Containerd를 사용하도록 Kubernetes 구성

Containerd가 설치되면 이를 컨테이너 런타임으로 사용하도록 Kubernetes를 구성해야 합니다. 이렇게 하려면 `/etc/kubernetes/manifests/kubelet.yaml` 파일을 편집하고 다음 줄을 추가해야 합니다.

```
--container-runtime=containerd
```

또한 `/etc/systemd/system/kubelet.service.d/10-kubelet.conf` 파일을 편집하고 다음 행을 추가해야 합니다.

```
Environment="KUBELET_EXTRA_ARGS=--container-runtime=containerd"
```

이렇게 변경한 후에는 `kubelet` 서비스를 다시 시작해야 합니다.

```
sudo systemctl restart kubelet
```

## 컨테이너 만들기

이제 Kubernetes가 Containerd를 사용하도록 구성되었으므로 컨테이너를 생성해 보겠습니다.

먼저 다음 내용으로 `container.json`이라는 파일을 만들어야 합니다.

```json
{
  "id": "container1",
  "runtime": "containerd",
  "image": "nginx:latest"
}
```

다음으로 `ctr` 명령을 사용하여 컨테이너를 생성해야 합니다.

```
sudo ctr create -f container.json
```

## 컨테이너 실행

이제 컨테이너를 만들었으니 실행해 봅시다.

먼저 다음 내용으로 `run.json`이라는 파일을 만들어야 합니다.

```json
{
  "id": "container1",
  "runtime": "containerd",
  "image": "nginx:latest",
  "command": ["nginx", "-g", "daemon off;"]
}
```

다음으로 `ctr` 명령을 사용하여 컨테이너를 실행해야 합니다.

```
sudo ctr run -f run.json
```

## 컨테이너 삭제

컨테이너를 삭제하려면 `ctr` 명령을 사용할 수 있습니다.

```
sudo ctr delete container1
```

## 결론

이 기사에서는 Kubernetes를 Containerd와 함께 사용하는 방법을 살펴보았습니다. 또한 Containerd를 설치하는 방법, 이를 사용하도록 Kubernetes를 구성하는 방법, 컨테이너를 만들고 실행하는 방법도 살펴보았습니다.