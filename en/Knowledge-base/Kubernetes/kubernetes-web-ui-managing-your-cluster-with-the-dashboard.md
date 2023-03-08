---
title: Kubernetes Web UI: Managing Your Cluster with the Dashboard
description: 
published: true
date: 2023-02-14T02:32:27.867Z
tags: 
editor: markdown
dateCreated: 2023-02-14T02:32:25.901Z
---

- [Interfaz de usuario web de Kubernetes: administración de su clúster con el tablero***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-web-ui-managing-your-cluster-with-the-dashboard)
{.links-list}
- [Kubernetes Web UI：使用仪表板管理您的集群***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-web-ui-managing-your-cluster-with-the-dashboard)
{.links-list}
- [Kubernetes 웹 UI: 대시보드로 클러스터 관리***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-web-ui-managing-your-cluster-with-the-dashboard)
{.links-list}


# Kubernetes Web UI: Managing Your Cluster with the Dashboard

Kubernetes is a powerful container orchestration tool that can help you manage your applications and resources at scale. The Kubernetes Dashboard is a web-based UI that can help you manage your Kubernetes cluster. In this article, we will look at how to use the Dashboard to manage your cluster.

## Accessing the Dashboard

To access the Dashboard, you will need to have a Kubernetes cluster up and running. You can follow the instructions in the Kubernetes documentation to [set up a local cluster](https://kubernetes.io/docs/setup/learning-environment/minikube/).

Once you have a cluster up and running, you can access the Dashboard by running the following command:

```
kubectl proxy
```

This will start a proxy to the Kubernetes API server and make the Dashboard available at http://localhost:8001/api/v1/namespaces/kube-system/services/kubernetes-dashboard:/proxy/.

## Creating a Kubernetes Cluster

To create a Kubernetes cluster, you will need to have a running Kubernetes cluster. You can follow the instructions in the Kubernetes documentation to [set up a local cluster](https://kubernetes.io/docs/setup/learning-environment/minikube/).

Once you have a Kubernetes cluster up and running, you can create a new cluster by running the following command:

```
kubectl create cluster my-cluster
```

You can verify that the cluster was created by running the following command:

```
kubectl get clusters
```

## Deleting a Kubernetes Cluster

To delete a Kubernetes cluster, you will need to have a running Kubernetes cluster. You can follow the instructions in the Kubernetes documentation to [set up a local cluster](https://kubernetes.io/docs/setup/learning-environment/minikube/).

Once you have a Kubernetes cluster up and running, you can delete a cluster by running the following command:

```
kubectl delete cluster my-cluster
```

You can verify that the cluster was deleted by running the following command:

```
kubectl get clusters
```

## Managing Nodes

The Kubernetes Dashboard can be used to manage nodes in a Kubernetes cluster. To view a list of nodes in the cluster, click on the "Nodes" link in the left-hand navigation. This will open a page that lists all of the nodes in the cluster.

From this page, you can view information about each node, such as its IP address, operating system, and kernel version. You can also perform actions on nodes, such as deleting them or scaling them up or down.

## Managing Pods

The Kubernetes Dashboard can be used to manage pods in a Kubernetes cluster. To view a list of pods in the cluster, click on the "Pods" link in the left-hand navigation. This will open a page that lists all of the pods in the cluster.

From this page, you can view information about each pod, such as its IP address and the nodes it is running on. You can also perform actions on pods, such as deleting them or scaling them up or down.

## Managing Deployments

The Kubernetes Dashboard can be used to manage deployments in a Kubernetes cluster. To view a list of deployments in the cluster, click on the "Deployments" link in the left-hand navigation. This will open a page that lists all of the deployments in the cluster.

From this page, you can view information about each deployment, such as the number of replicas and the pods that are part of the deployment. You can also perform actions on deployments, such as scaling them up or down.

## Managing Services

The Kubernetes Dashboard can be used to manage services in a Kubernetes cluster. To view a list of services in the cluster, click on the "Services" link in the left-hand navigation. This will open a page that lists all of the services in the cluster.

From this page, you can view information about each service, such as the type of service and the pods that are part of the service. You can also perform actions on services, such as editing the service or deleting it.

## Conclusion

In this article, we have seen how to use the Kubernetes Dashboard to manage a Kubernetes cluster. We have looked at how to create and delete clusters, how to manage nodes and pods, and how to manage deployments and services.