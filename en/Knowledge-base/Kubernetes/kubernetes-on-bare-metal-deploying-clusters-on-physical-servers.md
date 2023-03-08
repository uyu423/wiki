---
title: Kubernetes on Bare Metal: Deploying Clusters on Physical Servers
description: 
published: true
date: 2023-02-14T08:33:13.514Z
tags: 
editor: markdown
dateCreated: 2023-02-14T08:33:06.022Z
---

- [Kubernetes en Bare Metal: Implementación de clústeres en servidores físicos***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-on-bare-metal-deploying-clusters-on-physical-servers)
{.links-list}
- [裸机上的 Kubernetes：在物理服务器上部署集群***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-on-bare-metal-deploying-clusters-on-physical-servers)
{.links-list}
- [베어 메탈의 쿠버네티스: 물리적 서버에 클러스터 배포***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-on-bare-metal-deploying-clusters-on-physical-servers)
{.links-list}


# Kubernetes on Bare Metal: Deploying Clusters on Physical Servers

Nowadays, containers are being used more and more to package and deploy applications. This is because containers offer many benefits over traditional virtual machines, such as being more portable, having a smaller footprint, and being able to start up faster.

Kubernetes is a popular container orchestration tool that can be used to manage large numbers of containers. Kubernetes is often used with cloud-based solutions, but it can also be deployed on bare metal servers.

Deploying Kubernetes on bare metal servers can offer some advantages over using it with a cloud-based solution. For example, it can be more cost-effective and you have more control over the hardware.

In this article, we will take a look at how to deploy a Kubernetes cluster on bare metal servers. We will also look at some of the challenges that you may face when doing this.

## Overview

Before we get started, let's take a quick look at some of the key concepts that we will be using in this article.

**Kubernetes**: Kubernetes is a container orchestration tool that can be used to manage large numbers of containers.

**Bare metal server**: A bare metal server is a physical server that does not have a virtualization layer.

**Cluster**: A cluster is a group of servers that are used to run an application or service.

**Master node**: The master node is the server that is used to manage the Kubernetes cluster.

**Worker node**: Worker nodes are the servers that are used to run the containers.

## Prerequisites

Before you begin, you will need to have the following items:

- A group of bare metal servers. For this article, we will be using three servers.
- A network switch that the servers can be connected to.
- A way to install Kubernetes on the servers. For this article, we will be using the Kubernetes installer, kubeadm.

## Installing Kubernetes

In this section, we will take a look at how to install Kubernetes on the servers. We will be using the Kubernetes installer, kubeadm.

Kubeadm is a tool that can be used to install and configure Kubernetes. It is designed to be easy to use and easy to extend.

### Installing kubeadm

The first thing that we need to do is install kubeadm on the servers. We can do this with the following command:

```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update && sudo apt-get install -y kubeadm
```

### Initializing the master node

Once kubeadm is installed, we can initialize the master node. This is the server that will be used to manage the Kubernetes cluster.

To initialize the master node, we need to use the kubeadm init command. This command will start up a Kubernetes control plane on the server.

```
sudo kubeadm init
```

Once the command has completed, you will see a message that looks like this:

```
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following commands:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

You can now join any number of machines by running the following on each node
as root:

  kubeadm join 10.0.0.1:6443 --token ahc2xf.i0f4v9f0johtr5b4 --discovery-token-ca-cert-hash sha256:7ad1f8d3c908f3f558eaebf09abf8c3bdbbebfa7a7faebcbadea1a1a7fd0c74
```

You will need to run the commands that are listed in the output in order to configure your server to use the Kubernetes cluster.

### Joining worker nodes

Now that the master node is up and running, we can add worker nodes to the cluster. Worker nodes are the servers that are used to run the containers.

To add a worker node to the cluster, we need to use the kubeadm join command. This command will add the server to the Kubernetes cluster.

```
sudo kubeadm join 10.0.0.1:6443 --token ahc2xf.i0f4v9f0johtr5b4 --discovery-token-ca-cert-hash sha256:7ad1f8d3c908f3f558eaebf09abf8c3bdbbebfa7a7faebcbadea1a1a7fd0c74
```

## Configuring the Cluster

In this section, we will take a look at how to configure the Kubernetes cluster.

### Configuring the master node

The first thing that we need to do is configure the master node. We can do this by running the following command:

```
sudo kubectl apply -f https://git.io/weave-kube-1.6
```

This command will create a pod network on the server. A pod network is a network that is used to connect the containers.

### Configuring the worker nodes

Next, we need to configure the worker nodes. We can do this by running the following command on each worker node:

```
sudo kubectl apply -f https://git.io/weave-kube-1.6
```

This command will create a pod network on the server. A pod network is a network that is used to connect the containers.

## Deploying an Application

In this section, we will take a look at how to deploy an application to the Kubernetes cluster.

We will be using the nginx-deployment.yaml file that is located in the examples directory. This file contains the configuration for an nginx deployment.

To deploy the application, we need to run the following command:

```
kubectl apply -f examples/nginx-deployment.yaml
```

This command will create a deployment on the Kubernetes cluster. A deployment is a group of replicasets. A replicaset is a group of pods.

## Accessing the Application

In this section, we will take a look at how to access the application that we deployed.

To access the application, we need to create an ingress resource. An ingress resource is a resource that is used to route traffic to the application.

We can create an ingress resource by running the following command:

```
kubectl apply -f examples/nginx-ingress.yaml
```

This command will create an ingress resource on the Kubernetes cluster.

Once the ingress resource has been created, we can access the application by going to the following URL:

http://<cluster-ip>

## Deleting the Cluster

In this section, we will take a look at how to delete the Kubernetes cluster.

To delete the cluster, we need to use the kubectl delete command. This command will delete all of the resources in the cluster.

```
kubectl delete -f examples/nginx-deployment.yaml
kubectl delete -f examples/nginx-ingress.yaml
```

## Conclusion

In this article, we have taken a look at how to deploy a Kubernetes cluster on bare metal servers. We have also looked at how to deploy an application to the cluster.