---
title: Kubernetes Multi-Cluster Management: Managing Multiple Clusters with kubefed
description: 
published: true
date: 2023-02-14T04:32:37.510Z
tags: 
editor: markdown
dateCreated: 2023-02-14T04:32:29.987Z
---

- [Gestión de varios clústeres de Kubernetes: gestión de varios clústeres con kubefed***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-multi-cluster-management-managing-multiple-clusters-with-kubefed)
{.links-list}
- [Kubernetes 多集群管理：使用 kubefed 管理多个集群***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-multi-cluster-management-managing-multiple-clusters-with-kubefed)
{.links-list}
- [Kubernetes 다중 클러스터 관리: kubefed로 다중 클러스터 관리***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-multi-cluster-management-managing-multiple-clusters-with-kubefed)
{.links-list}



# Kubernetes Multi-Cluster Management: Managing Multiple Clusters with kubefed

In a production environment, it is not uncommon to have multiple Kubernetes clusters. This can be for a variety of reasons, including scaling, high availability, or different teams working on different projects.

Managing multiple Kubernetes clusters can be a challenge, especially when it comes to keeping them in sync. There are a few options for managing multiple Kubernetes clusters, but in this article, we will focus on kubefed.

kubefed is a tool that can be used to manage multiple Kubernetes clusters. It is part of the Kubernetes project and is designed to make it easy to create and maintain a federation of Kubernetes clusters.

kubefed has a few dependencies, including:

- kubectl
- kube-apiserver
- kube-controller-manager

kubefed also requires a Kubernetes cluster that meets the following requirements:

- Kubernetes version 1.4 or higher
- Cluster must have RBAC enabled

## Creating a kubefed Cluster

Creating a kubefed cluster is easy. First, we need to create a ConfigMap that will be used to store the kubefed configuration. We will call this ConfigMap "kubefed-config":

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: kubefed-config
  namespace: kube-system
data:
  kubefed.yaml: |
    apiVersion: federation/v1beta1
    kind: Federation
    metadata:
      name: federation
    spec:
      # Add clusters to the federation here.
      clusters:
      - clusterName: cluster1
        serverAddressByClientCIDRs:
        - clientCIDR: 0.0.0.0/0
          serverAddress: https://10.0.1.1:6443
      - clusterName: cluster2
        serverAddressByClientCIDRs:
        - clientCIDR: 0.0.0.0/0
          serverAddress: https://10.0.2.1:6443
    ```

This ConfigMap defines two Kubernetes clusters that we want to add to our federation. The "cluster1" and "cluster2" entries in the "clusters" list are the names of the clusters that we want to add. The "serverAddressByClientCIDRs" entry defines the URL of the Kubernetes API server for each cluster.

Next, we need to create a Secret that will be used to store the kubeconfig files for each cluster. We will call this Secret "kubefed-kubeconfig":

```
apiVersion: v1
kind: Secret
metadata:
  name: kubefed-kubeconfig
  namespace: kube-system
data:
  kubeconfig-cluster1: |
    apiVersion: v1
    kind: Config
    clusters:
    - cluster:
        server: https://10.0.1.1:6443
        name: cluster1
      name: cluster1
    contexts:
    - context:
        cluster: cluster1
        user: admin
      name: cluster1
    current-context: cluster1
    preferences: {}
    users:
    - name: admin
      user:
        token: abcdefg
  kubeconfig-cluster2: |
    apiVersion: v1
    kind: Config
    clusters:
    - cluster:
        server: https://10.0.2.1:6443
        name: cluster2
      name: cluster2
    contexts:
    - context:
        cluster: cluster2
        user: admin
      name: cluster2
    current-context: cluster2
    preferences: {}
    users:
    - name: admin
      user:
        token: hijklmnop
    ```

This Secret contains the kubeconfig files for each cluster. The kubeconfig file for cluster1 is stored in the "kubeconfig-cluster1" key and the kubeconfig file for cluster2 is stored in the "kubeconfig-cluster2" key.

With the ConfigMap and Secret in place, we can now create the kubefed cluster. We will use the kubectl command to create the kubefed cluster:

```
kubectl create -f kubefed-configmap.yaml
kubectl create -f kubefed-secret.yaml
kubectl create -f kubefed-cluster.yaml
```

This will create a new Kubernetes cluster called "kubefed". This cluster will be used to manage the other two Kubernetes clusters that we defined in the ConfigMap and Secret.

## Adding Clusters to kubefed

Now that we have a kubefed cluster, we can add our other Kubernetes clusters to it. We will use the kubefed command to add the clusters:

```
kubefed join cluster1 --host-cluster-context=cluster1 --cluster-context=cluster1
kubefed join cluster2 --host-cluster-context=cluster2 --cluster-context=cluster2
```

This will add the "cluster1" and "cluster2" Kubernetes clusters to the kubefed cluster. The "--host-cluster-context" and "--cluster-context" arguments specify the kubeconfig contexts to use for the host cluster (kubefed) and the cluster being added (cluster1 or cluster2).

## Managing kubefed

Now that we have our kubefed cluster up and running, we can start using it to manage our other Kubernetes clusters.

The kubefed command can be used to manage kubefed and the Kubernetes clusters that it is managing.

To list the Kubernetes clusters that kubefed is managing, use the "kubefed list" command:

```
kubefed list
```

This will list the Kubernetes clusters that kubefed is currently managing.

To get more information about a particular Kubernetes cluster, use the "kubefed describe" command:

```
kubefed describe cluster1
```

This will provide more information about the "cluster1" Kubernetes cluster.

The kubefed command can also be used to scale a Kubernetes cluster. To scale a cluster, use the "kubefed scale" command:

```
kubefed scale cluster1 --replicas=3
```

This will scale the "cluster1" Kubernetes cluster to three replicas.

## Deleting a kubefed Cluster

When you are finished with a kubefed cluster, you can delete it using the "kubefed delete" command:

```
kubefed delete cluster1
```

This will delete the "cluster1" Kubernetes cluster from kubefed.

## Conclusion

kubefed is a valuable tool for managing multiple Kubernetes clusters. It is easy to use and can help you keep your clusters in sync.