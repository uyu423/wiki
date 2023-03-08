---
title: Kubernetes Pods: The Building Blocks of Your Cluster
description: 
published: true
date: 2023-02-17T18:05:37.131Z
tags: 
editor: markdown
dateCreated: 2023-01-30T14:32:40.133Z
---

- [Kubernetes 포드: 클러스터의 빌딩 블록***Korean** version of this document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-pods-the-building-blocks-of-your-cluster)
{.links-list}
- [Kubernetes Pod: クラスターの構成要素***Japanese** version of this document is available*](/ja/Knowledge-base/Kubernetes/kubernetes-pods-the-building-blocks-of-your-cluster)
{.links-list}
- [Kubernetes Pod：集群的构建块***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-pods-the-building-blocks-of-your-cluster)
{.links-list}



# Kubernetes Pods: The Building Blocks of Your Cluster

Kubernetes pods are the smallest deployable units in a Kubernetes cluster, and they are the building blocks of your cluster. Pods are ephemeral, which means they are not guaranteed to be running at any given time, and they can be deleted and recreated as needed.

Pods are managed by the Kubernetes control plane, and they can be crashing and restarting without you even knowing it. This is one of the benefits of using Kubernetes: By abstracting away the individual machines in your cluster, you can treat your entire cluster as a single entity.

Pods contain one or more containers, and they can be used to host applications, databases, or anything else you need to run in your Kubernetes cluster. Pods are always co-located and co-scheduled on the same node, which means they can share resources like volumes and network interfaces.

When you create a pod, you must specify the desired state for the pod, including the container images and any required configuration. Kubernetes will then take care of keeping the pod in the desired state.

Pods are the basic units of deployment in Kubernetes, and they are usually used to host stateless applications. If you need to run a stateful application in Kubernetes, you will need to use a StatefulSet.

## Creating a Pod

You can create a pod using the `kubectl` command-line tool, or you can use an manifests file. 

### Using `kubectl`

To create a pod using `kubectl`, you can use the `run` command. For example, to create a pod that will run the `nginx` container image, you can use the following command:

```
kubectl run nginx --image=nginx
```

This will create a pod with a single `nginx` container. If you want to create a pod with multiple containers, you can use the `run-container` command:

```
kubectl run-container nginx-container --image=nginx --image=mysql
```

### Using a Manifest File

Alternatively, you can create a pod by creating a `Pod` manifest file and using the `kubectl` `create` command. For example, the following manifest file would create a pod with a single `nginx` container:

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

You can then create the pod by running the following command:

```
kubectl create -f nginx.yaml
```

## Deleting a Pod

Pods can be deleted using the `kubectl` `delete` command. For example, to delete the `nginx` pod created in the previous section, you can use the following command:

```
kubectl delete pod nginx
```

## Pod States

A pod can be in one of the following states:

- **Pending**: The pod has been created, but one or more of its containers has not been started.
- **Running**: The pod and all of its containers are running.
- **Succeeded**: The pod completed its work successfully and all of its containers are in the `Exited` state.
- **Failed**: The pod failed and all of its containers are in the `Exited` state.
- **Unknown**: The state of the pod could not be determined.

## Conclusion

Kubernetes pods are the building blocks of your cluster, and they are used to host applications, databases, or anything else you need to run in your Kubernetes cluster. Pods are always co-located and co-scheduled on the same node, which means they can share resources like volumes and network interfaces.

When you create a pod, you must specify the desired state for the pod, including the container images and any required configuration. Kubernetes will then take care of keeping the pod in the desired state.

Pods are the basic units of deployment in Kubernetes, and they are usually used to host stateless applications. If you need to run a stateful application in Kubernetes, you will need to use a StatefulSet.