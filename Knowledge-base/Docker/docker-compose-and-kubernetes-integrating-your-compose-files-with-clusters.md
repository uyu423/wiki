---
title: Docker Compose 및 Kubernetes: Compose 파일을 클러스터와 통합
description: 
published: true
date: 2023-02-17T18:02:28.685Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:24:42.380Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Docker Compose and Kubernetes: Integrating Your Compose Files with Clusters***English** version of this document is available*](/en/Knowledge-base/Docker/docker-compose-and-kubernetes-integrating-your-compose-files-with-clusters)
{.links-list}



# Docker Compose 및 Kubernetes: Compose 파일을 클러스터와 통합

이 기사에서는 Docker Compose와 Kubernetes를 함께 사용하는 방법을 살펴보겠습니다. 두 가지를 함께 사용하려는 이유를 살펴보는 것으로 시작하겠습니다. 그런 다음 Kubernetes에서 Compose 파일을 사용하는 방법의 예를 살펴보겠습니다.

Docker Compose는 훌륭한 개발 도구입니다. 이를 통해 YAML 파일로 애플리케이션 환경을 정의한 다음 단일 명령으로 애플리케이션을 가동할 수 있습니다.

Kubernetes는 컨테이너화된 애플리케이션을 대규모로 배포하고 관리하기 위한 훌륭한 도구입니다. 이를 통해 애플리케이션의 원하는 상태를 정의할 수 있으며 애플리케이션이 원하는 상태와 항상 일치하는지 확인할 수 있습니다.

Kubernetes의 장점 중 하나는 랩톱, 서버 또는 클라우드 등 어디에서나 실행할 수 있다는 것입니다. 즉, Kubernetes를 사용하여 프로덕션 환경뿐만 아니라 개발 환경도 관리할 수 있습니다.

개발에 Docker Compose를 사용 중이고 애플리케이션을 Kubernetes에 배포하려는 경우 도구를 사용하여 Compose 파일에서 Kubernetes Manifest 파일을 생성해야 합니다. 이 매니페스트 파일은 애플리케이션의 원하는 상태를 정의하고 Kubernetes는 이를 사용하여 애플리케이션이 원하는 상태와 항상 일치하는지 확인합니다.

Compose 파일에서 Kubernetes Manifest 파일을 생성할 수 있는 몇 가지 도구가 있지만 여기서는 Kompose를 사용할 것입니다. Kompose는 Compose 파일을 Kubernetes Manifest 파일로 변환하기 위해 특별히 설계된 도구입니다.

Kompose를 사용하려면 Docker와 Kubernetes가 모두 설치되어 있어야 합니다. Kubernetes를 아직 설치하지 않은 경우 Minikube를 사용할 수 있습니다. Minikube는 노트북에서 단일 노드 Kubernetes 클러스터를 실행할 수 있게 해주는 도구입니다.

Docker와 Kubernetes가 설치되면 다음 명령을 사용하여 Kompose를 설치할 수 있습니다.

```
curl -L https://github.com/kubernetes/kompose/releases/download/v1.19.0/kompose-linux-amd64 -o /usr/local/bin/kompose
```

Kompose가 설치되면 다음 명령을 사용하여 Compose 파일에서 Kubernetes 매니페스트 파일을 생성하는 데 사용할 수 있습니다.

```
kompose -f /path/to/compose/file.yml -o /path/to/manifest/file.yml
```

그러면 `/path/to/manifest/` 디렉터리에 `file.yml`이라는 Kubernetes 매니페스트 파일이 생성됩니다.

Kubernetes Manifest 파일이 있으면 `kubectl` 명령을 사용하여 애플리케이션을 Kubernetes에 배포할 수 있습니다. `kubectl` 명령은 Kubernetes용 명령줄 인터페이스입니다.

애플리케이션을 배포하려면 Kubernetes 클러스터가 있어야 합니다. Minikube를 사용하는 경우 다음 명령을 사용하여 Kubernetes 클러스터를 시작할 수 있습니다.

```
minikube start
```

Kubernetes 클러스터가 실행되면 다음 명령을 사용하여 애플리케이션을 클러스터에 배포할 수 있습니다.

```
kubectl apply -f /path/to/manifest/file.yml
```

이렇게 하면 애플리케이션이 Kubernetes에 배포됩니다. 애플리케이션이 배포되면 `kubectl` 명령을 사용하여 관리할 수 있습니다. 예를 들어 `kubectl` 명령을 사용하여 다음 명령으로 배포의 포드를 나열할 수 있습니다.

```
kubectl get pods
```

`kubectl` 명령을 사용하여 특정 팟(Pod)에 대한 자세한 정보를 얻을 수도 있습니다. 예를 들어 목록의 첫 번째 포드에 대한 자세한 정보를 얻으려면 다음 명령을 사용할 수 있습니다.

```
kubectl describe pod pod-name
```

애플리케이션이 Kubernetes에서 실행되면 `kubectl` 명령을 사용하여 액세스할 수 있습니다. 예를 들어 애플리케이션의 URL을 가져오려면 다음 명령을 사용할 수 있습니다.

```
kubectl get service my-app-name
```

애플리케이션의 URL이 출력됩니다. 그런 다음 해당 URL에서 애플리케이션에 액세스할 수 있습니다.

## Kubernetes와 Compose 파일 통합

Docker Compose와 Kubernetes를 함께 사용하려는 이유를 살펴보았으므로 이제 Kubernetes에서 Compose 파일을 사용하는 방법을 살펴보겠습니다.

Compose 파일에서 Kubernetes Manifest 파일을 생성하기 위해 `kompose` 명령을 사용할 것입니다. [Docker Compose 설명서](https://docs.docker.com/compose/)의 `docker-compose.yml` 파일을 사용하겠습니다.

이 Compose 파일에서 Kubernetes 매니페스트 파일을 생성하려면 다음 명령을 사용할 수 있습니다.

```
kompose -f docker-compose.yml -o kubernetes.yml
```

이렇게 하면 현재 디렉터리에 'kubernetes.yml'이라는 Kubernetes 매니페스트 파일이 생성됩니다.

이 파일에 무엇이 있는지 살펴보겠습니다. 가장 먼저 눈에 띄는 것은 파일 상단에 `apiVersion: extensions/v1beta1` 행이 있다는 것입니다. 이 줄은 Kubernetes에 `extensions/v1beta1` API 버전을 사용하고 있음을 알려줍니다.

다음으로 `kind: Deployment` 라인이 있습니다. 이 줄은 Kubernetes에 배포를 생성할 것임을 알립니다. 배치는 팟(Pod) 그룹을 나타내는 Kubernetes 오브젝트입니다.

그 다음에는 `metadata` 섹션이 있습니다. 이 섹션에는 배포에 대한 메타데이터가 포함되어 있습니다. 이 섹션에서 걱정해야 할 유일한 것은 `name` 필드입니다. 이 필드에는 배포 이름이 포함됩니다. 이 경우 배포 이름은 'compose-example'입니다.

다음으로 `spec` 섹션이 있습니다. 이 섹션에는 배포 사양이 포함되어 있습니다. 가장 먼저 지정해야 하는 것은 `replicas` 필드입니다. 이 필드는 배포에서 실행하려는 포드 수를 Kubernetes에 알려줍니다. 이 경우 두 개의 포드를 실행할 것입니다.

그 다음에는 `selector` 섹션이 있습니다. 이 섹션은 배포에 포함할 포드를 Kubernetes에 알려줍니다. 이 경우 `app=web` 레이블이 있는 모든 팟(Pod)을 포함할 것입니다.

다음으로 `템플릿` 섹션이 있습니다. 이 섹션에는 포드 템플릿의 정의가 포함되어 있습니다. 포드 템플릿은 포드의 구성을 정의하는 Kubernetes 개체입니다.

포드 템플릿에서 가장 먼저 정의해야 하는 것은 `metadata` 섹션입니다. 이 섹션에는 포드에 대한 메타데이터가 포함되어 있습니다. 이 섹션에서 걱정해야 할 유일한 것은 `labels` 필드입니다. 이 필드에는 팟(Pod)에 적용될 레이블이 포함되어 있습니다. 이 경우 포드에 `app=web` 레이블을 적용할 것입니다.

그 다음에는 `spec` 섹션이 있습니다. 이 섹션에는 포드의 사양이 포함되어 있습니다. 이 섹션에서 가장 먼저 지정해야 하는 것은 `containers` 필드입니다. 이 필드에는 포드에서 실행될 컨테이너 목록이 포함됩니다. 이 경우 하나의 컨테이너만 실행할 것입니다.

다음으로 컨테이너의 정의가 있습니다. 가장 먼저 정의해야 할 것은 컨테이너의 `이름`입니다. 이 경우 컨테이너를 `web`이라고 부를 것입니다.

그 다음에는 `image` 필드가 있습니다. 이 필드는 Kubernetes에 컨테이너에 사용할 도커 이미지를 알려줍니다. 이 경우에는 `nginx` 도커 이미지를 사용하겠습니다.

다음으로 `ports` 필드가 있습니다. 이 필드는 컨테이너에서 노출할 포트를 Kubernetes에 알려줍니다. 이 경우 포트 `80`을 노출할 것입니다.

마지막으로 `resources` 필드가 있습니다. 이 필드를 사용하면 컨테이너에 필요한 리소스를 지정할 수 있습니다. 이 경우 컨테이너에 `200m`의 CPU와 `128Mi`의 메모리가 필요하다고 지정합니다.

이것은 팟(Pod)을 정의하는 데 필요한 모든 것입니다. 포드가 정의되면 다음 명령을 실행하여 배포를 생성할 수 있습니다.

```
kubectl apply -f kubernetes.yml
```

이렇게 하면 'compose-example'이라는 배포가 생성됩니다. 다음 명령을 실행하여 배포를 볼 수 있습니다.

```
kubectl get deployments
```

다음 명령을 실행하여 배포의 일부인 포드를 볼 수도 있습니다.

```
kubectl get pods
```

`kubectl` 명령을 사용하여 특정 팟(Pod)에 대한 자세한 정보를 얻을 수 있습니다. 예를 들어 목록의 첫 번째 포드에 대한 자세한 정보를 얻으려면 다음 명령을 사용할 수 있습니다.

```
kubectl describe pod pod-name
```

애플리케이션이 Kubernetes에서 실행되면 `kubectl` 명령을 사용하여 액세스할 수 있습니다. 예를 들어 애플리케이션의 URL을 가져오려면 다음 명령을 사용할 수 있습니다.

```
kubectl get service compose-example
```

애플리케이션의 URL이 출력됩니다. 그런 다음 해당 URL에서 애플리케이션에 액세스할 수 있습니다.

## 결론

이 기사에서는 Docker Compose와 Kubernetes를 함께 사용하는 방법을 살펴보았습니다. Compose 파일에서 Kubernetes Manifest 파일을 생성하기 위해 Kompose를 사용하는 방법을 살펴보았습니다. 또한 `kubectl` 명령을 사용하여 애플리케이션을 Kubernetes에 배포하는 방법도 살펴보았습니다.