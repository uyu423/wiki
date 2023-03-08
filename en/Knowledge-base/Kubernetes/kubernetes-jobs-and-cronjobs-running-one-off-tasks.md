---
title: Kubernetes Jobs and CronJobs: Running One-Off Tasks
description: 
published: true
date: 2023-02-08T22:32:47.612Z
tags: 
editor: markdown
dateCreated: 2023-02-08T22:32:40.448Z
---

- [Kubernetes Jobs y CronJobs: ejecución de tareas únicas***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-jobs-and-cronjobs-running-one-off-tasks)
{.links-list}
- [Kubernetes 作业和 CronJobs：运行一次性任务***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-jobs-and-cronjobs-running-one-off-tasks)
{.links-list}
- [Kubernetes 작업 및 CronJob: 일회성 작업 실행***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-jobs-and-cronjobs-running-one-off-tasks)
{.links-list}


# Kubernetes Jobs and CronJobs: Running One-Off Tasks

In this article, we'll be discussing Jobs and CronJobs in Kubernetes and how to use them for running one-off tasks. We'll go over what each of these resource types are and what they can be used for, and we'll also provide some examples of how to create and manage Jobs and CronJobs.

## Jobs

Jobs are a type of Kubernetes resource that can be used to run one-off tasks. A Job will create one or more pods and ensure that the pods are successfully completed before it is considered successful. If a pod fails, the Job will automatically restart it.

Jobs can be used for a variety of tasks, such as batch jobs, data imports, database backups, and more.

To create a Job, you will need to create a Job manifest. The Job manifest defines the Job's specs, such as the number of replicas, the pod template, and the restart policy.

Here is an example Job manifest:

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

In the example above, we've defined a Job with a single replica. The Job will create a pod using the busybox image and run the command "echo Hello World!". The Job will also have a restartPolicy of Never, which means that it will not automatically restart if the pod fails.

To create the Job, you can use the kubectl apply command:

```
kubectl apply -f my-job.yaml
```

You can also use the kubectl create command:

```
kubectl create job my-job --image=busybox -- echo "Hello World!"
```

Once the Job is created, you can check its status using the kubectl get jobs command:

```
kubectl get jobs
NAME      DESIRED   SUCCESSFUL   AGE
my-job    1         1            5s
```

You can also check the status of the pod that the Job creates:

```
kubectl get pods
NAME                    READY   STATUS      RESTARTS   AGE
my-job-9f6b8b4b4-6x8nw   0/1     Completed   0          6s
```

Once the Job is completed, you can delete it using the kubectl delete job command:

```
kubectl delete job my-job
```

## CronJobs

CronJobs are a type of Kubernetes resource that can be used to run recurring tasks. A CronJob will create a Job at a specified time or interval.

CronJobs can be used for a variety of tasks, such as database backups, system maintenance, and more.

To create a CronJob, you will need to create a CronJob manifest. The CronJob manifest defines the CronJob's specs, such as the schedule, the Job template, and the concurrency policy.

Here is an example CronJob manifest:

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

In the example above, we've defined a CronJob that will run every 4 hours. The CronJob will create a Job using the busybox image and run the command "echo Hello World!". The Job will also have a restartPolicy of OnFailure, which means that it will automatically restart if the pod fails. The CronJob will have a concurrencyPolicy of Forbid, which means that only one Job can be run at a time.

To create the CronJob, you can use the kubectl apply command:

```
kubectl apply -f my-cronjob.yaml
```

You can also use the kubectl create command:

```
kubectl create cronjob my-cronjob --image=busybox -- echo "Hello World!"
```

Once the CronJob is created, you can check its status using the kubectl get cronjobs command:

```
kubectl get cronjobs
NAME       SCHEDULE      SUSPEND   ACTIVE   LAST SCHEDULE   AGE
my-cronjob   0 */4 * * *   False     0        <none>          5s
```

You can also check the status of the Job that the CronJob creates:

```
kubectl get jobs
NAME                          DESIRED   SUCCESSFUL   AGE
my-cronjob-1586409600          1         1            5s
```

Once the Job is completed, you can delete it using the kubectl delete job command:

```
kubectl delete job my-cronjob-1586409600
```

You can also delete the CronJob using the kubectl delete cronjob command:

```
kubectl delete cronjob my-cronjob
```

## Conclusion

In this article, we discussed Jobs and CronJobs in Kubernetes and how to use them for running one-off tasks. We went over what each of these resource types are and what they can be used for, and we also provided some examples of how to create and manage Jobs and CronJobs.