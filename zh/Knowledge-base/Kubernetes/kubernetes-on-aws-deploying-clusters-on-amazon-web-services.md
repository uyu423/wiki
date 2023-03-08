---
title: AWS 上的 Kubernetes：在 Amazon Web Services 上部署集群
description: 
published: true
date: 2023-02-01T00:06:05.590Z
tags: 
editor: markdown
dateCreated: 2023-02-01T00:06:03.908Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Kubernetes on AWS: Deploying Clusters on Amazon Web Services***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-aws-deploying-clusters-on-amazon-web-services)
{.links-list}



# AWS 上的 Kubernetes：在 Amazon Web Services 上部署集群

Kubernetes 是一个开源容器编排系统，用于自动化应用程序部署、扩展和管理。它将构成应用程序的容器分组为逻辑单元，以便于管理和发现。

AWS 是亚马逊提供的一个综合的、不断发展的云计算平台。它提供基础架构即服务 (IaaS)、平台即服务 (PaaS) 和打包软件即服务 (SaaS) 产品组合。

您可以使用 AWS 上的 Kubernetes 在 AWS 上部署、管理和扩展容器化应用程序。在本文中，我们将向您展示如何在 AWS 上部署 Kubernetes 集群。

##先决条件

要遵循本指南，您需要具备以下条件：

- AWS 账户。如果您没有，可以在 [此处](https://aws.amazon.com/) 创建一个。

- 在您的机器上安装和配置的 AWS 命令行界面 (CLI)。您可以在 [此处](https://docs.aws.amazon.com/cli/latest/userguide/installing.html) 找到有关如何操作的说明。

- 安装在您机器上的 kubectl 命令行工具。您可以在 [此处](https://kubernetes.io/docs/tasks/tools/install-kubectl/) 找到有关如何执行此操作的说明。

- 一个域名。您可以通过 [Freenom](https://www.freenom.com/) 等服务免费获得一个。

## 设置 AWS Kubernetes 集群

有多种方法可以在 AWS 上设置 Kubernetes 集群。在本文中，我们将使用 AWS 管理控制台来设置我们的集群。

首先，登录 AWS 管理控制台并导航到 Amazon EKS 服务。

![](https://i.imgur.com/LDAd5u8.png)

单击“创建集群”按钮。

![](https://i.imgur.com/p0bJUO4.png)

在下一页上，为您的集群输入一个名称并选择您要将其部署到的区域。然后，选择您要使用的 Kubernetes 版本。我们将使用最新版本，在撰写本文时为 1.17。

![](https://i.imgur.com/Ft7YIxu.png)

接下来，我们需要配置我们的工作节点。工作节点是我们集群中将运行我们的应用程序的机器。我们将为工作节点使用 Amazon EC2 实例。

单击“启动 CloudFormation 堆栈”按钮。

![](https://i.imgur.com/O4E0b4I.png)

在下一页上，选中“我承认 AWS CloudFormation 可能会创建 IAM 资源”复选框并单击“创建堆栈”按钮。

![](https://i.imgur.com/VkzM0Ss.png)

在下一页上，您将看到在 CloudFormation 中创建的堆栈。这将需要几分钟时间。

![](https://i.imgur.com/W0Qiu8D.png)

创建堆栈后，您可以单击“输出”选项卡查看我们的工作节点配置的详细信息。

![](https://i.imgur.com/tY0NVT3.png)

记下“NodeInstanceRole”和“WorkerNodeSecurityGroup”值，因为我们稍后需要它们。

现在我们的工作线程节点已经设置好了，我们可以返回到 Amazon EKS 控制台并创建我们的集群。

单击“下一步”按钮。

![](https://i.imgur.com/Ft7YIxu.png)

在下一页，我们需要配置我们的工作节点。选择您想要拥有的工作节点数，然后输入我们之前记下的“NodeInstanceRole”和“WorkerNodeSecurityGroup”值。

![](https://i.imgur.com/vALDKQi.png)

接下来，我们需要配置我们的网络。选择“VPC”选项并选择由我们的 CloudFormation 堆栈创建的 VPC。然后，选择“子网”选项并选择由我们的 CloudFormation 堆栈创建的两个子网。

![](https://i.imgur.com/7DpjTGi.png)

现在，我们需要选择 Kubernetes 集群端点访问类型。选择“公开”选项。

![](https://i.imgur.com/DY0b4oI.png)

接下来，我们需要配置我们的安全组。选择“安全组”选项并选择由我们的 CloudFormation 堆栈创建的安全组。

![](https://i.imgur.com/4JcM0Ss.png)

现在，我们需要选择 Kubernetes 集群日志记录类型。选择“Amazon CloudWatch”选项。

![](https://i.imgur.com/BkzM0Ss.png)

接下来，我们需要选择 Kubernetes 集群监控类型。选择“Amazon CloudWatch”选项。

![](https://i.imgur.com/nALDKQi.png)

现在，我们需要选择 Kubernetes 集群加密类型。选择“AES-256”选项。

![](https://i.imgur.com/p0bJUO4.png)

现在，我们需要选择一个 Kubernetes 集群自动伸缩组类型。选择“AsgBasedAutoScaling”选项。

![](https://i.imgur.com/FkzM0Ss.png)

现在，我们需要配置我们的工作节点自动缩放组。选择“WorkerNodesAsg”选项并选择由我们的 CloudFormation 堆栈创建的自动缩放组。

![](https://i.imgur.com/VkzM0Ss.png)

现在，我们需要选择 Kubernetes 集群扩展配置类型。选择“默认”选项。

![](https://i.imgur.com/p0bJUO4.png)

在下一页上，检查您的集群配置并单击“创建集群”按钮。

![](https://i.imgur.com/LDAd5u8.png)

在下一页上，您将看到正在创建的集群。这将需要几分钟时间。

![](https://i.imgur.com/W0Qiu8D.png)

创建集群后，您可以单击“配置 kubectl”按钮来配置 kubectl 命令行工具以与我们的集群进行通信。

![](https://i.imgur.com/nALDKQi.png)

在下一页上，单击“下载配置”按钮。

![](https://i.imgur.com/7DpjTGi.png)

这会将 kubeconfig 文件下载到您的机器上。将此文件移动到 ~/.kube 目录并将其重命名为 config。

现在，我们可以通过运行以下命令来测试我们的集群是否正常工作：

```
kubectl get svc
```

如果一切正常，您应该会在集群中看到一个服务列表。

## 在我们的 Kubernetes 集群上部署应用程序

现在我们的 Kubernetes 集群已启动并运行，我们可以在其上部署应用程序。对于此示例，我们将部署一个用 Go 编写的简单“Hello World”应用程序。

首先，我们需要为我们的应用程序创建一个 Dockerfile。在我们项目的根目录中创建一个名为“Dockerfile”的文件，内容如下：

```
FROM golang:1.13-alpine

RUN mkdir /app

ADD . /app/

WORKDIR /app

RUN go build -o main .

CMD ["/app/main"]
```

接下来，我们需要编写我们的应用程序代码。在我们项目的根目录中创建一个名为“main.go”的文件，内容如下：

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello World!")
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}
```

现在，我们可以构建我们的 Docker 镜像并将其推送到 Docker 注册表。我们将使用 Amazon ECR 作为我们的 Docker 注册表。

首先，我们需要在 Amazon ECR 中创建一个新的存储库。登录到 Amazon ECR 控制台并单击“创建存储库”按钮。

![](https://i.imgur.com/tY0NVT3.png)

在下一页上，为您的存储库输入一个名称，然后单击“创建存储库”按钮。

![](https://i.imgur.com/nALDKQi.png)

现在，我们可以构建我们的 Docker 镜像并将其推送到我们的新存储库。

运行以下命令来构建和推送我们的 Docker 镜像：

```
$ docker build -t {your_aws_account_id}.dkr.ecr.{your_region}.amazonaws.com/{your_repository_name} .

$ docker push {your_aws_account_id}.dkr.ecr.{your_region}.amazonaws.com/{your_repository_name}
```

将 {your_aws_account_id}、{your_region} 和 {your_repository_name} 替换为您的账户和存储库的适当值。

现在我们的 Docker 镜像被推送到我们的存储库，我们可以将它部署到我们的 Kubernetes 集群上。

首先，我们需要创建一个部署文件。在我们项目的根目录中创建一个名为“deployment.yaml”的文件，内容如下：

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
spec:
  replicas: 3
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: {your_aws_account_id}.dkr.ecr.{your_region}.amazonaws.com/{your_repository_name}
        ports:
        - containerPort: 8080
```

将 {your_aws_account_id}、{your_region} 和 {your_repository_name} 替换为您的账户和存储库的适当值。

现在，我们可以通过运行以下命令在我们的 Kubernetes 集群上部署我们的应用程序：

```
kubectl apply -f deployment.yaml
```

这将创建一个名为“hello-world”的部署，其中包含三个副本。

要查看我们的部署，我们需要将其公开给外界。我们可以通过创建服务来做到这一点。

首先，我们需要创建一个服务文件。在我们项目的根目录中创建一个名为“service.yaml”的文件，内容如下：

```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-world
spec:
  type: LoadBalancer
  ports:
  - port: 80
    protocol: TCP
    targetPort: 8080
  selector:
    app: hello-world
```

现在，我们可以通过运行以下命令来部署我们的服务：

```
kubectl apply -f service.yaml
```

这将创建一个类型为“LoadBalancer”的名为“hello-world”的服务。这种类型的服务将在 AWS 中创建一个负载均衡器，并将我们的部署暴露给外界。

要找出我们的负载均衡器的 URL，请运行以下命令：

```
kubectl get svc hello-world
```

您应该会看到类似于以下内容的输出：

```
NAME           TYPE           CLUSTER-IP      EXTERNAL-IP                                                              PORT(S)        AGE
hello-world    LoadBalancer   10.100.200.16   aaa.bbb.ccc.ddd   80:32000/TCP,443:31943/TCP   5m29s
```

“EXTERNAL-IP”值是我们的负载均衡器的 URL。

## 删除我们的 Kubernetes 集群

如果您想删除 Kubernetes 集群，您可以从 Amazon EKS 控制台执行此操作。

首先，登录 Amazon EKS 控制台并导航至“集群”页面。

![](https://i.imgur.com/LDAd5u8.png)

在下一页上，选中要删除的集群旁边的复选框，然后单击“删除”按钮。

![](https://i.imgur.com/7DpjTGi.png)

在下一页上，在“集群名称”字段中输入集群的名称，然后单击“删除集群”按钮。

![](https://i.imgur.com/p0bJUO4.png)

## 结论

在本文中，我们向您展示了如何在 AWS 上部署 Kubernetes 集群。我们还向您展示了如何在集群上部署应用程序。

如果您想了解更多关于 Kubernetes 的信息，我们推荐以下资源：

- Kubernetes 官方文档：https://kubernetes.io/docs/

- 官方 Amazon EKS 文档：https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html

- 官方 Amazon ECR 文档：https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html