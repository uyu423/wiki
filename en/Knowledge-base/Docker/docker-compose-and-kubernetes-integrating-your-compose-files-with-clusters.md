---
title: Docker Compose and Kubernetes: Integrating Your Compose Files with Clusters
description: 
published: true
date: 2023-02-17T18:02:27.355Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:24:42.379Z
---

- [Docker Compose 및 Kubernetes: Compose 파일을 클러스터와 통합***Korean** version of this document is available*](/ko/Knowledge-base/Docker/docker-compose-and-kubernetes-integrating-your-compose-files-with-clusters)
{.links-list}



# Docker Compose and Kubernetes: Integrating Your Compose Files with Clusters

In this article, we're going to take a look at how to use Docker Compose and Kubernetes together. We'll start by looking at why you might want to use both together. We'll then take a look at an example of how to use Compose files with Kubernetes.

Docker Compose is a great tool for development. It allows you to define your application's environment with a YAML file, and then spin up your application with a single command.

Kubernetes is a great tool for deploying and managing containerized applications at scale. It allows you to define your application's desired state, and then it ensures that your application always matches that desired state.

One of the great things about Kubernetes is that it can run anywhere - on your laptop, on a server, or in the cloud. This means that you can use Kubernetes to manage your development environment, as well as your production environment.

If you're using Docker Compose for development, and you want to deploy your application to Kubernetes, you'll need to use a tool to generate a Kubernetes Manifest file from your Compose file. This Manifest file will define your application's desired state, and Kubernetes will use it to ensure that your application always matches that desired state.

There are a few tools that can generate Kubernetes Manifest files from Compose files, but we're going to use Kompose. Kompose is a tool that's specifically designed for converting Compose files to Kubernetes Manifest files.

To use Kompose, you need to have both Docker and Kubernetes installed. If you don't already have Kubernetes installed, you can use Minikube. Minikube is a tool that allows you to run a single-node Kubernetes cluster on your laptop.

Once you have Docker and Kubernetes installed, you can install Kompose with the following command:

```
curl -L https://github.com/kubernetes/kompose/releases/download/v1.19.0/kompose-linux-amd64 -o /usr/local/bin/kompose
```

Once Kompose is installed, you can use it to generate a Kubernetes Manifest file from a Compose file with the following command:

```
kompose -f /path/to/compose/file.yml -o /path/to/manifest/file.yml
```

This will generate a Kubernetes Manifest file called `file.yml` in the `/path/to/manifest/` directory.

Once you have your Kubernetes Manifest file, you can deploy your application to Kubernetes with the `kubectl` command. The `kubectl` command is the command-line interface for Kubernetes.

To deploy your application, you need to have a Kubernetes cluster. If you're using Minikube, you can start a Kubernetes cluster with the following command:

```
minikube start
```

Once your Kubernetes cluster is running, you can deploy your application to it with the following command:

```
kubectl apply -f /path/to/manifest/file.yml
```

This will deploy your application to Kubernetes. Once your application is deployed, you can use the `kubectl` command to manage it. For example, you can use the `kubectl` command to list the pods in your deployment with the following command:

```
kubectl get pods
```

You can also use the `kubectl` command to get more information about a specific pod. For example, to get more information about the first pod in the list, you can use the following command:

```
kubectl describe pod pod-name
```

Once your application is running in Kubernetes, you can access it using the `kubectl` command. For example, to get the URL of your application, you can use the following command:

```
kubectl get service my-app-name
```

This will output the URL of your application. You can then access your application at that URL.

## Integrating Compose Files with Kubernetes

Now that we've looked at why you might want to use Docker Compose and Kubernetes together, let's look at how you can use Compose files with Kubernetes.

We're going to use the `kompose` command to generate a Kubernetes Manifest file from a Compose file. We're going to use the `docker-compose.yml` file from the [Docker Compose documentation](https://docs.docker.com/compose/).

To generate a Kubernetes Manifest file from this Compose file, we can use the following command:

```
kompose -f docker-compose.yml -o kubernetes.yml
```

This will generate a Kubernetes Manifest file called `kubernetes.yml` in the current directory.

Let's take a look at what's in this file. The first thing you'll notice is that there's a `apiVersion: extensions/v1beta1` line at the top of the file. This line tells Kubernetes that we're using the `extensions/v1beta1` API version.

Next, we have a `kind: Deployment` line. This line tells Kubernetes that we're going to be creating a deployment. A deployment is a Kubernetes object that represents a group of pods.

After that, we have a `metadata` section. This section contains metadata about our deployment. The only thing we need to worry about in this section is the `name` field. This field contains the name of our deployment. In this case, the name of our deployment is `compose-example`.

Next, we have a `spec` section. This section contains the specification of our deployment. The first thing we need to specify is the `replicas` field. This field tells Kubernetes how many pods we want to run in our deployment. In this case, we're going to run two pods.

After that, we have a `selector` section. This section tells Kubernetes which pods to include in our deployment. In this case, we're going to include all pods that have a `app=web` label.

Next, we have a `template` section. This section contains the definition of our pod template. A pod template is a Kubernetes object that defines the configuration of our pod.

The first thing we need to define in our pod template is the `metadata` section. This section contains metadata about our pod. The only thing we need to worry about in this section is the `labels` field. This field contains the labels that will be applied to our pod. In this case, we're going to apply the `app=web` label to our pod.

After that, we have a `spec` section. This section contains the specification of our pod. The first thing we need to specify in this section is the `containers` field. This field contains a list of the containers that will be run in our pod. In this case, we're only going to run one container.

Next, we have the definition of our container. The first thing we need to define is the `name` of our container. In this case, we're going to call our container `web`.

After that, we have the `image` field. This field tells Kubernetes which docker image to use for our container. In this case, we're going to use the `nginx` docker image.

Next, we have the `ports` field. This field tells Kubernetes which ports to expose from our container. In this case, we're going to expose port `80`.

Finally, we have the `resources` field. This field allows us to specify the resources that our container needs. In this case, we're going to specify that our container needs `200m` of CPU and `128Mi` of memory.

This is everything that's required to define a pod. Once you have a pod defined, you can create a deployment by running the following command:

```
kubectl apply -f kubernetes.yml
```

This will create a deployment called `compose-example`. You can view the deployment by running the following command:

```
kubectl get deployments
```

You can also view the pods that are part of the deployment by running the following command:

```
kubectl get pods
```

You can use the `kubectl` command to get more information about a specific pod. For example, to get more information about the first pod in the list, you can use the following command:

```
kubectl describe pod pod-name
```

Once your application is running in Kubernetes, you can access it using the `kubectl` command. For example, to get the URL of your application, you can use the following command:

```
kubectl get service compose-example
```

This will output the URL of your application. You can then access your application at that URL.

## Conclusion

In this article, we've looked at how to use Docker Compose and Kubernetes together. We've seen how to use Kompose to generate a Kubernetes Manifest file from a Compose file. We've also seen how to use the `kubectl` command to deploy our application to Kubernetes.