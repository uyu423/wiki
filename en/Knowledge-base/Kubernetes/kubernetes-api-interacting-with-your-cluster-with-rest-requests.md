---
title: Kubernetes API: Interacting with Your Cluster with REST Requests
description: 
published: true
date: 2023-02-14T03:33:39.194Z
tags: 
editor: markdown
dateCreated: 2023-02-14T03:33:30.965Z
---

- [API de Kubernetes: interacción con su clúster con solicitudes REST***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-api-interacting-with-your-cluster-with-rest-requests)
{.links-list}
- [Kubernetes API：通过 REST 请求与集群交互***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-api-interacting-with-your-cluster-with-rest-requests)
{.links-list}
- [Kubernetes API: REST 요청으로 클러스터와 상호 작용***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-api-interacting-with-your-cluster-with-rest-requests)
{.links-list}


# Kubernetes API: Interacting with Your Cluster with REST Requests

In this article, we'll take a look at how to use the Kubernetes API to interact with your Kubernetes cluster. We'll cover the basics of making REST requests to the Kubernetes API, and we'll look at some of the most common API resources and operations.

## Making REST Requests

The Kubernetes API is a [RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer) API, which means that you can use any HTTP client to make requests to the API. All you need to do is send an HTTP request to the appropriate API endpoint, and the Kubernetes API will respond with the requested data.

To make a request to the Kubernetes API, you need to know the URL of the API endpoint that you want to call, and you need to specify the HTTP method that you want to use. The most common HTTP methods are `GET`, `POST`, `PUT`, and `DELETE`.

For example, to get a list of all the pods in a namespace, you would make a `GET` request to the `/api/v1/namespaces/{namespace}/pods` endpoint. To create a new pod, you would make a `POST` request to the same endpoint.

In addition to the URL and the HTTP method, you also need to specify an [HTTP header](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields) called `Authorization` with a value of `Bearer {token}`, where `{token}` is a valid Kubernetes API token. You can get a Kubernetes API token by running the `kubectl get secrets` command.

## Common API Resources

Now that we've covered the basics of making REST requests to the Kubernetes API, let's take a look at some of the most common API resources.

### Pods

Pods are the smallest deployable units in Kubernetes, and they are always co-located and co-scheduled together on the same node. A pod represents a single instance of an application, and it can contain one or more containers.

To get a list of all the pods in a namespace, you can make a `GET` request to the `/api/v1/namespaces/{namespace}/pods` endpoint. To get the details of a specific pod, you can make a `GET` request to the `/api/v1/namespaces/{namespace}/pods/{name}` endpoint.

To create a new pod, you can make a `POST` request to the `/api/v1/namespaces/{namespace}/pods` endpoint. The request body should be a [JSON](https://www.json.org/) or [YAML](https://yaml.org/) object that specifies the pod specification.

Here's an example of a pod specification in JSON:

```json
{
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "nginx-pod",
    "labels": {
      "app": "nginx"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "nginx",
        "image": "nginx:1.7.9",
        "ports": [
          {
            "containerPort": 80
          }
        ]
      }
    ]
  }
}
```

And here's the same specification in YAML:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.7.9
    ports:
    - containerPort: 80
```

To update a pod, you can make a `PUT` or `PATCH` request to the `/api/v1/namespaces/{namespace}/pods/{name}` endpoint. The request body should be a JSON or YAML object that specifies the pod specification.

To delete a pod, you can make a `DELETE` request to the `/api/v1/namespaces/{namespace}/pods/{name}` endpoint.

### Replica Sets

Replica sets are a [Kubernetes resource](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) that ensures that a specified number of pod replicas are always running. If a pod is deleted or crashes, the replica set will ensure that a new pod is created to replace it.

To get a list of all the replica sets in a namespace, you can make a `GET` request to the `/apis/apps/v1/namespaces/{namespace}/replicasets` endpoint. To get the details of a specific replica set, you can make a `GET` request to the `/apis/apps/v1/namespaces/{namespace}/replicasets/{name}` endpoint.

To create a new replica set, you can make a `POST` request to the `/apis/apps/v1/namespaces/{namespace}/replicasets` endpoint. The request body should be a JSON or YAML object that specifies the replica set specification.

Here's an example of a replica set specification in JSON:

```json
{
  "apiVersion": "apps/v1",
  "kind": "ReplicaSet",
  "metadata": {
    "name": "nginx-replicaset",
    "labels": {
      "app": "nginx"
    }
  },
  "spec": {
    "replicas": 3,
    "selector": {
      "matchLabels": {
        "app": "nginx"
      }
    },
    "template": {
      "metadata": {
        "labels": {
          "app": "nginx"
        }
      },
      "spec": {
        "containers": [
          {
            "name": "nginx",
            "image": "nginx:1.7.9",
            "ports": [
              {
                "containerPort": 80
              }
            ]
          }
        ]
      }
    }
  }
}
```

And here's the same specification in YAML:

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
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
```

To update a replica set, you can make a `PUT` or `PATCH` request to the `/apis/apps/v1/namespaces/{namespace}/replicasets/{name}` endpoint. The request body should be a JSON or YAML object that specifies the replica set specification.

To delete a replica set, you can make a `DELETE` request to the `/apis/apps/v1/namespaces/{namespace}/replicasets/{name}` endpoint.

### Deployments

[Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) are a higher-level resource that manage replica sets and provide a declarative way to specify the desired state of your pods. A deployment defines a replica set and ensures that the specified number of replicas are always running.

To get a list of all the deployments in a namespace, you can make a `GET` request to the `/apis/apps/v1/namespaces/{namespace}/deployments` endpoint. To get the details of a specific deployment, you can make a `GET` request to the `/apis/apps/v1/namespaces/{namespace}/deployments/{name}` endpoint.

To create a new deployment, you can make a `POST` request to the `/apis/apps/v1/namespaces/{namespace}/deployments` endpoint. The request body should be a JSON or YAML object that specifies the deployment specification.

Here's an example of a deployment specification in JSON:

```json
{
  "apiVersion": "apps/v1",
  "kind": "Deployment",
  "metadata": {
    "name": "nginx-deployment",
    "labels": {
      "app": "nginx"
    }
  },
  "spec": {
    "replicas": 3,
    "selector": {
      "matchLabels": {
        "app": "nginx"
      }
    },
    "template": {
      "metadata": {
        "labels": {
          "app": "nginx"
        }
      },
      "spec": {
        "containers": [
          {
            "name": "nginx",
            "image": "nginx:1.7.9",
            "ports": [
              {
                "containerPort": 80
              }
            ]
          }
        ]
      }
    }
  }
}
```

And here's the same specification in YAML:

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
```

To update a deployment, you can make a `PUT` or `PATCH` request to the `/apis/apps/v1/namespaces/{namespace}/deployments/{name}` endpoint. The request body should be a JSON or YAML object that specifies the deployment specification.

To delete a deployment, you can make a `DELETE` request to the `/apis/apps/v1/namespaces/{namespace}/deployments/{name}` endpoint.

## Conclusion

In this article, we've covered the basics of interacting with the Kubernetes API using REST requests. We've looked at some of the most common API resources, and we've seen how to use the Kubernetes API to create, read, update, and delete those resources.