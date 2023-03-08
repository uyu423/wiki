---
title: Kubernetes와 Tekton: 애플리케이션을 위한 CI/CD 파이프라인 구현
description: 
published: true
date: 2023-02-14T13:33:36.204Z
tags: 
editor: markdown
dateCreated: 2023-02-14T13:33:34.603Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes with Tekton: Implementing CI/CD Pipelines for Your Applications***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-tekton-implementing-cicd-pipelines-for-your-applications)
{.links-list}


Kubernetes는 애플리케이션 배포, 확장 및 관리를 자동화하기 위한 오픈 소스 컨테이너 오케스트레이션 시스템입니다. Tekton은 Kubernetes에서 클라우드 네이티브 애플리케이션을 구축, 테스트 및 배포하기 위한 오픈 소스 툴킷입니다.

이 기사에서는 Tekton을 사용하여 Kubernetes 애플리케이션에 대한 CI/CD(지속적인 통합/지속적인 배포) 파이프라인을 설정하는 방법을 보여줍니다.

다음 주제를 다룰 것입니다.

* Tekton 파이프라인 설정
* Tekton 작업 구성
* Tekton 파이프라인 실행 생성

## Tekton 파이프라인 설정

가장 먼저 해야 할 일은 Tekton 파이프라인을 설정하는 것입니다. Tekton 파이프라인은 순서대로 실행할 수 있는 작업 모음입니다. Tekton 파이프라인의 각 작업은 병렬 또는 순차적으로 실행될 수 있습니다.

이 예에서는 두 가지 작업으로 Tekton 파이프라인을 생성합니다.

* 애플리케이션 코드를 빌드하는 빌드 작업
* 애플리케이션을 Kubernetes 클러스터에 배포하는 배포 작업

Tekton 파이프라인을 설정하기 위해 `tkn` 명령줄 도구를 사용합니다.

먼저 다음 내용으로 `build-deploy-pipeline.yaml`이라는 파일을 만들어야 합니다.

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

이 파일에서 우리는 `build-task` 및 `deploy-task`의 두 가지 작업으로 Tekton 파이프라인을 정의했습니다. 'taskRef' 필드는 각 작업에 사용해야 하는 Tekton 작업 템플릿의 이름을 지정합니다.

다음으로 다음 내용으로 `build-task-template.yaml`이라는 파일을 만들어야 합니다.

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

이 파일은 파이프라인의 'build-task'에 대한 Tekton 작업 템플릿을 정의합니다. 'inputs' 섹션은 작업에 대한 입력 리소스를 정의합니다. 이 경우 애플리케이션 소스 코드가 포함된 Git 리포지토리입니다. `outputs` 섹션은 작업에 대한 출력 리소스를 정의합니다. 이 경우 애플리케이션 코드가 포함된 Docker 이미지입니다.

`단계` 섹션은 작업에 대해 실행해야 하는 단계를 정의합니다. 이 경우 애플리케이션 코드를 빌드하기 위해 `go build` 명령을 실행하는 단일 단계가 있습니다.

다음으로 다음 내용으로 `deploy-task-template.yaml`이라는 파일을 만들어야 합니다.

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

이 파일은 파이프라인의 'deploy-task'에 대한 Tekton 작업 템플릿을 정의합니다. 'inputs' 섹션은 작업에 대한 입력 리소스를 정의합니다. 이 경우 애플리케이션 코드가 포함된 Docker 이미지입니다. '매개변수' 섹션은 작업에 대한 매개변수를 정의합니다. 이 경우 애플리케이션이 배포되어야 하는 네임스페이스입니다.

`단계` 섹션은 작업에 대해 실행해야 하는 단계를 정의합니다. 이 경우 애플리케이션을 Kubernetes 클러스터에 배포하기 위해 `k8s-deploy` 명령을 실행하는 단일 단계가 있습니다.

## Tekton 작업 구성

이제 Tekton 파이프라인을 생성했으므로 Tekton 작업을 구성해야 합니다.

먼저 다음 내용으로 `build-task-parameters.yaml`이라는 파일을 만들어야 합니다.

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

이 파일에서 파이프라인의 'build-task'에 대한 Tekton 작업 실행을 정의했습니다. 'taskRef' 필드는 작업에 사용해야 하는 Tekton 작업 템플릿의 이름을 지정합니다.

'inputs' 섹션은 작업에 대한 입력 리소스를 정의합니다. 이 경우 애플리케이션 소스 코드가 포함된 Git 리포지토리를 사용하고 있습니다. `url` 및 `revision` 매개변수는 Git 리포지토리의 URL 및 개정을 지정합니다.

`outputs` 섹션은 작업의 출력 리소스를 정의합니다. 이 경우 빌드된 애플리케이션 코드를 저장하기 위해 Docker 이미지를 사용하고 있습니다. `url` 매개변수는 Docker 이미지의 URL을 지정합니다.

다음으로 다음 내용으로 `deploy-task-parameters.yaml`이라는 파일을 만들어야 합니다.

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

이 파일에서 파이프라인의 'deploy-task'에 대한 Tekton 작업 실행을 정의했습니다. 'taskRef' 필드는 작업에 사용해야 하는 Tekton 작업 템플릿의 이름을 지정합니다.

'inputs' 섹션은 작업에 대한 입력 리소스를 정의합니다. 이 경우 애플리케이션 코드가 포함된 Docker 이미지를 사용하고 있습니다. `url` 매개변수는 Docker 이미지의 URL을 지정합니다.

`outputs` 섹션은 태스크의 출력 매개변수를 정의합니다. 이 경우 애플리케이션을 배포해야 하는 네임스페이스를 지정하기 위해 `namespace` 매개변수를 사용하고 있습니다.

## Tekton 파이프라인 실행 만들기

이제 Tekton 작업을 구성했으므로 파이프라인을 실행할 Tekton 파이프라인 실행을 생성할 수 있습니다.

먼저 다음 내용으로 `pipeline-run.yaml`이라는 파일을 만들어야 합니다.

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

이 파일에서 `build-deploy-pipeline`에 대한 Tekton 파이프라인 실행을 정의했습니다. 'pipelineRef' 필드는 파이프라인 실행에 사용해야 하는 Tekton 파이프라인의 이름을 지정합니다.

'serviceAccountName' 필드는 파이프라인 실행에 사용해야 하는 Kubernetes 서비스 계정의 이름을 지정합니다.

'timeout' 필드는 파이프라인 실행의 최대 기간을 지정합니다.

'workspaces' 섹션은 파이프라인 실행에 사용해야 하는 작업 공간을 정의합니다. 이 경우에는 `source-repo` 및 `application-image-repo`라는 두 개의 작업 공간을 사용하고 있습니다. 이러한 작업 공간은 작업에 대한 입력 및 출력 리소스를 저장하는 데 사용됩니다.

파이프라인 실행을 생성하기 위해 `tkn` 명령줄 도구를 사용할 수 있습니다.

```
tkn pipeline start build-deploy-pipeline-run --workspaces=source-repo=source-repo-ws,application-image-repo=application-image-repo-ws
```

이 명령은 `build-deploy-pipeline-run`이라는 이름으로 실행되는 파이프라인을 생성합니다. `--workspaces` 플래그는 파이프라인 실행에 사용해야 하는 작업 공간을 지정합니다.

파이프라인 실행이 생성되면 `tkn` 명령줄 도구를 사용하여 파이프라인 실행 상태를 가져올 수 있습니다.

```
tkn pipeline status build-deploy-pipeline-run
```

이 명령은 `build-deploy-pipeline-run` 파이프라인 실행 상태를 출력합니다.

## 결론

이 기사에서는 Tekton을 사용하여 Kubernetes 애플리케이션에 대한 CI/CD(지속적인 통합/지속적인 배포) 파이프라인을 설정하는 방법을 설명했습니다.