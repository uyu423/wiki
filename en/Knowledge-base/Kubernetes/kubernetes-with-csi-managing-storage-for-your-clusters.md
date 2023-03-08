---
title: Kubernetes with CSI: Managing Storage for Your Clusters
description: 
published: true
date: 2023-02-14T12:32:46.112Z
tags: 
editor: markdown
dateCreated: 2023-02-14T12:32:38.597Z
---

- [Kubernetes con CSI: administración de almacenamiento para sus clústeres***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-with-csi-managing-storage-for-your-clusters)
{.links-list}
- [带有 CSI 的 Kubernetes：管理集群的存储***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-with-csi-managing-storage-for-your-clusters)
{.links-list}
- [CSI가 포함된 Kubernetes: 클러스터용 스토리지 관리***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-with-csi-managing-storage-for-your-clusters)
{.links-list}


# Kubernetes with CSI: Managing Storage for Your Clusters

Container storage interface (CSI) is a set of APIs used by container orchestration solutions, such as Kubernetes, to provision and manage block storage for their applications. While Kubernetes has built-in support for some storage solutions, such as Google Cloud Storage, using CSI allows Kubernetes to support a wider range of storage solutions.

In this article, we'll take a look at how to use CSI with Kubernetes to manage storage for your clusters. We'll also learn about some of the benefits of using CSI and how it can help you more easily manage storage for your applications.

## What is CSI?

Container storage interface (CSI) is a set of APIs used by container orchestration solutions, such as Kubernetes, to provision and manage block storage for their applications. While Kubernetes has built-in support for some storage solutions, such as Google Cloud Storage, using CSI allows Kubernetes to support a wider range of storage solutions.

CSI provides a set of APIs that can be used to provision and manage storage for containers. For example, you can use CSI to create a storage volume for a container, attach it to a running container, or detach it from a running container. You can also use CSI to snapshot a container's storage volume or delete a storage volume.

## How to use CSI with Kubernetes

Using CSI with Kubernetes is simple. First, you'll need to install the CSI driver for your storage solution on each of your Kubernetes nodes. Next, you'll need to create a storage class for your storage solution. Finally, you'll need to create a Persistent Volume Claim (PVC) for each of your applications that require storage.

Installing the CSI driver is beyond the scope of this article, but you can find instructions for doing so in the documentation for your storage solution.

Once you have the CSI driver installed, you can create a storage class for your storage solution. A storage class defines the characteristics of the storage that will be used for your applications. For example, a storage class can define the size of the storage, the replication factor, and the performance profile.

To create a storage class, you'll need to use the kubectl command-line tool. The following command will create a storage class for a hypothetical storage solution called "mystorage":

```
kubectl create storage-class mystorage \
--provisioner=csi.mystorage.com \
--parameters=size=1Gi,replicationFactor=3,performanceProfile=low
```

Once you have a storage class defined, you can create a PVC for each of your applications that require storage. A PVC is a request for storage from a particular storage class. For example, the following PVC requests one gigabyte of storage from the "mystorage" storage class:

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

When you create a PVC, Kubernetes will provision a storage volume from the storage class and bind it to the PVC. You can then use the PVC to mount the storage volume to a container.

## Benefits of using CSI

There are a number of benefits to using CSI with Kubernetes:

-   **Simplified storage management**: Using CSI with Kubernetes can help simplify storage management for your applications. For example, you can use a single storage class to provision storage for multiple applications.

-   **Increased storage solution flexibility**: CSI allows Kubernetes to support a wider range of storage solutions. This can be helpful if you're using a storage solution that isn't natively supported by Kubernetes.

-   **Improved storage solution integration**: CSI can help improve the integration between Kubernetes and storage solutions. For example, some storage solutions may provide additional features, such as snapshotting and replication, that can be used with Kubernetes.

## Conclusion

In this article, we've looked at how to use CSI with Kubernetes to manage storage for your applications. We've also learned about some of the benefits of using CSI, such as simplified storage management and increased storage solution flexibility.