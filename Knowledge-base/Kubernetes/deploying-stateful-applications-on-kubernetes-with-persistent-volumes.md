---
title: 영구 볼륨을 사용하여 Kubernetes에 상태 저장 애플리케이션 배포
description: 
published: true
date: 2023-01-31T14:43:53.514Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:43:51.913Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Deploying Stateful Applications on Kubernetes with Persistent Volumes***English** version of this document is available*](/en/Knowledge-base/Kubernetes/deploying-stateful-applications-on-kubernetes-with-persistent-volumes)
{.links-list}



# 영구 볼륨을 사용하여 Kubernetes에 상태 저장 애플리케이션 배포

Kubernetes는 개발자가 컨테이너화된 애플리케이션을 대규모로 배포하고 관리할 수 있도록 하는 강력한 컨테이너 오케스트레이션 도구입니다. Kubernetes의 주요 기능 중 하나는 상태 저장 애플리케이션을 위한 영구 스토리지를 제공하는 기능입니다. 이는 데이터베이스와 같이 장애가 발생하거나 다시 시작해도 데이터가 지속되어야 하는 애플리케이션에 필수적입니다.

이 기사에서는 영구 볼륨이 있는 Kubernetes에 상태 저장 애플리케이션을 배포하는 방법을 살펴보겠습니다. 다음 주제를 다룹니다.

- 영구 볼륨이란 무엇이며 중요한 이유는 무엇입니까?
- 영구 볼륨을 생성하고 Kubernetes 포드에 연결하는 방법
- 상태 저장 애플리케이션에서 영구 볼륨을 사용하는 방법

## 영구 볼륨이란 무엇이며 왜 중요한가요?

PV(영구 볼륨)는 Kubernetes 포드의 데이터를 저장하는 데 사용되는 블록 장치입니다. 포드가 삭제되더라도 PV의 데이터는 삭제되지 않으며 다른 포드에서 재사용할 수 있습니다. 따라서 PV는 데이터베이스와 같은 상태 저장 애플리케이션용 데이터를 저장하는 데 이상적입니다.

PV는 실패 또는 재시작 후에도 데이터를 유지할 수 있기 때문에 중요합니다. 이는 데이터베이스와 같이 데이터가 지속되어야 하는 애플리케이션에 필수적입니다. PV는 또한 여러 팟(Pod) 간에 데이터를 공유할 수 있도록 하므로 여러 인스턴스 간에 데이터를 동기화해야 하는 애플리케이션에 유용할 수 있습니다.

## 영구 볼륨을 생성하고 Kubernetes 포드에 연결하는 방법

PV 생성은 2단계 프로세스입니다. 먼저 kubectl 명령줄 도구를 사용하여 PV 객체를 생성해야 합니다. 이 객체는 스토리지의 크기 및 유형과 같은 PV의 매개변수를 정의합니다. 둘째, Pod에서 PV를 사용하는 방법을 정의하는 PVC 객체를 생성해야 합니다.

다음 예에서는 스토리지가 1GB인 PV를 생성합니다.

```
kubectl create -f pv.yaml
```

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-1
  labels:
    type: local
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/tmp/data"
```

다음 예에서는 이전 예에서 만든 PV를 사용하는 PVC를 만듭니다.

```
kubectl create -f pvc.yaml
```

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-1
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  selector:
    matchLabels:
      type: local
```

그런 다음 PVC를 사용하여 PV를 사용하는 포드를 만들 수 있습니다.

```
kubectl create -f pod.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-1
spec:
  containers:
  - name: container-1
    image: busybox
    command: ["sleep", "3600"]
    volumeMounts:
    - name: pv-1
      mountPath: "/data"
  volumes:
  - name: pv-1
    persistentVolumeClaim:
      claimName: pvc-1
```

## 상태 저장 애플리케이션에서 영구 볼륨을 사용하는 방법

데이터베이스와 같은 상태 저장 애플리케이션은 영구 볼륨을 사용하여 Kubernetes에 배포할 수 있습니다. 다음 예는 PV를 사용하여 Kubernetes에 MySQL 데이터베이스를 배포하는 방법을 보여줍니다.

```
kubectl create -f mysql-pv.yaml
```

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql-pv-1
  labels:
    type: local
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/tmp/data"
```

```
kubectl create -f mysql-pvc.yaml
```

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pvc-1
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  selector:
    matchLabels:
      type: local
```

```
kubectl create -f mysql-pod.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mysql-pod-1
spec:
  containers:
  - name: mysql-container-1
    image: mysql:5.6
    env:
    - name: MYSQL_ROOT_PASSWORD
      value: "secret"
    - name: MYSQL_USER
      value: "user"
    - name: MYSQL_PASSWORD
      value: "secret"
    - name: MYSQL_DATABASE
      value: "db"
    ports:
    - containerPort: 3306
      name: mysql
    volumeMounts:
    - name: mysql-data
      mountPath: /var/lib/mysql
  volumes:
  - name: mysql-data
    persistentVolumeClaim:
      claimName: mysql-pvc-1
```

위의 예에서는 1GB의 스토리지가 있는 PV와 PV를 사용하는 PVC를 생성했습니다. 그런 다음 MySQL 컨테이너를 포함하고 PV를 /var/lib/mysql에 마운트하는 포드를 생성했습니다.

MySQL 컨테이너는 PV를 사용하여 데이터를 저장합니다. 포드가 삭제되더라도 PV의 데이터는 삭제되지 않고 다른 포드에서 재사용할 수 있습니다. 따라서 PV는 데이터베이스와 같은 상태 저장 애플리케이션용 데이터를 저장하는 데 이상적입니다.

## 결론

이 기사에서는 영구 볼륨이 있는 Kubernetes에 상태 저장 애플리케이션을 배포하는 방법을 살펴보았습니다. PV를 사용하여 상태 저장 응용 프로그램의 데이터를 저장하는 방법과 상태 저장 응용 프로그램에서 PV를 사용하는 방법을 살펴보았습니다.