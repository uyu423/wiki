---
title: Kubernetes with Knative: Building and Deploying Serverless Applications
description: 
published: true
date: 2023-02-12T02:17:37.666Z
tags: 
editor: markdown
dateCreated: 2023-02-12T02:17:36.018Z
---

- [Kubernetes con Knative: creación e implementación de aplicaciones sin servidor***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-with-knative-building-and-deploying-serverless-applications)
{.links-list}
- [Kubernetes 与 Knative：构建和部署无服务器应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-with-knative-building-and-deploying-serverless-applications)
{.links-list}
- [Knative를 사용한 Kubernetes: 서버리스 애플리케이션 구축 및 배포***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-with-knative-building-and-deploying-serverless-applications)
{.links-list}


# Kubernetes with Knative: Building and Deploying Serverless Applications

In this article, we'll explore how to use Kubernetes with Knative to build and deploy serverless applications. We'll start with a brief overview of serverless computing and Kubernetes, followed by a look at how Knative fits into the Kubernetes ecosystem. Then, we'll walk through a simple example of building and deploying a serverless application using Kubernetes and Knative.

## What is Serverless Computing?

Serverless computing is a cloud computing execution model in which the cloud provider runs the server, and the customer pays only for the used compute time. Serverless computing is a way to provide backend services on an as-needed basis.

There are two types of serverless computing:

- Function as a Service (FaaS): A service that runs user-provided code on demand.
- Backend as a Service (BaaS): A service that provides a backend for applications, such as push notifications or storage.

## What is Kubernetes?

Kubernetes is a portable, extensible open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available, including hosted Kubernetes solutions.

## What is Knative?

Knative is a set of open source components that extend Kubernetes to provide a platform for serverless workloads. Knative consists of three components:

- Serving: A set of components that provides a serverless platform on Kubernetes, including an HTTP proxy and automatically scaling compute resources.
- Build: A set of components that provides serverless container image builds.
- Eventing: A set of components that provides event-driven messaging and streaming.

Knative is designed to work with any container orchestrator that can run Kubernetes, including Google Kubernetes Engine (GKE), Azure Kubernetes Service (AKS), and Amazon Elastic Container Service for Kubernetes (EKS).

## Building and Deploying a Serverless Application on Kubernetes

In this section, we'll walk through an example of building and deploying a serverless application on Kubernetes using Knative. We'll use a simple "Hello, World" example written in Go.

First, we'll create a file named `main.go` with the following code:

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, World!")
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}
```

Next, we'll create a `Dockerfile` with the following contents:

```
FROM golang:1.11

WORKDIR /go/src/app

COPY . .

RUN go get -d -v ./...
RUN go install -v ./...

CMD ["app"]
```

Now that we have our code and `Dockerfile`, we can build our container image and push it to a container registry:

```
$ docker build -t gcr.io/<project-id>/helloworld:v1 .
$ docker push gcr.io/<project-id>/helloworld:v1
```

Replace `<project-id>` with your Google Cloud Platform project ID.

Once the container image is pushed to the registry, we can deploy it to Kubernetes using the `kubectl` command:

```
$ kubectl apply -f helloworld.yaml
```

Where `helloworld.yaml` is a YAML file with the following contents:

```yaml
apiVersion: serving.knative.dev/v1
kind: Service
metadata:
  name: helloworld
  namespace: default
spec:
  template:
    spec:
      containers:
        - image: gcr.io/<project-id>/helloworld:v1
          env:
            - name: TARGET
              value: "World"
```

Once the service is deployed, we can view the URL for our application:

```
$ kubectl get ksvc
NAME            URL                                                 LATESTCREATED          LATESTREADY             READY     REASON
helloworld      http://helloworld-default.default.svc.cluster.local   helloworld-00001-00000   helloworld-00001-00000   True
```

And we can test it by curl-ing the URL:

```
$ curl http://helloworld-default.default.svc.cluster.local
Hello, World!
```

## Conclusion

In this article, we've explored how to use Kubernetes with Knative to build and deploy serverless applications. We've looked at what serverless computing is, and how Knative fits into the Kubernetes ecosystem. Finally, we've walked through a simple example of building and deploying a serverless application using Kubernetes and Knative.