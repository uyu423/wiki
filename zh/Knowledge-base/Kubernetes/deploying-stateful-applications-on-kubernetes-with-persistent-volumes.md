---
title: 使用持久卷在 Kubernetes 上部署有状态应用程序
description: 
published: true
date: 2023-01-31T14:43:53.471Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:43:51.919Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Deploying Stateful Applications on Kubernetes with Persistent Volumes***English** version of this document is available*](/en/Knowledge-base/Kubernetes/deploying-stateful-applications-on-kubernetes-with-persistent-volumes)
{.links-list}



# 使用持久卷在 Kubernetes 上部署有状态应用程序

Kubernetes 是一个强大的容器编排工具，使开发人员能够大规模部署和管理容器化应用程序。 Kubernetes 的关键特性之一是它能够为有状态应用程序提供持久存储。这对于需要在发生故障或重启时保留数据的应用程序（例如数据库）来说是必不可少的。

在本文中，我们将了解如何在具有持久卷的 Kubernetes 上部署有状态应用程序。我们将涵盖以下主题：

- 什么是持久卷，为什么它们很重要？
- 如何创建持久卷并将其附加到 Kubernetes pod
- 如何在有状态应用程序中使用持久卷

## 什么是持久卷，为什么它们很重要？

持久卷 (PV) 是用于存储 Kubernetes pod 数据的块设备。当一个pod被删除时，PV上的数据并没有被删除，可以被另一个pod复用。这使得 PV 非常适合为有状态应用程序（例如数据库）存储数据。

PV 很重要，因为它们允许数据在故障或重新启动时保持不变。这对于需要持久保存数据的应用程序（例如数据库）来说是必不可少的。 PV 还允许在多个 pod 之间共享数据，这对于需要跨多个实例同步数据的应用程序非常有用。

## 如何创建持久卷并将其附加到 Kubernetes pod

创建 PV 是一个两步过程。首先，您需要使用 kubectl 命令行工具创建一个 PV 对象。该对象定义了 PV 的参数，例如存储的大小和类型。其次，您需要创建一个 PVC 对象来定义 Pod 如何使用 PV。

以下示例创建一个具有 1 GB 存储空间的 PV：

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

下一个示例创建一个 PVC，它使用在上一个示例中创建的 PV：

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

然后可以使用 PVC 创建使用 PV 的 pod：

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

## 如何在有状态应用程序中使用持久卷

可以使用持久卷将有状态的应用程序（例如数据库）部署在 Kubernetes 上。以下示例展示了如何使用 PV 在 Kubernetes 上部署 MySQL 数据库：

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

在上面的示例中，我们创建了一个具有 1 GB 存储空间的 PV 和一个使用该 PV 的 PVC。然后我们创建了一个包含 MySQL 容器的 pod，并将 PV 挂载在 /var/lib/mysql。

MySQL 容器将使用 PV 来存储数据。如果删除pod，PV上的数据不会被删除，可以被其他pod复用。这使得 PV 非常适合为有状态应用程序（例如数据库）存储数据。

## 结论

在本文中，我们研究了如何在具有持久卷的 Kubernetes 上部署有状态应用程序。我们已经了解了如何使用 PV 来存储有状态应用程序的数据以及如何将 PV 用于有状态应用程序。