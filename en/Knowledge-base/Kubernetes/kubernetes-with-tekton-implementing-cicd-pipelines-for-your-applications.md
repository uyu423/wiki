---
title: Kubernetes with Tekton: Implementing CI/CD Pipelines for Your Applications
description: 
published: true
date: 2023-02-14T13:33:41.904Z
tags: 
editor: markdown
dateCreated: 2023-02-14T13:33:34.607Z
---

- [Kubernetes con Tekton: Implementación de canalizaciones de CI/CD para sus aplicaciones***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-with-tekton-implementing-cicd-pipelines-for-your-applications)
{.links-list}
- [Kubernetes 与 Tekton：为您的应用程序实施 CI/CD 管道***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-with-tekton-implementing-cicd-pipelines-for-your-applications)
{.links-list}
- [Kubernetes와 Tekton: 애플리케이션을 위한 CI/CD 파이프라인 구현***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-with-tekton-implementing-cicd-pipelines-for-your-applications)
{.links-list}


Kubernetes is an open-source container orchestration system for automating application deployment, scaling, and management. Tekton is an open-source toolkit for building, testing, and deploying cloud-native applications on Kubernetes.

In this article, we will show you how to use Tekton to set up a continuous integration/continuous deployment (CI/CD) pipeline for your Kubernetes applications.

We will cover the following topics:

* Setting up a Tekton pipeline
* Configuring Tekton tasks
* Creating a Tekton pipeline run

## Setting up a Tekton pipeline

The first thing we need to do is set up a Tekton pipeline. A Tekton pipeline is a collection of tasks that can be executed in order. Each task in a Tekton pipeline can be executed in parallel or sequentially.

In this example, we will create a Tekton pipeline with two tasks:

* A build task that builds our application code
* A deploy task that deploys our application to a Kubernetes cluster

To set up our Tekton pipeline, we will use the `tkn` command-line tool.

First, we need to create a file called `build-deploy-pipeline.yaml` with the following contents:

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

In this file, we have defined a Tekton pipeline with two tasks: `build-task` and `deploy-task`. The `taskRef` field specifies the name of the Tekton task template that should be used for each task.

Next, we need to create a file called `build-task-template.yaml` with the following contents:

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

This file defines a Tekton task template for the `build-task` in our pipeline. The `inputs` section defines the input resources for the task, which in this case is a Git repository containing our application source code. The `outputs` section defines the output resources for the task, which in this case is a Docker image containing our application code.

The `steps` section defines the steps that should be executed for the task. In this case, we have a single step that runs the `go build` command to build our application code.

Next, we need to create a file called `deploy-task-template.yaml` with the following contents:

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

This file defines a Tekton task template for the `deploy-task` in our pipeline. The `inputs` section defines the input resources for the task, which in this case is a Docker image containing our application code. The `parameters` section defines the parameters for the task, which in this case is the namespace in which our application should be deployed.

The `steps` section defines the steps that should be executed for the task. In this case, we have a single step that runs the `k8s-deploy` command to deploy our application to a Kubernetes cluster.

## Configuring Tekton tasks

Now that we have created our Tekton pipeline, we need to configure our Tekton tasks.

First, we need to create a file called `build-task-parameters.yaml` with the following contents:

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

In this file, we have defined a Tekton task run for the `build-task` in our pipeline. The `taskRef` field specifies the name of the Tekton task template that should be used for the task.

The `inputs` section defines the input resources for the task. In this case, we are using a Git repository containing our application source code. The `url` and `revision` parameters specify the URL and revision of the Git repository.

The `outputs` section defines the output resources for the task. In this case, we are using a Docker image to store our built application code. The `url` parameter specifies the URL of the Docker image.

Next, we need to create a file called `deploy-task-parameters.yaml` with the following contents:

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

In this file, we have defined a Tekton task run for the `deploy-task` in our pipeline. The `taskRef` field specifies the name of the Tekton task template that should be used for the task.

The `inputs` section defines the input resources for the task. In this case, we are using a Docker image containing our application code. The `url` parameter specifies the URL of the Docker image.

The `outputs` section defines the output parameters for the task. In this case, we are using the `namespace` parameter to specify the namespace in which our application should be deployed.

## Creating a Tekton pipeline run

Now that we have configured our Tekton tasks, we can create a Tekton pipeline run to execute our pipeline.

First, we need to create a file called `pipeline-run.yaml` with the following contents:

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

In this file, we have defined a Tekton pipeline run for our `build-deploy-pipeline`. The `pipelineRef` field specifies the name of the Tekton pipeline that should be used for the pipeline run.

The `serviceAccountName` field specifies the name of the Kubernetes service account that should be used for the pipeline run.

The `timeout` field specifies the maximum duration of the pipeline run.

The `workspaces` section defines the workspaces that should be used for the pipeline run. In this case, we are using two workspaces: `source-repo` and `application-image-repo`. These workspaces will be used to store the input and output resources for our tasks.

To create the pipeline run, we can use the `tkn` command-line tool:

```
tkn pipeline start build-deploy-pipeline-run --workspaces=source-repo=source-repo-ws,application-image-repo=application-image-repo-ws
```

This command will create a pipeline run with the name `build-deploy-pipeline-run`. The `--workspaces` flag specifies the workspaces that should be used for the pipeline run.

Once the pipeline run has been created, we can use the `tkn` command-line tool to get the status of the pipeline run:

```
tkn pipeline status build-deploy-pipeline-run
```

This command will output the status of the `build-deploy-pipeline-run` pipeline run.

## Conclusion

In this article, we have shown you how to use Tekton to set up a continuous integration/continuous deployment (CI/CD) pipeline for your Kubernetes applications.