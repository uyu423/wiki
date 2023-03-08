---
title: Kubernetes 작업 및 CronJob: 일회성 작업 실행
description: 
published: true
date: 2023-02-08T22:32:42.098Z
tags: 
editor: markdown
dateCreated: 2023-02-08T22:32:40.444Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes Jobs and CronJobs: Running One-Off Tasks***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-jobs-and-cronjobs-running-one-off-tasks)
{.links-list}


# Kubernetes 작업 및 CronJobs: 일회성 작업 실행

이 기사에서는 Kubernetes의 작업 및 CronJob과 일회성 작업을 실행하는 데 사용하는 방법에 대해 설명합니다. 이러한 각 리소스 유형이 무엇이고 무엇을 사용할 수 있는지 살펴보고 작업 및 CronJob을 만들고 관리하는 방법에 대한 몇 가지 예도 제공합니다.

## 직업

작업은 일회성 작업을 실행하는 데 사용할 수 있는 Kubernetes 리소스 유형입니다. 작업은 하나 이상의 포드를 만들고 성공적인 것으로 간주되기 전에 포드가 성공적으로 완료되었는지 확인합니다. Pod가 실패하면 작업이 자동으로 Pod를 다시 시작합니다.

작업은 배치 작업, 데이터 가져오기, 데이터베이스 백업 등과 같은 다양한 작업에 사용할 수 있습니다.

작업을 만들려면 작업 매니페스트를 만들어야 합니다. 작업 매니페스트는 복제본 수, 포드 템플릿 및 다시 시작 정책과 같은 작업 사양을 정의합니다.

다음은 작업 매니페스트의 예입니다.

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

위의 예에서는 단일 복제본으로 작업을 정의했습니다. 작업은 busybox 이미지를 사용하여 포드를 생성하고 "echo Hello World!" 명령을 실행합니다. Job은 또한 Never의 restartPolicy를 갖게 됩니다. 즉, Pod가 실패해도 자동으로 다시 시작되지 않습니다.

작업을 생성하려면 kubectl apply 명령을 사용할 수 있습니다.

```
kubectl apply -f my-job.yaml
```

kubectl create 명령을 사용할 수도 있습니다.

```
kubectl create job my-job --image=busybox -- echo "Hello World!"
```

작업이 생성되면 kubectl get jobs 명령을 사용하여 상태를 확인할 수 있습니다.

```
kubectl get jobs
NAME      DESIRED   SUCCESSFUL   AGE
my-job    1         1            5s
```

작업이 생성하는 팟(Pod)의 상태를 확인할 수도 있습니다.

```
kubectl get pods
NAME                    READY   STATUS      RESTARTS   AGE
my-job-9f6b8b4b4-6x8nw   0/1     Completed   0          6s
```

작업이 완료되면 kubectl delete job 명령을 사용하여 삭제할 수 있습니다.

```
kubectl delete job my-job
```

## CronJobs

CronJob은 반복 작업을 실행하는 데 사용할 수 있는 Kubernetes 리소스 유형입니다. CronJob은 지정된 시간 또는 간격으로 작업을 생성합니다.

CronJob은 데이터베이스 백업, 시스템 유지 관리 등과 같은 다양한 작업에 사용할 수 있습니다.

CronJob을 만들려면 CronJob 매니페스트를 만들어야 합니다. CronJob 매니페스트는 일정, 작업 템플릿 및 동시성 정책과 같은 CronJob의 사양을 정의합니다.

다음은 CronJob 매니페스트의 예입니다.

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

위의 예에서는 4시간마다 실행되는 CronJob을 정의했습니다. CronJob은 busybox 이미지를 사용하여 작업을 생성하고 "echo Hello World!" 명령을 실행합니다. 작업에는 OnFailure의 restartPolicy도 포함됩니다. 즉, 포드가 실패하면 자동으로 다시 시작됩니다. CronJob은 Forbid의 concurrencyPolicy를 가지며, 이는 한 번에 하나의 작업만 실행할 수 있음을 의미합니다.

CronJob을 생성하려면 kubectl apply 명령을 사용할 수 있습니다.

```
kubectl apply -f my-cronjob.yaml
```

kubectl create 명령을 사용할 수도 있습니다.

```
kubectl create cronjob my-cronjob --image=busybox -- echo "Hello World!"
```

CronJob이 생성되면 kubectl get cronjobs 명령을 사용하여 상태를 확인할 수 있습니다.

```
kubectl get cronjobs
NAME       SCHEDULE      SUSPEND   ACTIVE   LAST SCHEDULE   AGE
my-cronjob   0 */4 * * *   False     0        <none>          5s
```

CronJob이 생성하는 작업의 상태를 확인할 수도 있습니다.

```
kubectl get jobs
NAME                          DESIRED   SUCCESSFUL   AGE
my-cronjob-1586409600          1         1            5s
```

작업이 완료되면 kubectl delete job 명령을 사용하여 삭제할 수 있습니다.

```
kubectl delete job my-cronjob-1586409600
```

kubectl delete cronjob 명령을 사용하여 CronJob을 삭제할 수도 있습니다.

```
kubectl delete cronjob my-cronjob
```

## 결론

이 기사에서는 Kubernetes의 작업 및 CronJob과 이를 사용하여 일회성 작업을 실행하는 방법에 대해 설명했습니다. 이러한 각 리소스 유형이 무엇이고 무엇을 사용할 수 있는지 살펴보고 작업 및 CronJob을 만들고 관리하는 방법에 대한 몇 가지 예도 제공했습니다.