---
title: Kubernetes con Tekton: Implementación de canalizaciones de CI/CD para sus aplicaciones
description: 
published: true
date: 2023-02-14T13:33:36.364Z
tags: 
editor: markdown
dateCreated: 2023-02-14T13:33:34.606Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes with Tekton: Implementing CI/CD Pipelines for Your Applications***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-tekton-implementing-cicd-pipelines-for-your-applications)
{.links-list}


Kubernetes es un sistema de orquestación de contenedores de código abierto para automatizar la implementación, el escalado y la administración de aplicaciones. Tekton es un conjunto de herramientas de código abierto para crear, probar e implementar aplicaciones nativas de la nube en Kubernetes.

En este artículo, le mostraremos cómo usar Tekton para configurar una canalización de integración continua/implementación continua (CI/CD) para sus aplicaciones de Kubernetes.

Cubriremos los siguientes temas:

* Configuración de una tubería de Tekton
* Configuración de tareas de Tekton
* Creación de una ejecución de tubería de Tekton

## Configuración de una canalización de Tekton

Lo primero que debemos hacer es configurar una tubería de Tekton. Una canalización de Tekton es una colección de tareas que se pueden ejecutar en orden. Cada tarea en una canalización de Tekton se puede ejecutar en paralelo o secuencialmente.

En este ejemplo, crearemos una canalización de Tekton con dos tareas:

* Una tarea de construcción que construye nuestro código de aplicación
* Una tarea de implementación que implementa nuestra aplicación en un clúster de Kubernetes

Para configurar nuestra canalización de Tekton, usaremos la herramienta de línea de comandos `tkn`.

Primero, necesitamos crear un archivo llamado `build-deploy-pipeline.yaml` con los siguientes contenidos:

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

En este archivo, hemos definido una canalización de Tekton con dos tareas: `build-task` y `deploy-task`. El campo `taskRef` especifica el nombre de la plantilla de tareas de Tekton que debe usarse para cada tarea.

A continuación, debemos crear un archivo llamado `build-task-template.yaml` con los siguientes contenidos:

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

Este archivo define una plantilla de tarea de Tekton para la `tarea de compilación` en nuestra canalización. La sección `inputs` define los recursos de entrada para la tarea, que en este caso es un repositorio Git que contiene el código fuente de nuestra aplicación. La sección `outputs` define los recursos de salida para la tarea, que en este caso es una imagen de Docker que contiene el código de nuestra aplicación.

La sección `pasos` define los pasos que se deben ejecutar para la tarea. En este caso, tenemos un solo paso que ejecuta el comando `go build` para construir el código de nuestra aplicación.

A continuación, debemos crear un archivo llamado `deploy-task-template.yaml` con los siguientes contenidos:

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

Este archivo define una plantilla de tarea de Tekton para la `tarea de implementación` en nuestra canalización. La sección `inputs` define los recursos de entrada para la tarea, que en este caso es una imagen de Docker que contiene el código de nuestra aplicación. La sección `parameters` define los parámetros para la tarea, que en este caso es el espacio de nombres en el que se debe implementar nuestra aplicación.

La sección `pasos` define los pasos que se deben ejecutar para la tarea. En este caso, tenemos un solo paso que ejecuta el comando `k8s-deploy` para implementar nuestra aplicación en un clúster de Kubernetes.

## Configuración de tareas de Tekton

Ahora que hemos creado nuestra canalización de Tekton, debemos configurar nuestras tareas de Tekton.

Primero, necesitamos crear un archivo llamado `build-task-parameters.yaml` con los siguientes contenidos:

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

En este archivo, hemos definido una ejecución de tarea de Tekton para la `tarea de compilación` en nuestra canalización. El campo `taskRef` especifica el nombre de la plantilla de tareas de Tekton que debe usarse para la tarea.

La sección `entradas` define los recursos de entrada para la tarea. En este caso, estamos usando un repositorio Git que contiene el código fuente de nuestra aplicación. Los parámetros `url` y `revision` especifican la URL y la revisión del repositorio de Git.

La sección `outputs` define los recursos de salida para la tarea. En este caso, estamos usando una imagen de Docker para almacenar nuestro código de aplicación creado. El parámetro `url` especifica la URL de la imagen de Docker.

A continuación, debemos crear un archivo llamado `deploy-task-parameters.yaml` con los siguientes contenidos:

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

En este archivo, hemos definido una ejecución de tarea de Tekton para `deploy-task` en nuestra canalización. El campo `taskRef` especifica el nombre de la plantilla de tareas de Tekton que debe usarse para la tarea.

La sección `entradas` define los recursos de entrada para la tarea. En este caso, estamos usando una imagen de Docker que contiene el código de nuestra aplicación. El parámetro `url` especifica la URL de la imagen de Docker.

La sección `outputs` define los parámetros de salida para la tarea. En este caso, estamos utilizando el parámetro `namespace` para especificar el espacio de nombres en el que se debe implementar nuestra aplicación.

## Creación de una ejecución de canalización de Tekton

Ahora que hemos configurado nuestras tareas de Tekton, podemos crear una ejecución de canalización de Tekton para ejecutar nuestra canalización.

Primero, necesitamos crear un archivo llamado `pipeline-run.yaml` con los siguientes contenidos:

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

En este archivo, hemos definido una ejecución de canalización de Tekton para nuestra `construcción-despliegue-tubería`. El campo `pipelineRef` especifica el nombre de la tubería de Tekton que debe usarse para la ejecución de la tubería.

El campo `serviceAccountName` especifica el nombre de la cuenta de servicio de Kubernetes que debe usarse para la ejecución de la canalización.

El campo `tiempo de espera` especifica la duración máxima de la ejecución de la canalización.

La sección `workspaces` define los espacios de trabajo que deben usarse para la ejecución de la canalización. En este caso, estamos usando dos espacios de trabajo: `source-repo` y `application-image-repo`. Estos espacios de trabajo se utilizarán para almacenar los recursos de entrada y salida para nuestras tareas.

Para crear la ejecución de la canalización, podemos usar la herramienta de línea de comandos `tkn`:

```
tkn pipeline start build-deploy-pipeline-run --workspaces=source-repo=source-repo-ws,application-image-repo=application-image-repo-ws
```

Este comando creará una ejecución de canalización con el nombre `build-deploy-pipeline-run`. El indicador `--workspaces` especifica los espacios de trabajo que deben usarse para la ejecución de la canalización.

Una vez que se ha creado la ejecución de la tubería, podemos usar la herramienta de línea de comandos `tkn` para obtener el estado de la ejecución de la tubería:

```
tkn pipeline status build-deploy-pipeline-run
```

Este comando generará el estado de la ejecución de la canalización `build-deploy-pipeline-run`.

## Conclusión

En este artículo, le mostramos cómo usar Tekton para configurar una canalización de integración continua/implementación continua (CI/CD) para sus aplicaciones de Kubernetes.