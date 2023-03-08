---
title: 带有 gVisor 的 Kubernetes：使用沙盒运行时增强容器安全性
description: 
published: true
date: 2023-02-14T11:33:10.657Z
tags: 
editor: markdown
dateCreated: 2023-02-14T11:33:08.987Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes with gVisor: Enhancing Container Security with a Sandboxed Runtime***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-gvisor-enhancing-container-security-with-a-sandboxed-runtime)
{.links-list}


# 带有 gVisor 的 Kubernetes：使用沙盒运行时增强容器安全性

Kubernetes 是一个开源系统，用于自动部署、扩展和管理容器化应用程序。 gVisor 是一个运行时沙箱，它使用内核功能来隔离进程并提高安全性。

## 什么是 gVisor？

gVisor 是一个运行时沙箱，它使用内核功能来隔离进程并提高安全性。它旨在在安全环境中运行不受信任的代码。 gVisor 由 Google Cloud Platform 使用并作为开源提供。

gVisor 是一个运行在 Linux 内核之上的用户空间程序。它提供了底层操作系统和资源的有限视图。这限制了恶意程序或错误程序可能造成的损害程度。

gVisor 不是一个完整的虚拟机。它不提供自己的内核或设备驱动程序。相反，它使用底层操作系统的内核和驱动程序。这使得 gVisor 比完整的虚拟机重量更轻且更易于使用。

## gVisor 是如何工作的？

gVisor 使用 Linux 内核特性来隔离进程。这些功能包括命名空间、cgroups 和 seccomp-bpf。

命名空间提供进程之间的隔离。它们允许进程拥有自己的系统视图，包括它们自己的文件系统和网络。

Cgroup 限制进程可以使用的资源。它们可用于限制进程可以使用的 CPU、内存和磁盘空间的数量。

Seccomp-bpf 是一种安全功能，允许将进程放入沙箱。它过滤系统调用并阻止危险的调用。

## Kubernetes 如何使用 gVisor？

Kubernetes 使用 gVisor 来提高容器的安全性。默认情况下，容器与主机操作系统共享相同的内核。这可能是一个安全风险，因为恶意容器可以访问主机操作系统。

gVisor 为容器提供沙盒运行时。这将容器与主机操作系统隔离开来并提高了安全性。

## 如何将 Kubernetes 与 gVisor 一起使用？

您可以通过将 `--runtime=runsc` 标志添加到 `kubelet` 命令来将 Kubernetes 与 gVisor 一起使用。这将使用 gVisor 作为容器的运行时。

您还可以通过将 `--runtime-provider=runsc` 标志添加到 `kubelet` 命令来将 Kubernetes 与 gVisor 一起使用。这将使用 gVisor 作为容器的运行时提供者。

## 如何使用 gVisor 安装 Kubernetes？

您可以使用包管理器（例如“apt”或“yum”）使用 gVisor 安装 Kubernetes。

```
apt install kubelet=1.10.11-00 runc=1.0.0-rc5-3
```

```
yum install kubelet-1.10.11-0 runc-1.0.0-rc5-3
```

## 如何使用 gVisor 升级 Kubernetes？

您可以使用包管理器（例如“apt”或“yum”）使用 gVisor 升级 Kubernetes。

```
apt upgrade kubelet=1.10.11-00 runc=1.0.0-rc5-3
```

```
yum upgrade kubelet-1.10.11-0 runc-1.0.0-rc5-3
```

## 如何使用 gVisor 配置 Kubernetes？

您可以通过将 `--runtime=runsc` 标志添加到 `kubelet` 命令来使用 gVisor 配置 Kubernetes。这将使用 gVisor 作为容器的运行时。

您还可以通过将 `--runtime-provider=runsc` 标志添加到 `kubelet` 命令来将 Kubernetes 与 gVisor 一起使用。这将使用 gVisor 作为容器的运行时提供者。

## 如何使用 gVisor 卸载 Kubernetes？

您可以使用“apt”或“yum”等包管理器通过 gVisor 卸载 Kubernetes。

```
apt remove kubelet runc
```

```
yum remove kubelet runc
```

## 结论

带有 gVisor 的 Kubernetes 是运行容器的安全方式。 gVisor 为容器提供沙盒运行时。这将容器与主机操作系统隔离开来并提高了安全性。