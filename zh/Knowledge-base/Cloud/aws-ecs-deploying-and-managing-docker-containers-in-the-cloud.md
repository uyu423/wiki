---
title: AWS ECS：在云中部署和管理 Docker 容器
description: 
published: true
date: 2023-02-16T00:17:54.261Z
tags: 
editor: markdown
dateCreated: 2023-02-16T00:17:51.794Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [AWS ECS: Deploying and Managing Docker Containers in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-ecs-deploying-and-managing-docker-containers-in-the-cloud)
{.links-list}


# AWS ECS：在云中部署和管理 Docker 容器

近年来，Docker 容器已成为打包和部署应用程序的标准。与传统虚拟机相比，它们具有许多优势，包括可移植性、减少资源开销以及与持续集成/持续交付 (CI/CD) 管道的轻松集成。

AWS Elastic Container Service (ECS) 是一种托管容器编排服务，可让您轻松地在云中运行和管理 Docker 容器。在本文中，我们将了解如何在 AWS ECS 上部署和管理 Docker 容器。

## 创建 ECS 集群

使用 AWS ECS 的第一步是创建 ECS 集群。 ECS 集群是用于托管 Docker 容器的 EC2 实例的逻辑分组。您可以使用 AWS 管理控制台、AWS 命令行界面 (CLI) 或 AWS SDK 创建 ECS 集群。

### 使用 AWS 管理控制台创建 ECS 集群

要使用 AWS 管理控制台创建 ECS 集群，首先打开 Amazon ECS 控制台并选择左侧导航中的“集群”链接。然后，单击“创建集群”按钮。

在“Create Cluster”页面上，选择“Networking only”模板并为您的集群命名。然后，单击“创建”按钮。

现在将创建您的集群，您可以在“集群”列表中查看它。

### 使用 AWS CLI 创建 ECS 集群

要使用 AWS CLI 创建 ECS 集群，首先创建一个名为“ecs-cli-cluster.json”的文件，其中包含以下内容：

```json
{
    "clusterName": "my-ecs-cluster",
    "networkConfiguration": {
        "awsvpcConfiguration": {
            "subnets": [
                "subnet-12345678",
                "subnet-87654321"
            ],
            "securityGroups": [
                "sg-12345678"
            ],
            "associatePublicIpAddress": true
        }
    }
}
```

将“clusterName”、“subnets”和“securityGroups”字段中的值替换为适合您环境的值。然后，运行以下命令创建集群：

```
aws ecs create-cluster --cli-input-json file://ecs-cli-cluster.json
```

## 创建 ECS 任务定义

现在您已经有了一个 ECS 集群，您可以将应用程序部署到它上面。 ECS 中的应用程序由任务定义定义，任务定义指定运行应用程序所需的 Docker 镜像和其他资源。

您可以使用 AWS 管理控制台、AWS CLI 或 AWS SDK 创建任务定义。

### 使用 AWS 管理控制台创建任务定义

要使用 AWS 管理控制台创建任务定义，首先打开 Amazon ECS 控制台并选择左侧导航中的“任务定义”链接。然后，单击“创建新任务定义”按钮。

在“选择启动类型”页面上，选择“EC2”启动类型并单击“下一步”按钮。

在“配置任务和容器定义”页面上，为您的任务命名和描述。然后，向下滚动到“容器定义”部分并单击“添加容器”按钮。

在“添加容器”模式中，输入以下值：

- **容器名称：**我的容器
- **图片：** nginx：最新
- **内存限制（MiB）：** 512
- **端口映射：** 80:80

然后，单击“添加”按钮。

您的容器现在将添加到任务定义中。向下滚动到“任务角色”部分，然后选择“无”选项。然后，向下滚动到“网络模式”部分并选择“网桥”选项。最后，单击“下一步”按钮。

在“审查”页面上，审查您的任务定义并单击“创建”按钮。

现在将创建您的任务定义，您可以在“任务定义”列表中查看它。

### 使用 AWS CLI 创建任务定义

要使用 AWS CLI 创建任务定义，首先创建一个名为“ecs-cli-task-definition.json”的文件，其中包含以下内容：

```json
{
    "family": "my-task-definition",
    "networkMode": "bridge",
    "containerDefinitions": [
        {
            "name": "my-container",
            "image": "nginx:latest",
            "memory": 512,
            "portMappings": [
                {
                    "containerPort": 80,
                    "hostPort": 80
                }
            ]
        }
    ]
}
```

将“family”和“containerDefinitions”字段中的值替换为适合您环境的值。然后，运行以下命令来创建任务定义：

```
aws ecs register-task-definition --cli-input-json file://ecs-cli-task-definition.json
```

## 将应用程序部署到 ECS 集群

现在您已拥有 ECS 集群和任务定义，您可以将应用程序部署到集群。您可以使用 AWS 管理控制台、AWS CLI 或 AWS 开发工具包将应用程序部署到 ECS 集群。

### 使用 AWS 管理控制台部署应用程序

要使用 AWS 管理控制台部署应用程序，首先打开 Amazon ECS 控制台并选择左侧导航中的“集群”链接。然后，选择要部署到的集群并单击“任务”选项卡。

在“任务”选项卡上，单击“运行新任务”按钮。

在“配置任务和容器设置”页面上，选择“my-task-definition”任务定义并单击“下一步”按钮。

在“配置网络”页面，选择“桥接”网络模式，点击“下一步”按钮。

在“审查”页面上，审查您的任务设置并单击“运行任务”按钮。

您的任务现在将部署到集群，您可以在“任务”选项卡中查看其状态。

### 使用 AWS CLI 部署应用程序

要使用 AWS CLI 部署应用程序，首先创建一个名为“ecs-cli-run-task.json”的文件，其中包含以下内容：

```json
{
    "taskDefinition": "my-task-definition",
    "networkConfiguration": {
        "awsvpcConfiguration": {
            "subnets": [
                "subnet-12345678",
                "subnet-87654321"
            ],
            "securityGroups": [
                "sg-12345678"
            ],
            "associatePublicIpAddress": true
        }
    }
}
```

将“taskDefinition”、“subnets”和“securityGroups”字段中的值替换为适合您环境的值。然后，运行以下命令部署任务：

```
aws ecs run-task --cli-input-json file://ecs-cli-run-task.json
```

## 监控 ECS 集群

AWS ECS 提供了许多工具来监控您的集群和集群上运行的任务。

第一个工具是 CloudWatch。 CloudWatch 是一项 AWS 服务，用于收集和处理 AWS 资源（包括 ECS 集群）的监控数据。您可以使用 CloudWatch 查看 ECS 集群的指标、设置警报和查看日志。

第二个工具是 Amazon CloudWatch Logs。 CloudWatch Logs 是一项服务，可用于监控、存储和访问来自 AWS 资源（包括 ECS 集群）的日志文件。您可以使用 CloudWatch Logs 查看 ECS 集群的日志以及集群上运行的任务。

第三个工具是 Amazon CloudWatch Events。 CloudWatch Events 是一项服务，可用于监控来自 AWS 资源（包括 ECS 集群）的事件。您可以使用 CloudWatch Events 查看 ECS 集群的事件以及集群上运行的任务。

## 删除 ECS 集群

如果您不再需要 ECS 集群，可以使用 AWS 管理控制台、AWS CLI 或 AWS 开发工具包将其删除。

### 使用 AWS 管理控制台删除 ECS 集群

要使用 AWS 管理控制台删除 ECS 集群，首先打开 Amazon ECS 控制台并选择左侧导航中的“集群”链接。然后，选择要删除的集群并单击“删除”按钮。

在“删除集群”页面，查看集群信息，点击“删除”按钮。

您的集群现在将被删除。

### 使用 AWS CLI 删除 ECS 集群

要使用 AWS CLI 删除 ECS 集群，请运行以下命令：

```
aws ecs delete-cluster --cluster my-ecs-cluster
```

## 结论

在本文中，我们了解了如何在 AWS ECS 上部署和管理 Docker 容器。我们已经了解了如何创建 ECS 集群、创建任务定义以及将应用程序部署到集群。我们还了解了如何使用 CloudWatch 监控 ECS 集群。最后，我们了解了如何删除 ECS 集群。