---
title: Kubernetes on OpenStack: Deploying Clusters on OpenStack
description: 
published: true
date: 2023-02-14T06:32:54.305Z
tags: 
editor: markdown
dateCreated: 2023-02-14T06:32:47.093Z
---

- [Kubernetes en OpenStack: implementación de clústeres en OpenStack***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-on-openstack-deploying-clusters-on-openstack)
{.links-list}
- [OpenStack 上的 Kubernetes：在 OpenStack 上部署集群***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-on-openstack-deploying-clusters-on-openstack)
{.links-list}
- [OpenStack의 Kubernetes: OpenStack에 클러스터 배포***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-on-openstack-deploying-clusters-on-openstack)
{.links-list}


# Kubernetes on OpenStack: Deploying Clusters on OpenStack

OpenStack is a cloud operating system that controls large pools of compute, storage, and networking resources throughout a datacenter, all managed through a dashboard that gives administrators control while empowering their users to provision resources through a web interface.

Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications.

The goal of this article is to show you how to deploy a Kubernetes cluster on OpenStack. We'll cover the following topics:

- Prerequisites
- Creating a Kubernetes cluster
- Deploying an application on the cluster

## Prerequisites

In order to follow this guide, you will need the following:

- An OpenStack cloud with the following:
  - A network
  - A router
  - A subnet
  - A security group
  - A key pair
  - At least 3 compute nodes
- The OpenStack CLI installed and configured
- The Kubernetes CLI installed and configured

## Creating a Kubernetes cluster

We'll use the `kube-up.sh` script to deploy a Kubernetes cluster. This script will create all of the necessary resources on OpenStack, including compute instances, networks, and load balancers.

First, clone the Kubernetes repository:

```
git clone https://github.com/kubernetes/kubernetes.git
```

Next, change into the `kubernetes/cluster/openstack` directory:

```
cd kubernetes/cluster/openstack
```

Then, create a file named `cloud-config.yaml` with the following contents:

```yaml
#cloud-config

write_files:
- owner: root:root
  path: /etc/kubernetes/kube-up-config.yaml
  content: |
    CLOUD_PROVIDER=openstack
    OPENSTACK_AUTH_URL=https://identity.example.com:5000/v3
    OPENSTACK_USERNAME=admin
    OPENSTACK_PASSWORD=admin
    OPENSTACK_TENANT_NAME=admin
    OPENSTACK_REGION=regionOne
    OPENSTACK_CLUSTER_NAME=kubernetes
    OPENSTACK_CLUSTER_SIZE=3
    OPENSTACK_MASTER_FLAVOR=m1.small
    OPENSTACK_MASTER_IMAGE=ubuntu-16.04-x86_64-20170119
    OPENSTACK_WORKER_FLAVOR=m1.small
    OPENSTACK_WORKER_IMAGE=ubuntu-16.04-x86_64-20170119
    OPENSTACK_NETWORK_NAME=kubernetes
    OPENSTACK_MASTER_OS_DISTRIBUTION=ubuntu
    OPENSTACK_WORKER_OS_DISTRIBUTION=ubuntu
```

Replace the values in this file with your own OpenStack credentials and settings.

Now, you can deploy the cluster by running the `kube-up.sh` script:

```
./kube-up.sh
```

This will take a few minutes to complete. Once it's finished, you should see 3 compute instances in your OpenStack dashboard, along with a network, router, and load balancer.

## Deploying an application on the cluster

Now that we have a Kubernetes cluster up and running on OpenStack, let's deploy a simple application on it. We'll use a pre-built container image for a "Hello, World" web application.

First, we need to create a file named `hello-world.yaml` with the following contents:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
  labels:
    app: hello-world
spec:
  replicas: 3
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: tutum/hello-world
        ports:
        - containerPort: 80
```

This file defines a deployment named "hello-world" with 3 replica pods. The pods will be created from the `tutum/hello-world` container image, which is a simple "Hello, World" web application. The pods will be exposed on port 80.

We can now deploy this application by running the following command:

```
kubectl create -f hello-world.yaml
```

This will take a few seconds to create the pods. Once they're up and running, we can expose them to the outside world by creating a service:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-world
  labels:
    app: hello-world
spec:
  type: LoadBalancer
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: hello-world
```

Save this file as `hello-world-service.yaml` and deploy it with the following command:

```
kubectl create -f hello-world-service.yaml
```

This will create a load balancer and expose the service on port 80. You can find the public IP address of the load balancer by running the following command:

```
kubectl get service hello-world
```

You should see an output similar to the following:

```
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP       PORT(S)        AGE
hello-world  LoadBalancer   10.0.0.1        1.2.3.4           80:31527/TCP   1m
```

You can now access the "Hello, World" web application by visiting the load balancer's public IP address in your web browser.

## Conclusion

In this article, we showed you how to deploy a Kubernetes cluster on OpenStack. We also showed you how to deploy a simple web application on the cluster.

For further reading, check out the following resources:

- [Kubernetes on OpenStack: A Reference Architecture](https://www.openstack.org/assets/pdf/kubernetes-on-openstack-a-reference-architecture.pdf)
- [Deploying Kubernetes on OpenStack](https://www.mirantis.com/blog/deploying-kubernetes-on-openstack/)
- [Kubernetes the Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way)