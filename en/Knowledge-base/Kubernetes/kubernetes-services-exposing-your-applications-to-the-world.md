---
title: Kubernetes Services: Exposing Your Applications to the World
description: 
published: true
date: 2023-01-30T02:51:22.355Z
tags: 
editor: markdown
dateCreated: 2023-01-30T02:51:22.355Z
---

- [Kubernetes Services: 애플리케이션을 전 세계에 노출***Korean** version of this document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-services-exposing-your-applications-to-the-world)
{.links-list}


Kubernetes services are a powerful way to expose your applications to the world. By using services, you can easily map public DNS names to your applications, load balance traffic across multiple instances of your application, and secure your applications with SSL/TLS certificates. In this post, we'll take a look at how to use services to expose your applications to the world.

First, let's create a service. We'll use the nginx-demo service from the Kubernetes demos repository:

$ kubectl create -f https://raw.githubusercontent.com/kubernetes/kubernetes/master/examples/nginx-demo/nginx-demo-service.yaml

This will create a service named nginx-demo that points to the nginx-demo deployment. By default, the service will be exposed on a random port on the cluster's nodes. We can see this by running kubectl describe on the service:

$ kubectl describe service nginx-demo

Name: nginx-demo

Namespace: default

Labels: app=nginx-demo

Selector: app=nginx-demo

Type: NodePort

IP: 10.0.0.219

LoadBalancer IP:

Port: <unnamed> 80/TCP

NodePort: <unnamed> 30695/TCP

Endpoints: 10.244.1.2:80

Session Affinity: None

No events.

As you can see, the service is exposed on port 80 of the cluster's nodes. We can now access the service by pointing our browser to any of the nodes in the cluster. Let's say we have a node with IP address 10.0.0.1. We can now access the nginx-demo service by going to http://10.0.0.1:30695.

We can also expose the service on a specific port by using the --port flag:

$ kubectl expose deployment nginx-demo --port=80 --type=NodePort

This will create a service named nginx-demo that is exposed on port 80 of the cluster's nodes.

Now that we've seen how to use services to expose our applications, let's look at how to map public DNS names to our services. We'll use the nginx-demo service from the Kubernetes demos repository:

$ kubectl create -f https://raw.githubusercontent.com/kubernetes/kubernetes/master/examples/nginx-demo/nginx-demo-service.yaml

This will create a service named nginx-demo that points to the nginx-demo deployment. By default, the service will be exposed on a random port on the cluster's nodes. We can see this by running kubectl describe on the service:

$ kubectl describe service nginx-demo

Name: nginx-demo

Namespace: default

Labels: app=nginx-demo

Selector: app=nginx-demo

Type: NodePort

IP: 10.0.0.219

LoadBalancer IP:

Port: <unnamed> 80/TCP

NodePort: <unnamed> 30695/TCP

Endpoints: 10.244.1.2:80

Session Affinity: None

No events.

As you can see, the service is exposed on port 80 of the cluster's nodes. We can now access the service by pointing our browser to any of the nodes in the cluster. Let's say we have a node with IP address 10.0.0.1. We can now access the nginx-demo service by going to http://10.0.0.1:30695.

We can also expose the service on a specific port by using the --port flag:

$ kubectl expose deployment nginx-demo --port=80 --type=NodePort

This will create a service named nginx-demo that is exposed on port 80 of the cluster's nodes.

Now that we've seen how to use services to expose our applications, let's look at how to map public DNS names to our services. We'll use the nginx-demo service from the Kubernetes demos repository:

$ kubectl create -f https://raw.githubusercontent.com/kubernetes/kubernetes/master/examples/nginx-demo/nginx-demo-service.yaml

This will create a service named nginx-demo that points to the nginx-demo deployment. By default, the service will be exposed on a random port on the cluster's nodes. We can see this by running kubectl describe on the service:

$ kubectl describe service nginx-demo

Name: nginx-demo

Namespace: default

Labels: app=nginx-demo

Selector: app=nginx-demo

Type: NodePort

IP: 10.0.0.219

LoadBalancer IP:

Port: <unnamed> 80/TCP

NodePort: <unnamed> 30695/TCP

Endpoints: 10.244.1.2:80

Session Affinity: None

No events.

As you can see, the service is exposed on port 80 of the cluster's nodes. We can now access the service by pointing our browser to any of the nodes in the cluster. Let's say we have a node with IP address 10.0.0.1. We can now access the nginx-demo service by going to http://10.0.0.1:30695.

We can also expose the service on a specific port by using the --port flag:

$ kubectl expose deployment nginx-demo --port=80 --type=NodePort

This will create a service named nginx-demo that is exposed on port 80 of the cluster's nodes.

Now that we've seen how to use services to expose our applications, let's look at how to map public DNS names to our services. We'll use the nginx-demo service from the Kubernetes demos repository:

$ kubectl create -f https://raw.githubusercontent.com/kubernetes/kubernetes/master/examples/nginx-demo/nginx-demo-service.yaml

This will create a service named nginx-demo that points to the nginx-demo deployment. By default, the service will be exposed on a random port on the cluster's nodes. We can see this by running kubectl describe on the service:

$ kubectl describe service nginx-demo

Name: nginx-demo

Namespace: default

Labels: app=nginx-demo

Selector: app=nginx-demo

Type: NodePort

IP: 10.0.0.219

LoadBalancer IP:

Port: <unnamed> 80/TCP

NodePort: <unnamed> 30695/TCP

Endpoints: 10.244.1.2:80

Session Affinity: None

No events.

As you can see, the service is exposed on port 80 of the cluster's nodes. We can now access the service by pointing our browser to any of the nodes in the cluster. Let's say we have a node with IP address 10.0.0.1. We can now access the nginx-demo service by going to http://10.0.0.1:30695.

We can also expose the service on a specific port by using the --port flag:

$ kubectl expose deployment nginx-demo --port=80 --type=NodePort

This will create a service named nginx-demo that is exposed on port 80 of the cluster's nodes.

Now that we've seen how to use services to expose our applications, let's look at how to map public DNS names to our services. We'll use the nginx-demo service from the Kubernetes demos repository:

$ kubectl create -f https://raw.githubusercontent.com/kubernetes/kubernetes/master/examples/nginx-demo/nginx-demo-service.yaml

This will create a service named nginx-demo that points to the nginx-demo deployment. By default, the service will be exposed on a random port on the cluster's nodes. We can see this by running kubectl describe on the service:

$ kubectl describe service nginx-demo

Name: nginx-demo

Namespace: default

Labels: app=nginx-demo

Selector: app=nginx-demo

Type: NodePort

IP: 10.0.0.219

LoadBalancer IP:

Port: <unnamed> 80/TCP

NodePort: <unnamed> 30695/TCP

Endpoints: 10.244.1.2:80

Session Affinity: None

No events.

As you can see, the service is exposed on port 80 of the cluster's nodes. We can now access the service by pointing our browser to any of the nodes in the cluster. Let's say we have a node with IP address 10.0.0.1. We can now access the nginx-demo service by going to http://10.0.0.1:30695.

We can also expose the service on a specific port by using the --port flag:

$ kubectl expose deployment nginx-demo --port=80 --type=NodePort

This will create a service named nginx-demo that is exposed on port 80 of the cluster's nodes.

Now that we've seen how to use services to expose our applications, let's look at how to map public DNS names to our services. We'll use the nginx-demo service from the Kubernetes demos repository:

$ kubectl create -f https://raw.githubusercontent.com/kubernetes/kubernetes/master/examples/nginx-demo/nginx-demo-service.yaml

This will create a service named nginx-demo that points to the nginx-demo deployment. By default, the service will be exposed on a random port on the cluster's nodes. We can see this by running kubectl describe on the service:

$ kubectl describe service nginx-demo

Name: nginx-demo

Namespace: default

Labels: app=nginx-demo

Selector: app=nginx-demo

Type: NodePort

IP: 10.0.0.219

LoadBalancer IP:

Port: <unnamed> 80/TCP

NodePort: <unnamed> 30695/TCP

Endpoints: 10.244.1.2:80

Session Affinity: None

No events.

As you can see, the service is exposed on port 80 of the cluster's nodes. We can now access the service by pointing our browser to any of the nodes in the cluster. Let's say we have a node with IP address 10.0.0.1. We can now access the nginx-demo service by going to http://10.0.0.1:30695.

We can also expose the service on a specific port by using the --port flag:

$ kubectl expose deployment nginx-demo --port=80 --type=NodePort

This will create a service named nginx-demo that is exposed on port 80 of the cluster's nodes.

Now that we've seen how to use services to expose our applications, let's look at how to map public DNS names to our services. We'll use the nginx-demo service from the Kubernetes demos repository:

$ kubectl create -f https://raw.githubusercontent.com/kubernetes/kubernetes/master/examples/nginx-demo/nginx-demo-service.yaml

This will create a service named nginx-demo that points to the nginx-demo deployment. By default, the service will be exposed on a random port on the cluster's nodes. We can see this by running kubectl describe on the service:

$ kubectl describe service nginx-demo

Name: nginx-demo

Namespace: default

Labels: app=nginx-demo

Selector: app=nginx-demo

Type: NodePort

IP: 10.0.0.219

LoadBalancer IP:

Port: <unnamed> 80/TCP

NodePort: <unnamed> 30695/TCP

Endpoints: 10.244.1.2:80

Session Affinity: None

No events.

As you can see, the service is exposed on port 80 of the cluster's nodes. We can now access the service by pointing our browser to any of the nodes in the cluster. Let's say we have a node with IP address 10.0.0.1. We can now access the nginx-demo service by going to http://10.0.0.1:30695.

We can also expose the service on a specific port by using the --port flag:

$ kubectl expose deployment nginx-demo --port=80 --type=NodePort

This will create a service named nginx-demo that is exposed on port 80 of the cluster's nodes.

Now that we've seen how to use services to expose our applications, let's look at how to map public DNS names to our services. We'll use the nginx-demo service from the Kubernetes demos repository:

$ kubectl create -f https://raw.githubusercontent.com/kubernetes/kubernetes/master/examples/nginx-demo/nginx-demo-service.yaml

This will create a service named nginx-demo that points to the nginx-demo deployment. By default, the service will be exposed on a random port on the cluster's nodes. We can see this by running kubectl describe on the service:

$ kubectl describe service nginx-demo

Name: nginx-demo

Namespace: default

Labels: app=nginx-demo

Selector: app=nginx-demo

Type: NodePort

IP: 10.0.0.219

LoadBalancer IP:

Port: <unnamed> 80/TCP

NodePort: <unnamed> 30695/TCP

Endpoints: 10.244.1.2:80

Session Affinity: None

No events.

As you can see, the service is exposed on port 80 of the cluster's nodes. We can now access the service by pointing our browser to any of the nodes in the cluster.