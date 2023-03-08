---
title: Kotlin 및 Kubernetes: 애플리케이션 배포 및 확장
description: 
published: true
date: 2023-02-12T16:18:08.333Z
tags: 
editor: markdown
dateCreated: 2023-02-12T16:18:01.483Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and Kubernetes: Deploying and Scaling Your Applications***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-kubernetes-deploying-and-scaling-your-applications)
{.links-list}


# Kotlin 및 Kubernetes: 애플리케이션 배포 및 확장

Kotlin은 동시성 및 코루틴 지원으로 인기를 얻고 있는 JVM 언어입니다. Kubernetes는 컨테이너화된 애플리케이션을 배포, 관리 및 확장하는 데 널리 사용되는 컨테이너 오케스트레이션 플랫폼입니다.

이 기사에서는 Kotlin과 Kubernetes를 사용하여 애플리케이션을 배포하고 확장하는 방법을 살펴봅니다. 또한 이러한 기술을 함께 사용하기 위한 몇 가지 모범 사례에 대해서도 알아봅니다.

## Kotlin 및 Kubernetes로 애플리케이션 컨테이너화

Kubernetes에 애플리케이션을 배포하는 첫 번째 단계는 애플리케이션을 컨테이너화하는 것입니다. Docker, rkt 또는 LXD와 같은 모든 컨테이너화 기술을 사용할 수 있습니다. 이 문서에서는 Docker를 사용합니다.

Docker는 애플리케이션을 쉽게 패키징하고 배포할 수 있게 해주는 컨테이너화 플랫폼입니다. Linux 컨테이너를 사용하여 애플리케이션을 위한 격리된 환경을 만듭니다.

Kotlin 애플리케이션을 컨테이너화하려면 먼저 `Dockerfile`을 만들어야 합니다. `Dockerfile`은 도커 이미지를 빌드하는 방법에 대한 도커 지침이 포함된 텍스트 파일입니다.

다음은 Kotlin 애플리케이션을 위한 간단한 `Dockerfile`입니다.

```Dockerfile
FROM openjdk:8-jdk-alpine

VOLUME /tmp

ARG JAR_FILE

COPY ${JAR_FILE} app.jar

ENTRYPOINT ["java","-jar","/app.jar"]
```

이 `Dockerfile`은 `openjdk:8-jdk-alpine` 도커 이미지를 기본 이미지로 사용합니다. 그런 다음 `/tmp`에 볼륨을 생성하고 `app.jar` 파일을 컨테이너에 복사합니다. `ENTRYPOINT` 명령은 컨테이너가 시작될 때 실행될 명령을 지정하는 데 사용됩니다.

이제 `Dockerfile`이 있으므로 `docker build` 명령을 사용하여 도커 이미지를 빌드할 수 있습니다. 다음은 `Dockerfile`에서 도커 이미지를 빌드하는 명령입니다.

```
docker build -t kotlin-app:latest .
```

이 명령은 `kotlin-app:latest` 태그가 있는 도커 이미지를 빌드합니다. 이제 `docker run` 명령을 사용하여 도커 컨테이너에서 애플리케이션을 실행할 수 있습니다.

```
docker run -d -p 8080:8080 kotlin-app:latest
```

이 명령은 분리 모드에서 컨테이너를 시작하고 컨테이너의 포트 '8080'을 호스트의 포트 '8080'에 노출합니다. 이제 `http://localhost:8080`에서 애플리케이션에 액세스할 수 있습니다.

## Kubernetes에 애플리케이션 배포

이제 애플리케이션을 컨테이너화했으므로 Kubernetes에 배포할 수 있습니다. Kubernetes는 컨테이너화된 애플리케이션을 배포, 관리 및 확장하는 데 사용할 수 있는 컨테이너 오케스트레이션 플랫폼입니다.

Kubernetes에 애플리케이션을 배포하는 방법에는 여러 가지가 있습니다. 이 기사에서는 `kubectl` 명령줄 도구를 사용합니다.

'kubectl' 도구를 사용하여 Kubernetes 리소스를 만들고 관리할 수 있습니다. 이를 사용하여 `Deployment` 리소스를 생성합니다. Kubernetes에서 애플리케이션 배포를 관리하는 데 'Deployment' 리소스가 사용됩니다.

다음은 애플리케이션의 `Deployment` 리소스를 생성하는 `kubectl` 명령입니다.

```
kubectl create deployment kotlin-app --image=kotlin-app:latest
```

이 명령은 `kotlin-app`이라는 이름으로 `Deployment` 리소스를 생성합니다. 배포를 위해 `kotlin-app:latest` 도커 이미지를 사용합니다.

`Deployment` 리소스가 생성되면 Kubernetes는 애플리케이션을 실행할 `Pod`를 생성합니다. 'Pod'는 Kubernetes에 함께 배포되는 하나 이상의 컨테이너 그룹입니다.

애플리케이션의 `Pod`는 `default` 네임스페이스에 생성됩니다. `kubectl get pods` 명령을 사용하여 `Pod`를 볼 수 있습니다.

```
kubectl get pods

NAME                             READY   STATUS    RESTARTS   AGE
kotlin-app-7567cf6b7f-x8b8j       1/1     Running   0          2m9s
```

'Pod'가 실행되고 있는 것을 볼 수 있습니다. 이제 `http://localhost:8080`에서 애플리케이션에 액세스할 수 있습니다.

## Kubernetes에서 애플리케이션 확장

Kubernetes를 사용하면 애플리케이션을 쉽게 확장할 수 있습니다. `kubectl` 도구를 사용하여 애플리케이션을 확장할 수 있습니다.

다음은 애플리케이션을 10개의 복제본으로 확장하는 명령입니다.

```
kubectl scale deployment kotlin-app --replicas=10
```

이 명령은 `Deployment` 리소스를 10개의 복제본으로 확장합니다. Kubernetes는 추가 복제본을 실행하기 위해 추가 `Pod`를 생성합니다. `kubectl get pods` 명령을 사용하여 `Pods`를 볼 수 있습니다.

```
kubectl get pods

NAME                             READY   STATUS    RESTARTS   AGE
kotlin-app-7567cf6b7f-x8b8j       1/1     Running   0          9m
kotlin-app-7567cf6b7f-b4vh2       1/1     Running   0          9m
kotlin-app-7567cf6b7f-4xb4p       1/1     Running   0          9m
kotlin-app-7567cf6b7f-c66r8       1/1     Running   0          9m
kotlin-app-7567cf6b7f-f8j8k       1/1     Running   0          9m
kotlin-app-7567cf6b7f-hbk8r       1/1     Running   0          9m
kotlin-app-7567cf6b7f-kxw6k       1/1     Running   0          9m
kotlin-app-7567cf6b7f-mjsjl       1/1     Running   0          9m
kotlin-app-7567cf6b7f-nlx89       1/1     Running   0          9m
kotlin-app-7567cf6b7f-snx4x       1/1     Running   0          9m
```

Kubernetes가 10개의 복제본을 실행하기 위해 10개의 'Pod'를 생성한 것을 볼 수 있습니다. 이제 `http://localhost:8080`에서 애플리케이션에 액세스할 수 있습니다.

## Kotlin 및 Kubernetes 사용을 위한 모범 사례

다음은 Kotlin 및 Kubernetes 사용에 대한 몇 가지 모범 사례입니다.

* Kubernetes에 배포할 애플리케이션을 개발하려면 Kotlin과 같은 JVM 언어를 사용하세요. 이렇게 하면 Kotlin의 동시성 및 코루틴 기능을 사용하여 효율적이고 확장 가능한 애플리케이션을 작성할 수 있습니다.

* `Deployment` 및 `Service`와 같은 Kubernetes 리소스를 사용하여 애플리케이션의 배포 및 확장을 관리합니다.

* `kubectl` 도구를 사용하여 Kubernetes 리소스와 상호 작용합니다.

* `Docker`를 사용하여 애플리케이션을 컨테이너화하십시오.

* `kubectl` 도구를 사용하여 애플리케이션을 확장하십시오.