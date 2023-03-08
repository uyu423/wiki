---
title: Kubernetes Namespaces: Isolating Resources in Multi-Tenant Clusters
description: 
published: true
date: 2023-02-08T23:32:23.417Z
tags: 
editor: markdown
dateCreated: 2023-02-08T23:32:17.379Z
---

- [Espacios de nombres de Kubernetes: aislamiento de recursos en clústeres de múltiples inquilinos***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-namespaces-isolating-resources-in-multi-tenant-clusters)
{.links-list}
- [Kubernetes 命名空间：隔离多租户集群中的资源***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-namespaces-isolating-resources-in-multi-tenant-clusters)
{.links-list}
- [Kubernetes 네임스페이스: 다중 테넌트 클러스터에서 리소스 격리***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-namespaces-isolating-resources-in-multi-tenant-clusters)
{.links-list}


# Kubernetes Namespaces: Isolating Resources in Multi-Tenant Clusters

Kubernetes namespaces offer a simple but powerful way to isolate resources in a shared cluster. By creating separate namespaces for each tenant, you can control which users have access to which resources, and limit the visibility of resources between tenants.

## Creating Namespaces

You can create a namespace by running the `kubectl create namespace` command. For example, to create a namespace for a tenant called `acme`, you would run:

```
kubectl create namespace acme
```

## Assigning Resources to Namespaces

Once a namespace has been created, you can assign resources to it using the `--namespace` flag with the `kubectl` command. For example, to create a pod in the `acme` namespace, you would run:

```
kubectl create pod --namespace acme ...
```

## Viewing Resources in a Namespace

By default, the `kubectl` command will only show resources in the `default` namespace. To view resources in a different namespace, you can use the `--namespace` flag with the `kubectl get` command. For example, to view all pods in the `acme` namespace, you would run:

```
kubectl get pods --namespace acme
```

## Switching Between Namespaces

If you find yourself frequently running commands in a specific namespace, you can use the `kubectl config set-context` command to switch between namespaces. For example, to switch to the `acme` namespace, you would run:

```
kubectl config set-context $(kubectl config current-context) --namespace=acme
```

## Deleting Namespaces

You can delete a namespace by running the `kubectl delete namespace` command. For example, to delete the `acme` namespace, you would run:

```
kubectl delete namespace acme
```

## Conclusion

Kubernetes namespaces offer a simple but powerful way to isolate resources in a shared cluster. By creating separate namespaces for each tenant, you can control which users have access to which resources, and limit the visibility of resources between tenants.