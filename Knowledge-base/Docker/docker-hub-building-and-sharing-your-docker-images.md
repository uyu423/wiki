---
title: Docker 허브: Docker 이미지 빌드 및 공유
description: 
published: true
date: 2023-02-14T01:17:24.381Z
tags: 
editor: markdown
dateCreated: 2023-02-14T01:17:17.198Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Docker Hub: Building and Sharing Your Docker Images***English** document is available*](/en/Knowledge-base/Docker/docker-hub-building-and-sharing-your-docker-images)
{.links-list}


# Docker 허브: Docker 이미지 빌드 및 공유

Docker Hub는 Docker 이미지를 빌드하고 공유하기 위한 클라우드 기반 레지스트리 서비스입니다. Docker Hub를 사용하면 애플리케이션을 쉽게 빌드, 테스트 및 배포할 수 있습니다.

Docker Hub는 무료 플랜과 유료 Pro 플랜을 제공합니다. 무료 플랜을 사용하면 공개 리포지토리를 무제한으로 생성할 수 있지만 개인 리포지토리는 1개로 제한됩니다. Pro 플랜을 사용하면 공개 및 비공개 리포지토리를 무제한으로 생성할 수 있습니다.

Docker Hub에 이미지를 푸시하는 방법에는 두 가지가 있습니다.

1. **docker push** 명령

2. **도커 허브 웹 인터페이스**

## 도커 푸시 명령

**docker push** 명령은 이미지를 Docker 레지스트리에 푸시합니다. Docker 레지스트리는 이미지를 저장하고 제공하는 호스트입니다.

**docker push** 명령을 사용하려면 이미지 이름과 태그를 지정해야 합니다. 예를 들어 "latest" 태그가 있는 이미지를 Docker Hub에 푸시하려면 다음 명령을 사용합니다.

```
docker push <username>/<image>:<tag>
```

<username>을 Docker Hub 사용자 이름으로, <image>를 이미지 이름으로, <tag>를 태그로 바꿉니다.

## 도커 허브 웹 인터페이스

Docker Hub 웹 인터페이스는 Docker 이미지를 푸시, 풀 및 관리하는 데 사용할 수 있는 웹 기반 애플리케이션입니다.

웹 인터페이스를 사용하여 Docker Hub에 이미지를 푸시하려면 먼저 Docker Hub 계정에 로그인하십시오. 그런 다음 **리포지토리 생성** 버튼을 클릭합니다.

리포지토리 이름과 설명을 입력한 다음 **만들기** 버튼을 클릭합니다.

그런 다음 **파일 업로드** 버튼을 클릭합니다.

업로드할 이미지를 선택한 다음 **업로드** 버튼을 클릭합니다.

마지막으로 **게시** 버튼을 클릭합니다.

이제 이미지가 Docker Hub의 리포지토리로 푸시됩니다.

## 결론

Docker Hub는 Docker 이미지를 전 세계와 공유할 수 있는 좋은 방법입니다. Docker Hub를 사용하면 애플리케이션을 쉽게 빌드, 테스트 및 배포할 수 있습니다.