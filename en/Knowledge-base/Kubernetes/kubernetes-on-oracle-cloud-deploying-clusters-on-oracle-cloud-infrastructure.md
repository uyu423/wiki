---
title: Kubernetes on Oracle Cloud: Deploying Clusters on Oracle Cloud Infrastructure
description: 
published: true
date: 2023-02-01T11:57:48.421Z
tags: 
editor: markdown
dateCreated: 2023-02-01T11:57:46.959Z
---

- [Oracle Cloud의 Kubernetes: Oracle Cloud Infrastructure에 클러스터 배포***Korean** version of this document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-on-oracle-cloud-deploying-clusters-on-oracle-cloud-infrastructure)
{.links-list}
- [Oracle 云上的 Kubernetes：在 Oracle 云基础设施上部署集群***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-on-oracle-cloud-deploying-clusters-on-oracle-cloud-infrastructure)
{.links-list}


# Kubernetes on Oracle Cloud: Deploying Clusters on Oracle Cloud Infrastructure

Kubernetes is a popular open-source container orchestration platform that can be used to deploy and manage containerized applications at scale. Oracle Cloud Infrastructure (OCI) is a cloud computing platform offering a range of services, including compute, storage, and networking.

In this article, we'll show you how to deploy a Kubernetes cluster on Oracle Cloud Infrastructure. We'll cover the following topics:

- Creating an Oracle Cloud Infrastructure account
- Creating a Kubernetes cluster
- Deploying a sample application on the Kubernetes cluster

## Creating an Oracle Cloud Infrastructure Account

If you don't have an Oracle Cloud Infrastructure account, you can create one for free. To create an account:

1. Go to the [Oracle Cloud Infrastructure sign-up page](https://cloud.oracle.com/en_US/tryit).
2. Enter your information and click **Create Account**.
3. Follow the instructions to verify your account.

Once your account is verified, you can log in to the [Oracle Cloud Infrastructure console](https://console.us-ashburn-1.oraclecloud.com/a/billing).

## Creating a Kubernetes Cluster

 Oracle Cloud Infrastructure Container Engine for Kubernetes is a managed service that makes it easy to deploy and manage Kubernetes clusters on Oracle Cloud Infrastructure. With Container Engine for Kubernetes, you can create Kubernetes clusters in minutes.

To create a Kubernetes cluster:

1. Log in to the [Oracle Cloud Infrastructure console](https://console.us-ashburn-1.oraclecloud.com/a/billing).
2. In the navigation menu, click **Containers** and then click **Container Clusters**.
3. Click **Create Cluster**.
4. Enter the following information:

- **Name**: Enter a name for the cluster.
- **Kubernetes Version**: Select the Kubernetes version you want to use.
- **Network Options**:
  - **Virtual Cloud Network**: Create a new virtual cloud network or select an existing one.
  - **Subnet**: Create a new subnet or select an existing one.
  - **Public IP Address**: Create a new public IP address or select an existing one.
- **Node Pools**:
  - **Name**: Enter a name for the node pool.
  - **Kubernetes Version**: Select the Kubernetes version you want to use.
  - **Image Type**: Select the image type you want to use.
  - **Shape**: Select the shape you want to use.
  - **Initial Nodes**: Enter the number of nodes you want to create.
  - **Max Nodes**: Enter the maximum number of nodes you want to allow.
  - **Min Nodes**: Enter the minimum number of nodes you want to allow.
- **Storage Options**:
  - **Storage Class**: Select the storage class you want to use.
  - **Size (GB)**: Enter the size of the storage you want to use.
- **Node Metadata**:
  - **Labels**: Enter any labels you want to use.
  - **Annotations**: Enter any annotations you want to use.
- **Node Taints**: Enter any taints you want to use.
- **Service Accounts**: Enter any service accounts you want to use.
- **RBAC**: Select the RBAC options you want to use.

5. Click **Create Cluster**.

It will take a few minutes for the cluster to be created. Once the cluster is up and running, you can click **View Cluster** to see the details of the cluster.

## Deploying a Sample Application on the Kubernetes Cluster

Now that you have a Kubernetes cluster up and running, you can deploy a sample application on the cluster. To deploy the sample application:

1. Log in to the [Oracle Cloud Infrastructure console](https://console.us-ashburn-1.oraclecloud.com/a/billing).
2. In the navigation menu, click **Containers** and then click **Container Clusters**.
3. Click the name of the cluster you want to deploy the application on.
4. Click **Deploy Application**.
5. Enter the following information:

- **Application Type**: Select the type of application you want to deploy.
- **Application Name**: Enter a name for the application.
- **Image Name**: Enter the name of the image you want to use.
- **Image Tag**: Enter the tag of the image you want to use.
- **Image Pull Policy**: Select the image pull policy you want to use.
- **Command**: Enter the command you want to use.
- **Arguments**: Enter the arguments you want to use.
- **Environment Variables**: Enter the environment variables you want to use.
- **Working Directory**: Enter the working directory you want to use.
- **Ports**: Enter the ports you want to use.
- **Service Accounts**: Enter the service accounts you want to use.
- **Labels**: Enter the labels you want to use.
- **Annotations**: Enter the annotations you want to use.
- **Limits**: Enter the limits you want to use.
- **Requests**: Enter the requests you want to use.

6. Click **Deploy**.

It will take a few minutes for the application to be deployed. Once the application is deployed, you can click **View Application** to see the details of the application.

## Conclusion

In this article, we showed you how to deploy a Kubernetes cluster on Oracle Cloud Infrastructure. We also showed you how to deploy a sample application on the Kubernetes cluster.