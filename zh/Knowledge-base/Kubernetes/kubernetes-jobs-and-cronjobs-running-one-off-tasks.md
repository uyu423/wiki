---
title: Kubernetes 作业和 CronJobs：运行一次性任务
description: 
published: true
date: 2023-02-08T22:32:42.057Z
tags: 
editor: markdown
dateCreated: 2023-02-08T22:32:40.445Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes Jobs and CronJobs: Running One-Off Tasks***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-jobs-and-cronjobs-running-one-off-tasks)
{.links-list}


# Kubernetes 作业和 CronJobs：运行一次性任务

在本文中，我们将讨论 Kubernetes 中的 Jobs 和 CronJobs 以及如何使用它们来运行一次性任务。我们将详细介绍每种资源类型是什么以及它们的用途，我们还将提供一些示例来说明如何创建和管理 Jobs 和 CronJobs。

## 工作

作业是一种 Kubernetes 资源，可用于运行一次性任务。一个 Job 会创建一个或多个 Pod，并确保 Pod 成功完成才被认为是成功的。如果 pod 发生故障，Job 将自动重启它。

作业可用于多种任务，例如批处理作业、数据导入、数据库备份等。

要创建作业，您需要创建作业清单。 Job 清单定义了 Job 的规格，例如副本数、pod 模板和重启策略。

这是一个示例作业清单：

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: my-job
spec:
  template:
    spec:
      containers:
      - name: my-job
        image: busybox
        command: ["echo", "Hello World!"]
      restartPolicy: Never
  backoffLimit: 4
```

在上面的示例中，我们定义了一个具有单个副本的作业。作业将使用 busybox 图像创建一个 pod 并运行命令“echo Hello World!”。 Job 也会有一个 Never 的 restartPolicy，这意味着如果 pod 失败它不会自动重启。

要创建作业，您可以使用 kubectl apply 命令：

```
kubectl apply -f my-job.yaml
```

您还可以使用 kubectl create 命令：

```
kubectl create job my-job --image=busybox -- echo "Hello World!"
```

创建作业后，您可以使用 kubectl get jobs 命令检查其状态：

```
kubectl get jobs
NAME      DESIRED   SUCCESSFUL   AGE
my-job    1         1            5s
```

您还可以检查 Job 创建的 pod 的状态：

```
kubectl get pods
NAME                    READY   STATUS      RESTARTS   AGE
my-job-9f6b8b4b4-6x8nw   0/1     Completed   0          6s
```

作业完成后，您可以使用 kubectl delete job 命令将其删除：

```
kubectl delete job my-job
```

## 定时任务

CronJobs 是一种 Kubernetes 资源，可用于运行重复性任务。 CronJob 将在指定的时间或间隔创建一个 Job。

CronJobs 可用于多种任务，例如数据库备份、系统维护等。

要创建 CronJob，您需要创建 CronJob 清单。 CronJob 清单定义了 CronJob 的规范，例如计划、作业模板和并发策略。

这是一个示例 CronJob 清单：

```yaml
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: my-cronjob
spec:
  schedule: "0 */4 * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: my-cronjob
            image: busybox
            command: ["echo", "Hello World!"]
          restartPolicy: OnFailure
  concurrencyPolicy: Forbid
```

在上面的示例中，我们定义了一个每 4 小时运行一次的 CronJob。 CronJob 将使用 busybox 图像创建一个作业并运行命令“echo Hello World!”。 Job 也会有一个 OnFailure 的 restartPolicy，这意味着如果 pod 失败，它会自动重启。 CronJob 的 concurrencyPolicy 为 Forbid，这意味着一次只能运行一个 Job。

要创建 CronJob，您可以使用 kubectl apply 命令：

```
kubectl apply -f my-cronjob.yaml
```

您还可以使用 kubectl create 命令：

```
kubectl create cronjob my-cronjob --image=busybox -- echo "Hello World!"
```

创建 CronJob 后，您可以使用 kubectl get cronjobs 命令检查其状态：

```
kubectl get cronjobs
NAME       SCHEDULE      SUSPEND   ACTIVE   LAST SCHEDULE   AGE
my-cronjob   0 */4 * * *   False     0        <none>          5s
```

您还可以检查 CronJob 创建的作业的状态：

```
kubectl get jobs
NAME                          DESIRED   SUCCESSFUL   AGE
my-cronjob-1586409600          1         1            5s
```

作业完成后，您可以使用 kubectl delete job 命令将其删除：

```
kubectl delete job my-cronjob-1586409600
```

您还可以使用 kubectl delete cronjob 命令删除 CronJob：

```
kubectl delete cronjob my-cronjob
```

## 结论

在本文中，我们讨论了 Kubernetes 中的 Jobs 和 CronJobs 以及如何使用它们来运行一次性任务。我们了解了每种资源类型的含义以及它们的用途，我们还提供了一些示例来说明如何创建和管理 Jobs 和 CronJobs。