---
title: 059: 스프링 부트 애플리케이션을 클라우드에 배포
description: 
published: true
date: 2023-02-04T22:32:15.591Z
tags: 
editor: markdown
dateCreated: 2023-02-04T22:32:13.953Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [059: Deploying a Spring Boot Application to the Cloud***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/059-deploying-a-spring-boot-application-to-the-cloud)
{.links-list}


# 059: 스프링 부트 애플리케이션을 클라우드에 배포

클라우드 컴퓨팅은 구성 가능한 컴퓨팅 리소스(예: 네트워크, 서버, 스토리지, 애플리케이션 및 서비스)의 공유 풀에 대한 유비쿼터스의 편리한 온디맨드 네트워크 액세스를 가능하게 하는 모델입니다. 퍼블릭, 프라이빗 또는 하이브리드와 같은 다양한 방식으로 배포할 수 있습니다.

이 게시물에서는 Spring Boot 애플리케이션을 클라우드에 배포하는 방법에 중점을 둘 것입니다. [Spring Cloud GCP](https://spring.io/projects/spring-cloud-gcp)의 예를 사용하여 Google Cloud Platform(GCP)에 Spring Boot 애플리케이션을 빠르고 쉽게 배포하는 방법을 보여줍니다.

## 전제 조건

- GCP 계정
- 스프링 부트 애플리케이션

## 1단계: GCP 프로젝트 만들기

먼저 GCP 프로젝트를 생성해야 합니다. 이는 [GCP 콘솔](https://console.cloud.google.com/)을 통해 수행할 수 있습니다.

## 2단계: Cloud Build 및 App Engine API 사용 설정

다음으로 Cloud Build 및 App Engine API를 사용 설정해야 합니다. 이는 [GCP 콘솔](https://console.cloud.google.com/apis/dashboard)을 통해 수행할 수 있습니다.

## 3단계: Cloud Build 트리거 만들기

이제 Cloud Build 트리거를 만들어야 합니다. 이는 [GCP 콘솔](https://console.cloud.google.com/cloud-build/triggers)을 통해 수행할 수 있습니다.

## 4단계: 애플리케이션 배포

마지막으로 애플리케이션을 배포할 수 있습니다. 이는 [GCP 콘솔](https://console.cloud.google.com/appengine/deploy)을 통해 수행할 수 있습니다.

## 결론

이 게시물에서는 GCP를 사용하여 Spring Boot 애플리케이션을 클라우드에 배포하는 방법을 살펴보았습니다.