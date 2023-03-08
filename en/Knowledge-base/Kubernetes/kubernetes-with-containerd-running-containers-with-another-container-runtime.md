---
title: Kubernetes with Containerd: Running Containers with Another Container Runtime
description: 
published: true
date: 2023-02-14T10:32:30.958Z
tags: 
editor: markdown
dateCreated: 2023-02-14T10:32:28.857Z
---

- [Kubernetes con Containerd: ejecución de contenedores con otro tiempo de ejecución de contenedores***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-with-containerd-running-containers-with-another-container-runtime)
{.links-list}
- [带有 Containerd 的 Kubernetes：使用另一个容器运行时运行容器***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-with-containerd-running-containers-with-another-container-runtime)
{.links-list}
- [Containerd가 포함된 Kubernetes: 다른 컨테이너 런타임으로 컨테이너 실행***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-with-containerd-running-containers-with-another-container-runtime)
{.links-list}


# Kubernetes with Containerd: Running Containers with Another Container Runtime

The default container runtime for Kubernetes is Docker, but Kubernetes is also compatible with other container runtimes. In this article, we'll take a look at running Kubernetes with Containerd.

## Why Use Containerd?

Containerd is an industry-standard container runtime that is popular for its simplicity and robustness. It is also used by other container orchestration platforms such as Docker Swarm and Apache Mesos.

## Installing Containerd

To install Containerd, you can use a package manager such as apt or yum.

```
sudo apt install containerd
```

## Configuring Kubernetes to Use Containerd

Once Containerd is installed, you need to configure Kubernetes to use it as the container runtime. To do this, you need to edit the `/etc/kubernetes/manifests/kubelet.yaml` file and add the following line:

```
--container-runtime=containerd
```

You also need to edit the `/etc/systemd/system/kubelet.service.d/10-kubelet.conf` file and add the following line:

```
Environment="KUBELET_EXTRA_ARGS=--container-runtime=containerd"
```

After making these changes, you need to restart the `kubelet` service.

```
sudo systemctl restart kubelet
```

## Creating a Container

Now that Kubernetes is configured to use Containerd, let's create a container.

First, we need to create a file called `container.json` with the following contents:

```json
{
  "id": "container1",
  "runtime": "containerd",
  "image": "nginx:latest"
}
```

Next, we need to create the container using the `ctr` command.

```
sudo ctr create -f container.json
```

## Running a Container

Now that we have created a container, let's run it.

First, we need to create a file called `run.json` with the following contents:

```json
{
  "id": "container1",
  "runtime": "containerd",
  "image": "nginx:latest",
  "command": ["nginx", "-g", "daemon off;"]
}
```

Next, we need to run the container using the `ctr` command.

```
sudo ctr run -f run.json
```

## Deleting a Container

To delete a container, we can use the `ctr` command.

```
sudo ctr delete container1
```

## Conclusion

In this article, we have looked at how to use Kubernetes with Containerd. We have also seen how to install Containerd, configure Kubernetes to use it, and how to create and run containers.