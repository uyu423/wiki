---
title: Kubernetes on Google Cloud: Deploying Clusters on Google Cloud Platform
description: 
published: true
date: 2023-02-14T05:33:07.877Z
tags: 
editor: markdown
dateCreated: 2023-02-14T05:33:05.645Z
---

- [Kubernetes en Google Cloud: implementación de clústeres en Google Cloud Platform***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-on-google-cloud-deploying-clusters-on-google-cloud-platform)
{.links-list}
- [Google Cloud 上的 Kubernetes：在 Google Cloud Platform 上部署集群***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-on-google-cloud-deploying-clusters-on-google-cloud-platform)
{.links-list}
- [Google Cloud의 Kubernetes: Google Cloud Platform에 클러스터 배포***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-on-google-cloud-deploying-clusters-on-google-cloud-platform)
{.links-list}


# Kubernetes on Google Cloud: Deploying Clusters on Google Cloud Platform

Kubernetes is an open-source system for automating the deployment, scaling, and management of containerized applications. It groups containers that make up an application into logical units for easy management and discovery. Kubernetes is hosted on Google Cloud Platform (GCP) and is used to orchestrate and manage containers deployed on GCP.

Kubernetes on GCP is a scalable, reliable, and cost-effective way to deploy your containerized applications. GCP offers many benefits over other cloud providers, including pay-as-you-go pricing, per-minute billing, and no upfront costs. You can also use Kubernetes on GCP to manage your on-premises workloads.

In this article, we will show you how to deploy a Kubernetes cluster on GCP. We will also show you how to deploy a simple application on your Kubernetes cluster.

## Prerequisites

- A Google Cloud account
- A project created in the Google Cloud Console
- The gcloud command-line tool installed on your local machine
- Basic knowledge of Kubernetes

## Creating a Kubernetes Cluster

A Kubernetes cluster consists of a set of nodes, each of which is a physical or virtual machine that runs the Kubernetes components. There are two types of nodes in a Kubernetes cluster:

- **Master nodes**: These nodes are responsible for the management of the Kubernetes cluster. They provide the API server, scheduler, and controller-manager components.
- **Worker nodes**: These nodes run the applications that are deployed on the Kubernetes cluster.

In this section, we will show you how to create a Kubernetes cluster with three nodes: one master node and two worker nodes.

### Creating the Master Node

1. Log in to the Google Cloud Console and go to the **Compute Engine** > **VM instances** page.
2. Click the **Create instance** button.
3. In the **Name** field, enter **kubernetes-master**.
4. In the **Zone** field, select a zone that is close to your location.
5. In the **Machine type** field, select **n1-standard-1**.
6. In the **Boot disk** section, click **Change**.
7. In the **Boot disk** section, select **Ubuntu 16.04 LTS** from the **Operating system** drop-down list.
8. In the **Boot disk type** drop-down list, select **SSD (persistent disk)**.
9. In the **Boot disk size** field, enter **10GB**.
10. Click the **Select** button.
11. In the **Firewall** section, select the **Allow HTTP traffic** checkbox.
12. Click the **Create** button.

Your master node should now be created.

### Creating the Worker Nodes

1. Log in to the Google Cloud Console and go to the **Compute Engine** > **VM instances** page.
2. Click the **Create instance** button.
3. In the **Name** field, enter **kubernetes-worker-1**.
4. In the **Zone** field, select the same zone that you selected for the master node.
5. In the **Machine type** field, select **n1-standard-1**.
6. In the **Boot disk** section, click **Change**.
7. In the **Boot disk** section, select **Ubuntu 16.04 LTS** from the **Operating system** drop-down list.
8. In the **Boot disk type** drop-down list, select **SSD (persistent disk)**.
9. In the **Boot disk size** field, enter **10GB**.
10. Click the **Select** button.
11. In the **Firewall** section, select the **Allow HTTP traffic** checkbox.
12. Click the **Create** button.

Repeat the above steps to create a second worker node, but use **kubernetes-worker-2** as the name for the second node.

Your worker nodes should now be created.

## Installing Kubernetes

In this section, we will show you how to install Kubernetes on your master node.

1. Log in to your master node using SSH.
2. Run the following command to add the Kubernetes apt repository:

```
$ sudo apt-get install -y apt-transport-https
3. Run the following command to add the Kubernetes GPG key:

```
$ curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
4. Run the following command to add the Kubernetes repository:

```
$ sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
5. Update the package list:

```
$ sudo apt-get update
6. Install Kubernetes:

```
$ sudo apt-get install -y kubelet kubeadm kubectl
7. Once the installation is complete, run the following command to start the Kubernetes master node:

```
$ sudo kubeadm init
8. Run the following command to configure kubectl:

```
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config
9. Your Kubernetes master node should now be up and running.

## Joining Worker Nodes to the Cluster

In this section, we will show you how to join your worker nodes to the Kubernetes cluster.

1. Log in to your master node using SSH.
2. Run the following command to get the join command:

```
$ sudo kubeadm token create --print-join-command
3. Log in to your worker nodes using SSH.
4. Run the join command that you got in the previous step on each of your worker nodes.
5. Your worker nodes should now be joined to the Kubernetes cluster.

## Deploying an Application

In this section, we will show you how to deploy a simple application on your Kubernetes cluster.

1. Log in to your master node using SSH.
2. Create a file named **nginx-deployment.yaml** with the following contents:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
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
3. Run the following command to deploy the application:

```
$ kubectl create -f nginx-deployment.yaml
4. Run the following command to list the deployed pods:

```
$ kubectl get pods
5. Run the following command to expose the deployment:

```
$ kubectl expose deployment nginx-deployment --type=LoadBalancer --port=80 --target-port=80
6. Run the following command to get the service URL:

```
$ kubectl get service nginx-deployment
7. Access the application using the service URL. You should see the default Nginx page.

Your application is now deployed on your Kubernetes cluster.

## Deleting the Cluster

In this section, we will show you how to delete the Kubernetes cluster.

1. Log in to your master node using SSH.
2. Run the following command to delete the cluster:

```
$ sudo kubeadm reset
3. Delete the master node:

```
$ gcloud compute instances delete kubernetes-master
4. Delete the worker nodes:

```
$ gcloud compute instances delete kubernetes-worker-1
$ gcloud compute instances delete kubernetes-worker-2
5. Your Kubernetes cluster should now be deleted.

## Conclusion

In this article, we have shown you how to deploy a Kubernetes cluster on GCP. We have also shown you how to deploy a simple application on your Kubernetes cluster.