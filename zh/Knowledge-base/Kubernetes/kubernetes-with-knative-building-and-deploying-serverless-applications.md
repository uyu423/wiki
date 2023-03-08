---
title: Kubernetes 与 Knative：构建和部署无服务器应用程序
description: 
published: true
date: 2023-02-12T02:17:42.614Z
tags: 
editor: markdown
dateCreated: 2023-02-12T02:17:36.014Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes with Knative: Building and Deploying Serverless Applications***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-knative-building-and-deploying-serverless-applications)
{.links-list}


# Kubernetes 与 Knative：构建和部署无服务器应用程序

在本文中，我们将探讨如何使用 Kubernetes 和 Knative 来构建和部署无服务器应用程序。我们将从简要概述无服务器计算和 Kubernetes 开始，然后了解 Knative 如何融入 Kubernetes 生态系统。然后，我们将介绍一个使用 Kubernetes 和 Knative 构建和部署无服务器应用程序的简单示例。

## 什么是无服务器计算？

无服务器计算是一种云计算执行模型，其中云提供商运行服务器，客户只需为使用的计算时间付费。无服务器计算是一种按需提供后端服务的方式。

有两种类型的无服务器计算：

- 功能即服务 (FaaS)：按需运行用户提供的代码的服务。
- 后端即服务 (BaaS)：为应用程序提供后端的服务，例如推送通知或存储。

## 什么是 Kubernetes？

Kubernetes 是一个可移植、可扩展的开源平台，用于管理容器化工作负载和服务，可促进声明式配置和自动化。它有一个庞大的、快速发展的生态系统。 Kubernetes 服务、支持和工具广泛可用，包括托管 Kubernetes 解决方案。

## 什么是 Knative？

Knative 是一组开源组件，可扩展 Kubernetes 以提供无服务器工作负载的平台。 Knative 由三个组件组成：

- 服务：一组在 Kubernetes 上提供无服务器平台的组件，包括 HTTP 代理和自动扩展计算资源。
- 构建：一组提供无服务器容器镜像构建的组件。
- 事件：一组提供事件驱动的消息传递和流的组件。

Knative 旨在与任何可以运行 Kubernetes 的容器编排器配合使用，包括 Google Kubernetes Engine (GKE)、Azure Kubernetes Service (AKS) 和 Amazon Elastic Container Service for Kubernetes (EKS)。

## 在 Kubernetes 上构建和部署无服务器应用程序

在本节中，我们将介绍一个使用 Knative 在 Kubernetes 上构建和部署无服务器应用程序的示例。我们将使用一个用 Go 编写的简单的“Hello, World”示例。

首先，我们将使用以下代码创建一个名为 `main.go` 的文件：

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

接下来，我们将创建一个包含以下内容的 `Dockerfile`：

```
FROM golang:1.11

WORKDIR /go/src/app

COPY . .

RUN go get -d -v ./...
RUN go install -v ./...

CMD ["app"]
```

现在我们有了代码和 Dockerfile，我们可以构建容器镜像并将其推送到容器注册表：

```
$ docker build -t gcr.io/<project-id>/helloworld:v1 .
$ docker push gcr.io/<project-id>/helloworld:v1
```

将 `<project-id>` 替换为您的 Google Cloud Platform 项目 ID。

将容器镜像推送到注册表后，我们可以使用 `kubectl` 命令将其部署到 Kubernetes：

```
$ kubectl apply -f helloworld.yaml
```

其中 `helloworld.yaml` 是一个包含以下内容的 YAML 文件：

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

部署服务后，我们可以查看应用程序的 URL：

```
$ kubectl get ksvc
NAME            URL                                                 LATESTCREATED          LATESTREADY             READY     REASON
helloworld      http://helloworld-default.default.svc.cluster.local   helloworld-00001-00000   helloworld-00001-00000   True
```

我们可以通过卷曲 URL 来测试它：

```
$ curl http://helloworld-default.default.svc.cluster.local
Hello, World!
```

## 结论

在本文中，我们探讨了如何结合使用 Kubernetes 和 Knative 来构建和部署无服务器应用程序。我们了解了什么是无服务器计算，以及 Knative 如何融入 Kubernetes 生态系统。最后，我们介绍了一个使用 Kubernetes 和 Knative 构建和部署无服务器应用程序的简单示例。