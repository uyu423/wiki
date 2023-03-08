---
title: Kubernetes on DigitalOcean: Deploying Clusters on DigitalOcean
description: 
published: true
date: 2023-02-17T18:03:00.037Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:26:55.615Z
---

- [DigitalOcean의 Kubernetes: DigitalOcean에 클러스터 배포***Korean** version of this document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-on-digitalocean-deploying-clusters-on-digitalocean)
{.links-list}
- [DigitalOcean での Kubernetes: DigitalOcean でのクラスターのデプロイ***Japanese** version of this document is available*](/ja/Knowledge-base/Kubernetes/kubernetes-on-digitalocean-deploying-clusters-on-digitalocean)
{.links-list}
- [DigitalOcean 上的 Kubernetes：在 DigitalOcean 上部署集群***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-on-digitalocean-deploying-clusters-on-digitalocean)
{.links-list}


# Kubernetes on DigitalOcean: Deploying Clusters on DigitalOcean

Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. It is portable and extensible, and provides a foundation for building cluster management solutions.

DigitalOcean is a cloud computing platform that provides virtual private servers (VPSs) and other cloud services. It is a popular choice for hosting web applications and microservices.

This article provides an overview of deploying Kubernetes clusters on DigitalOcean. It covers provisioning resources, configuring networking, and deploying applications.

## Provisioning Resources

DigitalOcean provides a Kubernetes service that makes it easy to provision resources and deploy Kubernetes clusters. The first step is to create a Kubernetes cluster. This can be done through the control panel or the API.

Once the cluster is created, you will need to add nodes to it. Nodes can be added manually or automatically. Automatic node provisioning is available for clusters with three or more nodes.

## Configuring Networking

Kubernetes clusters on DigitalOcean are deployed with a private network by default. This network is isolated from the public Internet, and can only be accessed from within the cluster.

To access services on the Internet, you will need to configure a gateway. This can be done through the Kubernetes dashboard or the API.

If you need to access services on-premises, you will need to configure a VPN. DigitalOcean provides an IPsec VPN service that can be used to connect to on-premises resources.

## Deploying Applications

To deploy an application on a Kubernetes cluster, you will need to create a deployment. This can be done through the Kubernetes dashboard or the API.

Once the deployment is created, you will need to specify the container image to use and the port to expose. You can also specify environment variables and other options.

After the deployment is created, you will need to create a service. This will expose the deployment to the outside world. The service can be created through the Kubernetes dashboard or the API.

Once the service is created, you will need to specify the type of service (LoadBalancer, ClusterIP, or NodePort), and the port to expose. You can also specify other options, such as the name of the service.

## Conclusion

This article has covered the basics of deploying Kubernetes clusters on DigitalOcean. It has shown how to provision resources, configure networking, and deploy applications.