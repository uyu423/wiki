---
title: Kubernetes Jobs y CronJobs: ejecución de tareas únicas
description: 
published: true
date: 2023-02-08T22:32:42.116Z
tags: 
editor: markdown
dateCreated: 2023-02-08T22:32:40.447Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes Jobs and CronJobs: Running One-Off Tasks***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-jobs-and-cronjobs-running-one-off-tasks)
{.links-list}


# Kubernetes Jobs y CronJobs: ejecución de tareas únicas

En este artículo, analizaremos Jobs y CronJobs en Kubernetes y cómo usarlos para ejecutar tareas únicas. Repasaremos qué es cada uno de estos tipos de recursos y para qué se pueden usar, y también proporcionaremos algunos ejemplos de cómo crear y administrar Trabajos y CronJobs.

## Trabajos

Los trabajos son un tipo de recurso de Kubernetes que se puede usar para ejecutar tareas únicas. Un trabajo creará uno o más pods y se asegurará de que los pods se completen correctamente antes de que se considere exitoso. Si un pod falla, el trabajo lo reiniciará automáticamente.

Los trabajos se pueden usar para una variedad de tareas, como trabajos por lotes, importaciones de datos, copias de seguridad de bases de datos y más.

Para crear un trabajo, deberá crear un manifiesto de trabajo. El manifiesto del trabajo define las especificaciones del trabajo, como la cantidad de réplicas, la plantilla del pod y la política de reinicio.

Aquí hay un ejemplo de manifiesto de trabajo:

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

En el ejemplo anterior, hemos definido un trabajo con una única réplica. El trabajo creará un pod usando la imagen de busybox y ejecutará el comando "echo Hello World!". El trabajo también tendrá una política de reinicio de Nunca, lo que significa que no se reiniciará automáticamente si falla el pod.

Para crear el trabajo, puede usar el comando kubectl apply:

```
kubectl apply -f my-job.yaml
```

También puede usar el comando kubectl create:

```
kubectl create job my-job --image=busybox -- echo "Hello World!"
```

Una vez que se crea el trabajo, puede verificar su estado usando el comando kubectl get jobs:

```
kubectl get jobs
NAME      DESIRED   SUCCESSFUL   AGE
my-job    1         1            5s
```

También puede verificar el estado del pod que crea el Trabajo:

```
kubectl get pods
NAME                    READY   STATUS      RESTARTS   AGE
my-job-9f6b8b4b4-6x8nw   0/1     Completed   0          6s
```

Una vez que se completa el trabajo, puede eliminarlo con el comando kubectl delete job:

```
kubectl delete job my-job
```

## Trabajos cron

Los CronJobs son un tipo de recurso de Kubernetes que se puede usar para ejecutar tareas recurrentes. Un CronJob creará un trabajo en un tiempo o intervalo específico.

CronJobs se puede usar para una variedad de tareas, como copias de seguridad de bases de datos, mantenimiento del sistema y más.

Para crear un CronJob, deberá crear un manifiesto de CronJob. El manifiesto de CronJob define las especificaciones de CronJob, como la programación, la plantilla de trabajo y la política de concurrencia.

Aquí hay un ejemplo de manifiesto de CronJob:

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

En el ejemplo anterior, hemos definido un CronJob que se ejecutará cada 4 horas. El CronJob creará un trabajo usando la imagen de busybox y ejecutará el comando "echo Hello World!". El trabajo también tendrá una política de reinicio de OnFailure, lo que significa que se reiniciará automáticamente si falla el pod. CronJob tendrá una política de concurrencia de Prohibir, lo que significa que solo se puede ejecutar un trabajo a la vez.

Para crear el CronJob, puede usar el comando kubectl apply:

```
kubectl apply -f my-cronjob.yaml
```

También puede usar el comando kubectl create:

```
kubectl create cronjob my-cronjob --image=busybox -- echo "Hello World!"
```

Una vez que se crea el CronJob, puede verificar su estado usando el comando kubectl get cronjobs:

```
kubectl get cronjobs
NAME       SCHEDULE      SUSPEND   ACTIVE   LAST SCHEDULE   AGE
my-cronjob   0 */4 * * *   False     0        <none>          5s
```

También puede verificar el estado del Trabajo que crea el CronJob:

```
kubectl get jobs
NAME                          DESIRED   SUCCESSFUL   AGE
my-cronjob-1586409600          1         1            5s
```

Una vez que se completa el trabajo, puede eliminarlo con el comando kubectl delete job:

```
kubectl delete job my-cronjob-1586409600
```

También puede eliminar el CronJob usando el comando kubectl delete cronjob:

```
kubectl delete cronjob my-cronjob
```

## Conclusión

En este artículo, discutimos Jobs y CronJobs en Kubernetes y cómo usarlos para ejecutar tareas únicas. Repasamos qué es cada uno de estos tipos de recursos y para qué se pueden usar, y también brindamos algunos ejemplos de cómo crear y administrar Trabajos y CronJobs.