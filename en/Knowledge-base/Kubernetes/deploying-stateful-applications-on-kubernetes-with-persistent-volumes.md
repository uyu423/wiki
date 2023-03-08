---
title: Deploying Stateful Applications on Kubernetes with Persistent Volumes
description: 
published: true
date: 2023-01-31T14:43:55.426Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:43:51.910Z
---

- [영구 볼륨을 사용하여 Kubernetes에 상태 저장 애플리케이션 배포***Korean** version of this document is available*](/ko/Knowledge-base/Kubernetes/deploying-stateful-applications-on-kubernetes-with-persistent-volumes)
{.links-list}
- [永続ボリュームを使用して Kubernetes にステートフル アプリケーションをデプロイする***Japanese** version of this document is available*](/ja/Knowledge-base/Kubernetes/deploying-stateful-applications-on-kubernetes-with-persistent-volumes)
{.links-list}
- [使用持久卷在 Kubernetes 上部署有状态应用程序***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kubernetes/deploying-stateful-applications-on-kubernetes-with-persistent-volumes)
{.links-list}



# Deploying Stateful Applications on Kubernetes with Persistent Volumes

Kubernetes is a powerful container orchestration tool that enables developers to deploy and manage containerized applications at scale. One of the key features of Kubernetes is its ability to provide persistent storage for stateful applications. This is essential for applications that require data to be persisted across failures or restarts, such as databases.

In this article, we'll take a look at how to deploy stateful applications on Kubernetes with persistent volumes. We'll cover the following topics:

- What are persistent volumes and why are they important?
- How to create and attach a persistent volume to a Kubernetes pod
- How to use persistent volumes with stateful applications

## What are persistent volumes and why are they important?

A persistent volume (PV) is a block device that is used to store data for a Kubernetes pod. When a pod is deleted, the data on the PV is not deleted and can be reused by another pod. This makes PV's ideal for storing data for stateful applications, such as databases.

PV's are important because they allow data to be persisted across failures or restarts. This is essential for applications that require data to be persisted, such as databases. PV's also allow data to be shared between multiple pods, which can be useful for applications that require data to be synchronized across multiple instances.

## How to create and attach a persistent volume to a Kubernetes pod

Creating a PV is a two-step process. First, you need to create a PV object using the kubectl command-line tool. This object defines the parameters of the PV, such as the size and type of storage. Second, you need to create a PVC object that defines how the PV will be used by a pod.

The following example creates a PV with 1 GB of storage:

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

The next example creates a PVC that uses the PV created in the previous example:

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

The PVC can then be used to create a pod that uses the PV:

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

## How to use persistent volumes with stateful applications

Stateful applications, such as databases, can be deployed on Kubernetes using persistent volumes. The following example shows how to deploy a MySQL database on Kubernetes using a PV:

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

In the example above, we created a PV with 1 GB of storage and a PVC that uses the PV. We then created a pod that contains a MySQL container and mounts the PV at /var/lib/mysql.

The MySQL container will use the PV to store data. If the pod is deleted, the data on the PV will not be deleted and can be reused by another pod. This makes PV's ideal for storing data for stateful applications, such as databases.

## Conclusion

In this article, we've looked at how to deploy stateful applications on Kubernetes with persistent volumes. We've seen how PV's can be used to store data for stateful applications and how to use PV's with stateful applications.