---
title: Kubernetes 与 Tekton：为您的应用程序实施 CI/CD 管道
description: 
published: true
date: 2023-02-14T13:33:36.250Z
tags: 
editor: markdown
dateCreated: 2023-02-14T13:33:34.603Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes with Tekton: Implementing CI/CD Pipelines for Your Applications***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-tekton-implementing-cicd-pipelines-for-your-applications)
{.links-list}


Kubernetes 是一个开源容器编排系统，用于自动化应用程序部署、扩展和管理。 Tekton 是一个开源工具包，用于在 Kubernetes 上构建、测试和部署云原生应用程序。

在本文中，我们将向您展示如何使用 Tekton 为您的 Kubernetes 应用程序设置持续集成/持续部署 (CI/CD) 管道。

我们将涵盖以下主题：

* 设置 Tekton 管道
* 配置 Tekton 任务
* 创建 Tekton 管道运行

## 设置 Tekton 管道

我们需要做的第一件事是设置 Tekton 管道。 Tekton 管道是可以按顺序执行的任务的集合。 Tekton 管道中的每个任务都可以并行或顺序执行。

在此示例中，我们将创建一个包含两个任务的 Tekton 管道：

* 构建应用程序代码的构建任务
* 将我们的应用程序部署到 Kubernetes 集群的部署任务

要设置我们的 Tekton 管道，我们将使用“tkn”命令行工具。

首先，我们需要创建一个名为“build-deploy-pipeline.yaml”的文件，其中包含以下内容：

```yaml
apiVersion: tekton.dev/v1alpha1
kind: Pipeline
metadata:
  name: build-deploy-pipeline
spec:
  tasks:
  - name: build-task
    taskRef:
      name: build-task-template
  - name: deploy-task
    taskRef:
      name: deploy-task-template
```

在此文件中，我们定义了一个包含两个任务的 Tekton 管道：`build-task` 和 `deploy-task`。 `taskRef` 字段指定应用于每个任务的 Tekton 任务模板的名称。

接下来，我们需要创建一个名为“build-task-template.yaml”的文件，其中包含以下内容：

```yaml
apiVersion: tekton.dev/v1alpha1
kind: TaskTemplate
metadata:
  name: build-task-template
spec:
  inputs:
  - name: source
    resourceRef:
      name: source-repo
  outputs:
  - name: application-image
    resourceRef:
      name: application-image-repo
  steps:
  - name: build-step
    image: golang:1.14
    command: ['go', 'build', '-o', '/workspace/application-image']
```

该文件为管道中的“build-task”定义了一个 Tekton 任务模板。 `inputs` 部分定义任务的输入资源，在本例中是包含我们的应用程序源代码的 Git 存储库。 `outputs` 部分定义任务的输出资源，在本例中是包含我们的应用程序代码的 Docker 映像。

`steps` 部分定义了应该为任务执行的步骤。在这种情况下，我们只有一步运行 `go build` 命令来构建我们的应用程序代码。

接下来，我们需要创建一个名为“deploy-task-template.yaml”的文件，其中包含以下内容：

```yaml
apiVersion: tekton.dev/v1alpha1
kind: TaskTemplate
metadata:
  name: deploy-task-template
spec:
  inputs:
  - name: application-image
    resourceRef:
      name: application-image-repo
  parameters:
  - name: namespace
    type: string
  steps:
  - name: deploy-step
    image: quay.io/openshift-evangelists/k8s-deploy:latest
    command:
    - k8s-deploy
    - -n
    - '$(params.namespace)'
    - -i
    - '$(inputs.application-image.path)/application-image'
```

该文件为我们管道中的“部署任务”定义了一个 Tekton 任务模板。 `inputs` 部分定义任务的输入资源，在本例中是包含我们的应用程序代码的 Docker 映像。 `parameters` 部分定义了任务的参数，在本例中是我们的应用程序应部署到的命名空间。

`steps` 部分定义了应该为任务执行的步骤。在这种情况下，我们只需一步即可运行“k8s-deploy”命令，将我们的应用程序部署到 Kubernetes 集群。

## 配置 Tekton 任务

现在我们已经创建了 Tekton 管道，我们需要配置 Tekton 任务。

首先，我们需要创建一个名为“build-task-parameters.yaml”的文件，其中包含以下内容：

```yaml
apiVersion: tekton.dev/v1alpha1
kind: TaskRun
metadata:
  name: build-task-run
spec:
  taskRef:
    name: build-task-template
  inputs:
    resources:
    - name: source-repo
      resourceSpec:
        type: git
        params:
        - name: url
          value: 'https://github.com/openshift-evangelists/k8s-cd-demo.git'
        - name: revision
          value: master
    outputs:
    - name: application-image
      resourceSpec:
        type: image
        params:
        - name: url
          value: 'docker.io/library/busybox:1.31'
```

在此文件中，我们为管道中的“build-task”定义了一个 Tekton 任务运行。 `taskRef` 字段指定应用于任务的 Tekton 任务模板的名称。

`inputs` 部分定义任务的输入资源。在本例中，我们使用包含应用程序源代码的 Git 存储库。 `url` 和 `revision` 参数指定 Git 存储库的 URL 和修订版本。

`outputs` 部分定义任务的输出资源。在这种情况下，我们使用 Docker 镜像来存储我们构建的应用程序代码。 `url` 参数指定 Docker 镜像的 URL。

接下来，我们需要创建一个名为“deploy-task-parameters.yaml”的文件，其中包含以下内容：

```yaml
apiVersion: tekton.dev/v1alpha1
kind: TaskRun
metadata:
  name: deploy-task-run
spec:
  taskRef:
    name: deploy-task-template
  inputs:
    resources:
    - name: application-image
      resourceSpec:
        type: image
        params:
        - name: url
          value: 'docker.io/library/busybox:1.31'
  outputs:
    params:
    - name: namespace
      value: 'default'
```

在此文件中，我们为管道中的“deploy-task”定义了一个 Tekton 任务运行。 `taskRef` 字段指定应用于任务的 Tekton 任务模板的名称。

`inputs` 部分定义任务的输入资源。在这种情况下，我们使用包含我们的应用程序代码的 Docker 映像。 `url` 参数指定 Docker 镜像的 URL。

`outputs` 部分定义任务的输出参数。在这种情况下，我们使用 `namespace` 参数来指定我们的应用程序应该部署到的命名空间。

## 创建 Tekton 管道运行

现在我们已经配置了 Tekton 任务，我们可以创建 Tekton 管道运行来执行我们的管道。

首先，我们需要创建一个名为 pipeline-run.yaml 的文件，其中包含以下内容：

```yaml
apiVersion: tekton.dev/v1alpha1
kind: PipelineRun
metadata:
  name: build-deploy-pipeline-run
spec:
  pipelineRef:
    name: build-deploy-pipeline
  serviceAccountName: tekton-service-account
  timeout: 10m
  workspaces:
  - name: source-repo
    workspace:
      volumeClaimTemplate:
        metadata:
          name: source-repo
        spec:
          accessModes:
          - ReadWriteOnce
          resources:
            requests:
              storage: 2Gi
  - name: application-image-repo
    workspace:
      volumeClaimTemplate:
        metadata:
          name: application-image-repo
        spec:
          accessModes:
          - ReadWriteOnce
          resources:
            requests:
              storage: 2Gi
```

在此文件中，我们为我们的“build-deploy-pipeline”定义了一个 Tekton 管道运行。 `pipelineRef` 字段指定应用于管道运行的 Tekton 管道的名称。

`serviceAccountName` 字段指定应用于管道运行的 Kubernetes 服务帐户的名称。

`timeout` 字段指定流水线运行的最长持续时间。

`workspaces` 部分定义应该用于管道运行的工作区。在这种情况下，我们使用两个工作区：`source-repo` 和 `application-image-repo`。这些工作区将用于存储我们任务的输入和输出资源。

要创建流水线运行，我们可以使用 `tkn` 命令行工具：

```
tkn pipeline start build-deploy-pipeline-run --workspaces=source-repo=source-repo-ws,application-image-repo=application-image-repo-ws
```

此命令将创建一个名为“build-deploy-pipeline-run”的管道运行。 `--workspaces` 标志指定应用于管道运行的工作区。

创建管道运行后，我们可以使用 `tkn` 命令行工具来获取管道运行的状态：

```
tkn pipeline status build-deploy-pipeline-run
```

此命令将输出“build-deploy-pipeline-run”管道运行的状态。

## 结论

在本文中，我们向您展示了如何使用 Tekton 为您的 Kubernetes 应用程序设置持续集成/持续部署 (CI/CD) 管道。