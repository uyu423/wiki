---
title: Docker 이미지 관리: 레지스트리에 태깅 및 푸시
description: 
published: true
date: 2023-02-01T21:43:22.575Z
tags: 
editor: markdown
dateCreated: 2023-02-01T21:43:18.426Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Docker Image Management: Tagging and Pushing to a Registry***English** document is available*](/en/Knowledge-base/Docker/docker-image-management-tagging-and-pushing-to-a-registry)
{.links-list}



# Docker 이미지 관리: 태깅 및 레지스트리로 푸시

Docker 이미지는 컨테이너 생성의 기초입니다. 기본적으로 이미지는 Docker, Inc.에서 관리하는 공개 레지스트리인 Docker Hub에서 가져옵니다. 그러나 자체 레지스트리를 실행하고 이미지를 여기에 푸시할 수도 있습니다.

이 문서에서는 Docker 이미지를 관리하는 두 가지 방법인 태그 지정 및 레지스트리 푸시에 대해 설명합니다.

## 이미지 태그하기

`도커 태그`로 이미지에 태그를 지정할 수 있습니다. 예를 들어 버전 번호로 이미지에 레이블을 지정하는 데 유용합니다. 이미지에 태그를 지정하려면 다음 구문을 사용하십시오.

```
docker tag <image> <tag>
```

예를 들어 이미지 `nginx`에 `1.7.9` 태그를 지정하려면 다음 명령을 실행합니다.

```
docker tag nginx 1.7.9
```

태깅은 컨테이너를 실행할 때 이미지의 특정 버전을 지정할 수 있기 때문에 이미지 관리에 중요합니다. 기본적으로 이미지의 최신 버전에 해당하는 `latest` 태그가 사용됩니다.

## 레지스트리에 이미지 푸시

이미지에 태그를 지정하면 레지스트리에 이미지를 푸시할 수 있습니다. `docker push` 명령을 사용하여 이미지를 레지스트리로 푸시할 수 있습니다. 이 명령의 구문은 다음과 같습니다.

```
docker push <registry>/<repository>/<image>
```

예를 들어 `nginx` 이미지를 Docker Hub에 푸시하려면 다음 명령을 사용합니다.

```
docker push nginx
```

레지스트리에 이미지를 푸시하는 것은 다른 사람과 이미지를 공유하는 방법입니다. 이미지를 레지스트리에 푸시하면 다른 사람이 이미지를 가져와서 사용할 수 있습니다.

## 요약

이 문서에서는 Docker 이미지를 관리하는 두 가지 방법인 태그 지정 및 레지스트리로 푸시에 대해 배웠습니다. 이미지 태그 지정은 버전 번호 또는 기타 정보로 레이블을 지정하는 방법입니다. 이미지를 레지스트리에 푸시하는 것은 이미지를 다른 사람과 공유하는 방법입니다.