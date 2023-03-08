---
title: Kubernetes with CRI-O: Running Containers with an Alternative Container Runtime
description: 
published: true
date: 2023-02-14T09:32:23.736Z
tags: 
editor: markdown
dateCreated: 2023-02-14T09:32:22.075Z
---

- [Kubernetes con CRI-O: ejecución de contenedores con un tiempo de ejecución de contenedor alternativo***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-with-cri-o-running-containers-with-an-alternative-container-runtime)
{.links-list}
- [带有 CRI-O 的 Kubernetes：使用替代容器运行时运行容器***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-with-cri-o-running-containers-with-an-alternative-container-runtime)
{.links-list}
- [CRI-O가 포함된 Kubernetes: 대체 컨테이너 런타임으로 컨테이너 실행***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-with-cri-o-running-containers-with-an-alternative-container-runtime)
{.links-list}


# Kubernetes with CRI-O: Running Containers with an Alternative Container Runtime

## What is CRI-O?

CRI-O is an alternative container runtime for Kubernetes. It is designed to be lightweight and have a minimal footprint, making it ideal for running containers on Kubernetes. CRI-O uses the Open Containers Initiative (OCI) runtime specification and is compatible with the Kubernetes CRI (Container Runtime Interface).

## Why use CRI-O with Kubernetes?

There are a few reasons why you might want to use CRI-O with Kubernetes:

- CRI-O is designed to be lightweight and have a minimal footprint. This makes it ideal for running containers on Kubernetes.
- CRI-O uses the Open Containers Initiative (OCI) runtime specification. This means that it is compatible with the Kubernetes CRI (Container Runtime Interface).
- CRI-O is integrated with the Kubernetes container network interface (CNI) plugin. This makes it easy to set up networking for containers running on Kubernetes.

## How to use CRI-O with Kubernetes

Using CRI-O with Kubernetes is easy. You can either use the CRI-O container runtime directly, or use the CRI-O Kubernetes integration.

### Using the CRI-O container runtime directly

To use the CRI-O container runtime directly, you need to set the `--runtime` flag when starting the Kubernetes `kubelet`:

```
$ kubelet --runtime=cri-o
```

### Using the CRI-O Kubernetes integration

To use the CRI-O Kubernetes integration, you need to set the `--container-runtime` flag when starting the Kubernetes `kubelet`:

```
$ kubelet --container-runtime=cri-o
```

You also need to set the `--feature-gates` flag to enable the CRI-O Kubernetes integration:

```
$ kubelet --feature-gates=CRIO=true
```

## Conclusion

CRI-O is a great alternative container runtime for Kubernetes. It is designed to be lightweight and have a minimal footprint, making it ideal for running containers on Kubernetes. CRI-O uses the Open Containers Initiative (OCI) runtime specification and is compatible with the Kubernetes CRI (Container Runtime Interface). CRI-O is also integrated with the Kubernetes container network interface (CNI) plugin. This makes it easy to set up networking for containers running on Kubernetes.