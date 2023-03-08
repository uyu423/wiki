---
title: CSI가 포함된 Kubernetes: 클러스터용 스토리지 관리
description: 
published: true
date: 2023-02-14T12:32:40.423Z
tags: 
editor: markdown
dateCreated: 2023-02-14T12:32:38.589Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes with CSI: Managing Storage for Your Clusters***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-csi-managing-storage-for-your-clusters)
{.links-list}


# CSI가 있는 쿠버네티스: 클러스터를 위한 스토리지 관리

CSI(컨테이너 스토리지 인터페이스)는 Kubernetes와 같은 컨테이너 오케스트레이션 솔루션에서 애플리케이션용 블록 스토리지를 프로비저닝하고 관리하는 데 사용하는 API 세트입니다. 쿠버네티스는 Google Cloud Storage와 같은 일부 스토리지 솔루션을 기본적으로 지원하지만 CSI를 사용하면 쿠버네티스가 더 넓은 범위의 스토리지 솔루션을 지원할 수 있습니다.

이 기사에서는 Kubernetes와 함께 CSI를 사용하여 클러스터의 스토리지를 관리하는 방법을 살펴보겠습니다. 또한 CSI 사용의 몇 가지 이점과 응용 프로그램의 스토리지를 보다 쉽게 관리하는 데 어떻게 도움이 되는지 알아봅니다.

## CSI란?

CSI(컨테이너 스토리지 인터페이스)는 Kubernetes와 같은 컨테이너 오케스트레이션 솔루션에서 애플리케이션용 블록 스토리지를 프로비저닝하고 관리하는 데 사용하는 API 세트입니다. 쿠버네티스는 Google Cloud Storage와 같은 일부 스토리지 솔루션을 기본적으로 지원하지만 CSI를 사용하면 쿠버네티스가 더 넓은 범위의 스토리지 솔루션을 지원할 수 있습니다.

CSI는 컨테이너용 스토리지를 프로비저닝하고 관리하는 데 사용할 수 있는 일련의 API를 제공합니다. 예를 들어 CSI를 사용하여 컨테이너용 스토리지 볼륨을 생성하거나 실행 중인 컨테이너에 연결하거나 실행 중인 컨테이너에서 분리할 수 있습니다. CSI를 사용하여 컨테이너의 스토리지 볼륨을 스냅샷하거나 스토리지 볼륨을 삭제할 수도 있습니다.

## 쿠버네티스와 함께 CSI를 사용하는 방법

쿠버네티스와 함께 CSI를 사용하는 것은 간단합니다. 먼저 각 Kubernetes 노드에 스토리지 솔루션용 CSI 드라이버를 설치해야 합니다. 다음으로 스토리지 솔루션에 대한 스토리지 클래스를 생성해야 합니다. 마지막으로 스토리지가 필요한 각 애플리케이션에 대해 PVC(영구 볼륨 클레임)를 생성해야 합니다.

CSI 드라이버 설치는 이 문서의 범위를 벗어나지만 스토리지 솔루션 설명서에서 이에 대한 지침을 찾을 수 있습니다.

CSI 드라이버가 설치되면 스토리지 솔루션에 대한 스토리지 클래스를 생성할 수 있습니다. 스토리지 클래스는 애플리케이션에 사용될 스토리지의 특성을 정의합니다. 예를 들어 스토리지 클래스는 스토리지 크기, 복제 팩터 및 성능 프로파일을 정의할 수 있습니다.

스토리지 클래스를 생성하려면 kubectl 명령줄 도구를 사용해야 합니다. 다음 명령은 "mystorage"라는 가상 스토리지 솔루션에 대한 스토리지 클래스를 생성합니다.

```
kubectl create storage-class mystorage \
--provisioner=csi.mystorage.com \
--parameters=size=1Gi,replicationFactor=3,performanceProfile=low
```

스토리지 클래스가 정의되면 스토리지가 필요한 각 애플리케이션에 대해 PVC를 작성할 수 있습니다. PVC는 특정 스토리지 클래스의 스토리지 요청입니다. 예를 들어 다음 PVC는 "mystorage" 스토리지 클래스에서 1GB의 스토리지를 요청합니다.

```
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: mystorage-pvc
  namespace: default
spec:
  storageClassName: mystorage
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

PVC를 생성하면 Kubernetes는 스토리지 클래스에서 스토리지 볼륨을 프로비저닝하고 이를 PVC에 바인딩합니다. 그런 다음 PVC를 사용하여 스토리지 볼륨을 컨테이너에 마운트할 수 있습니다.

## CSI 사용의 이점

Kubernetes와 함께 CSI를 사용하면 여러 가지 이점이 있습니다.

- **스토리지 관리 간소화**: Kubernetes와 함께 CSI를 사용하면 애플리케이션의 스토리지 관리를 간소화할 수 있습니다. 예를 들어 단일 스토리지 클래스를 사용하여 여러 애플리케이션에 대한 스토리지를 프로비저닝할 수 있습니다.

- **스토리지 솔루션 유연성 향상**: CSI를 통해 Kubernetes는 더 광범위한 스토리지 솔루션을 지원할 수 있습니다. 이는 Kubernetes에서 기본적으로 지원하지 않는 스토리지 솔루션을 사용하는 경우에 유용할 수 있습니다.

- **향상된 스토리지 솔루션 통합**: CSI는 Kubernetes와 스토리지 솔루션 간의 통합을 개선하는 데 도움이 될 수 있습니다. 예를 들어 일부 저장소 솔루션은 Kubernetes와 함께 사용할 수 있는 스냅샷 및 복제와 같은 추가 기능을 제공할 수 있습니다.

## 결론

이 기사에서는 CSI를 Kubernetes와 함께 사용하여 애플리케이션의 스토리지를 관리하는 방법을 살펴보았습니다. 또한 단순화된 스토리지 관리 및 향상된 스토리지 솔루션 유연성과 같은 CSI 사용의 이점에 대해서도 배웠습니다.