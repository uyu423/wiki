---
title: Kubernetes with gVisor: Enhancing Container Security with a Sandboxed Runtime
description: 
published: true
date: 2023-02-14T11:33:16.549Z
tags: 
editor: markdown
dateCreated: 2023-02-14T11:33:08.992Z
---

- [Kubernetes con gVisor: mejora de la seguridad de los contenedores con un tiempo de ejecución en espacio aislado***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-with-gvisor-enhancing-container-security-with-a-sandboxed-runtime)
{.links-list}
- [带有 gVisor 的 Kubernetes：使用沙盒运行时增强容器安全性***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-with-gvisor-enhancing-container-security-with-a-sandboxed-runtime)
{.links-list}
- [Kubernetes with gVisor: 샌드박스 런타임으로 컨테이너 보안 강화***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-with-gvisor-enhancing-container-security-with-a-sandboxed-runtime)
{.links-list}


# Kubernetes with gVisor: Enhancing Container Security with a Sandboxed Runtime

Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications. gVisor is a runtime sandbox that uses kernel features to isolate processes and improve security.

## What is gVisor?

gVisor is a runtime sandbox that uses kernel features to isolate processes and improve security. It is designed to run untrusted code in a secure environment. gVisor is used by Google Cloud Platform and is available as open source.

gVisor is a user-space program that runs on top of the Linux kernel. It provides a limited view of the underlying operating system and resources. This limits the amount of damage that can be caused by a malicious or buggy program.

gVisor is not a complete virtual machine. It does not provide its own kernel or device drivers. Instead, it uses the kernel and drivers of the underlying operating system. This makes gVisor lighter weight and easier to use than a full virtual machine.

## How does gVisor work?

gVisor uses Linux kernel features to isolate processes. These features include namespaces, cgroups, and seccomp-bpf.

Namespaces provide isolation between processes. They allow processes to have their own view of the system, including their own file system and network.

Cgroups limit the resources that a process can use. They can be used to limit the amount of CPU, memory, and disk space a process can use.

Seccomp-bpf is a security feature that allows processes to be sandboxed. It filters system calls and blocks dangerous ones.

## How does Kubernetes use gVisor?

Kubernetes uses gVisor to improve the security of containers. By default, containers share the same kernel as the host operating system. This can be a security risk because a malicious container can access the host operating system.

gVisor provides a sandboxed runtime for containers. This isolates the containers from the host operating system and improves security.

## How do I use Kubernetes with gVisor?

You can use Kubernetes with gVisor by adding the `--runtime=runsc` flag to the `kubelet` command. This will use gVisor as the runtime for containers.

You can also use Kubernetes with gVisor by adding the `--runtime-provider=runsc` flag to the `kubelet` command. This will use gVisor as the runtime provider for containers.

## How do I install Kubernetes with gVisor?

You can install Kubernetes with gVisor by using a package manager such as `apt` or `yum`.

```
apt install kubelet=1.10.11-00 runc=1.0.0-rc5-3
```

```
yum install kubelet-1.10.11-0 runc-1.0.0-rc5-3
```

## How do I upgrade Kubernetes with gVisor?

You can upgrade Kubernetes with gVisor by using a package manager such as `apt` or `yum`.

```
apt upgrade kubelet=1.10.11-00 runc=1.0.0-rc5-3
```

```
yum upgrade kubelet-1.10.11-0 runc-1.0.0-rc5-3
```

## How do I configure Kubernetes with gVisor?

You can configure Kubernetes with gVisor by adding the `--runtime=runsc` flag to the `kubelet` command. This will use gVisor as the runtime for containers.

You can also use Kubernetes with gVisor by adding the `--runtime-provider=runsc` flag to the `kubelet` command. This will use gVisor as the runtime provider for containers.

## How do I uninstall Kubernetes with gVisor?

You can uninstall Kubernetes with gVisor by using a package manager such as `apt` or `yum`.

```
apt remove kubelet runc
```

```
yum remove kubelet runc
```

## Conclusion

Kubernetes with gVisor is a secure way to run containers. gVisor provides a sandboxed runtime for containers. This isolates the containers from the host operating system and improves security.