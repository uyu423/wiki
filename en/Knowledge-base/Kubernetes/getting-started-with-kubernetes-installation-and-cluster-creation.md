---
title: Getting Started with Kubernetes: Installation and Cluster Creation
description: 
published: true
date: 2023-02-08T17:32:58.699Z
tags: 
editor: markdown
dateCreated: 2023-02-08T17:32:52.675Z
---

- [Introducción a Kubernetes: instalación y creación de clústeres***Spanish** document is available*](/es/Knowledge-base/Kubernetes/getting-started-with-kubernetes-installation-and-cluster-creation)
{.links-list}
- [Kubernetes 入门：安装和集群创建***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/getting-started-with-kubernetes-installation-and-cluster-creation)
{.links-list}
- [Kubernetes 시작하기: 설치 및 클러스터 생성***Korean** document is available*](/ko/Knowledge-base/Kubernetes/getting-started-with-kubernetes-installation-and-cluster-creation)
{.links-list}


# Getting Started with Kubernetes: Installation and Cluster Creation

Kubernetes is a powerful container orchestration tool that can help you automate the deployment, scaling, and management of your containerized applications. In this article, we will show you how to install Kubernetes on your local machine and create a Kubernetes cluster.

## Prerequisites

Before you begin, you will need the following:

- A local machine running Linux or Windows
- [Docker](https://docs.docker.com/install/) installed and running
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) installed
- [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/) installed

## Installing Kubernetes

Kubernetes can be installed on your local machine using Minikube. Minikube is a lightweight Kubernetes implementation that can be used for development and testing purposes.

To install Kubernetes using Minikube, run the following command:

```
$ minikube start
```

This will start a virtual machine and install Kubernetes on it. Once the installation is complete, you can verify the installation by running the following command:

```
$ kubectl get nodes
```

This command should list the node that was created by Minikube.

## Creating a Kubernetes Cluster

Now that Kubernetes is up and running, you can create a Kubernetes cluster. To do this, you will need to create a [deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) and a [service](https://kubernetes.io/docs/concepts/services-networking/service/).

A deployment is a Kubernetes object that describes a desired state for a group of pods. A service is a Kubernetes object that exposes a group of pods to the outside world.

To create a deployment and a service, you will need to create a [YAML](https://en.wikipedia.org/wiki/YAML) file that contains the following:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  ports:
  - port: 80
    nodePort: 30000
  selector:
    app: nginx
```

In this file, we have defined a deployment with three replicas of the [nginx](https://www.nginx.com/) container and a service that exposes the deployment to the outside world.

To create the deployment and service, run the following command:

```
$ kubectl apply -f deployment.yaml
```

This will create the deployment and service. You can verify that the deployment and service were created by running the following commands:

```
$ kubectl get deployments
```

```
$ kubectl get services
```

## Accessing the Kubernetes Cluster

Now that the deployment and service have been created, you can access the Kubernetes cluster from your local machine. To do this, you will need to get the IP address of the Minikube virtual machine and the node port of the service.

To get the IP address of the Minikube virtual machine, run the following command:

```
$ minikube ip
```

To get the node port of the service, run the following command:

```
$ kubectl describe service nginx-service
```

You should see the following output:

```
Name:              nginx-service
Namespace:         default
Labels:            <none>
Annotations:       <none>
Selector:          app=nginx
Type:              NodePort
IP:                10.0.0.1
Port:              <unnamed>  80/TCP
TargetPort:        80/TCP
NodePort:          <unnamed>  30000/TCP
Endpoints:         10.0.0.2:80,10.0.0.3:80,10.0.0.4:80
Session Affinity:  None
External Traffic Policy:  Cluster
Events:            <none>
```

The node port is the value of the `NodePort` field. In this case, the node port is `30000`.

To access the Kubernetes cluster, open a web browser and go to `http://<minikube-ip>:<node-port>`. In our example, the URL would be `http://10.0.0.1:30000`.

You should see the default nginx page:

![nginx](https://www.nginx.com/wp-content/uploads/2018/08/nginx-logo.png)

## Deleting the Kubernetes Cluster

To delete the Kubernetes cluster, run the following command:

```
$ minikube delete
```

This will delete the Minikube virtual machine and all the resources that were created in the previous steps.

## Conclusion

In this article, we showed you how to install Kubernetes on your local machine and create a Kubernetes cluster. Kubernetes is a powerful tool that can help you automate the deployment, scaling, and management of your containerized applications.