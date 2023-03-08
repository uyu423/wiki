---
title: Kubernetes on Azure: Deploying Clusters on Microsoft Azure
description: 
published: true
date: 2023-02-01T16:17:59.813Z
tags: 
editor: markdown
dateCreated: 2023-02-01T16:17:58.187Z
---

- [Kubernetes en Azure: implementación de clústeres en Microsoft Azure***Spanish** version of this document is available*](/es/Knowledge-base/Kubernetes/kubernetes-on-azure-deploying-clusters-on-microsoft-azure)
{.links-list}
- [Azure의 Kubernetes: Microsoft Azure에 클러스터 배포***Korean** version of this document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-on-azure-deploying-clusters-on-microsoft-azure)
{.links-list}
- [Azure 上的 Kubernetes：在 Microsoft Azure 上部署集群***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-on-azure-deploying-clusters-on-microsoft-azure)
{.links-list}


# Kubernetes on Azure: Deploying Clusters on Microsoft Azure

Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications. It groups containers that make up an application into logical units for easy management and discovery. Microsoft Azure offers a managed Kubernetes service called Azure Kubernetes Service (AKS) that makes it quick and easy to deploy a production-ready Kubernetes cluster in Azure.

In this article, we will show you how to deploy a Kubernetes cluster on Azure using AKS. We will also show you how to deploy a simple application to the cluster and expose it to the internet.

## Prerequisites

Before you begin, you will need the following:

- An Azure account. If you don't have one, you can sign up for a free trial.
- The Azure CLI installed on your local machine.
- The kubectl command-line tool.

## Creating an AKS Cluster

The first step is to create an AKS cluster using the Azure CLI. We will use the az aks create command to create a resource group, an AKS cluster, and generate a kubeconfig file. The kubeconfig file is used by the kubectl tool to connect to the Kubernetes cluster.

Run the following command to create an AKS cluster:

```
az aks create \
  --resource-group myResourceGroup \
  --name myAKSCluster \
  --node-count 3 \
  --generate-ssh-keys
```

It will take a few minutes for the AKS cluster to be created. Once it is ready, you can use the kubectl tool to connect to the cluster.

## Connecting to the Cluster

To connect to the AKS cluster, you need to retrieve the cluster credentials from Azure and configure kubectl to use them.

Run the following command to retrieve the credentials:

```
az aks get-credentials \
  --resource-group myResourceGroup \
  --name myAKSCluster
```

This will download a kubeconfig file and merge it with the existing kubeconfig file on your machine.

You can now use the kubectl tool to interact with the AKS cluster. Run the following command to get a list of the nodes in the cluster:

```
kubectl get nodes
```

## Deploying an Application

Now that we have a working Kubernetes cluster, we can deploy an application to it. For this example, we will deploy a simple web application written in Node.js.

First, we need to create a Docker image of the application. We will use the Dockerfile in the project's root directory to build the image. Run the following command to build the image:

```
docker build -t my-app:v1 .
```

Once the image has been built, we can push it to a Docker registry. For this example, we will push it to Azure Container Registry (ACR).

First, we need to create an ACR instance. We can use the az acr create command to do this. Run the following command to create an ACR instance:

```
az acr create \
  --resource-group myResourceGroup \
  --name myACR \
  --sku Basic
```

Once the ACR instance has been created, we can push the Docker image to it. Run the following command to push the image:

```
docker push myacr.azurecr.io/my-app:v1
```

Now that the image has been pushed to ACR, we can deploy it to our AKS cluster. We will use a Kubernetes deployment to do this. A deployment is a resource that manages a set of replicas of a pod. The pod is the basic unit of deployment in Kubernetes. It is a group of one or more containers that are deployed together on the same host.

We will use the kubectl tool to create the deployment. Run the following command to create the deployment:

```
kubectl create deployment my-app --image=myacr.azurecr.io/my-app:v1
```

This will create a deployment named my-app that will manage a replica set of pods. The pods will be created from the my-app:v1 image that we pushed to ACR.

We can use the kubectl get deployments command to see the deployment that we just created:

```
kubectl get deployments
```

We can also use the kubectl get pods command to see the pods that are managed by the deployment:

```
kubectl get pods
```

## Exposing the Application

Now that our application is deployed, we need to expose it to the internet so that users can access it. We can do this by creating a Kubernetes service. A service is an abstraction that defines a logical set of pods and a policy by which to access them.

We will create a service of type LoadBalancer. This will create a load balancer in Azure and map it to the pods that are managed by the my-app deployment.

Run the following command to create the service:

```
kubectl expose deployment my-app --type=LoadBalancer --port=80 --target-port=8080
```

This will create a service named my-app that exposes port 80 on the load balancer. Traffic to this port will be forwarded to port 8080 on the pods that are managed by the my-app deployment.

We can use the kubectl get services command to see the service that we just created:

```
kubectl get services
```

Once the service has been created, it will take a few minutes for the load balancer to be provisioned and for the service to be assigned a public IP address. You can use the kubectl get services command to see the status of the service:

```
kubectl get services
```

Once the service has been created, you can use the public IP address to access the application in a web browser.

## Deleting the Cluster

If you no longer need the AKS cluster, you can delete it to stop incurring charges. To delete the cluster, run the following command:

```
az aks delete \
  --resource-group myResourceGroup \
  --name myAKSCluster
```

## Conclusion

In this article, we have shown you how to deploy a Kubernetes cluster on Azure using AKS. We have also shown you how to deploy a simple application to the cluster and expose it to the internet.