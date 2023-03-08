---
title: 086: Kubernetes에 Spring Boot 애플리케이션 배포
description: 
published: true
date: 2023-02-05T16:32:17.769Z
tags: 
editor: markdown
dateCreated: 2023-02-05T16:32:16.104Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [086: Deploying a Spring Boot Application to Kubernetes***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/086-deploying-a-spring-boot-application-to-kubernetes)
{.links-list}


# 086: Kubernetes에 Spring Boot 애플리케이션 배포

Kubernetes는 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하기 위한 오픈 소스 시스템입니다.

Spring Boot는 웹 애플리케이션 및 마이크로 서비스를 구축하기 위한 인기 있는 Java 프레임워크입니다.

이 게시물에서는 Kubernetes에 Spring Boot 애플리케이션을 배포하는 방법을 보여줍니다.

## 전제 조건

- 쿠버네티스 클러스터
- 스프링 부트 애플리케이션

## 애플리케이션 배포

1. 애플리케이션에 대한 Kubernetes 배포를 생성합니다.

   ```
   apiVersion: 앱/v1
   종류: 배포
   메타데이터:
     이름: myapp-deployment
   투기:
     복제본: 3
     선택자:
       일치 라벨:
         앱: 마이앱
     주형:
       메타데이터:
         라벨:
           앱: 마이앱
       투기:
         컨테이너:
         - 이름: myapp 컨테이너
           이미지: myapp-이미지
           포트:
           - 컨테이너 포트: 8080
   ```

2. 애플리케이션을 위한 Kubernetes 서비스를 생성합니다.

   ```
   api 버전: v1
   종류: 서비스
   메타데이터:
     이름: myapp 서비스
   투기:
     유형: 로드밸런서
     포트:
     - 포트: 80
       대상 포트: 8080
     선택자:
       앱: 마이앱
   ```

3. Kubernetes 클러스터에 배포 및 서비스를 적용합니다.

   ```
   kubectl 적용 -f myapp-deployment.yaml
   kubectl 적용 -f myapp-service.yaml
   ```

4. 배포 및 서비스가 실행 중인지 확인합니다.

   ```
   kubectl 배포 가져오기
   kubectl 서비스 받기
   ```

이제 애플리케이션이 Kubernetes에 배포되었습니다!

## 추가 정보

- [쿠버네티스 문서](https://kubernetes.io/docs/)
- [스프링 부트 문서](https://spring.io/projects/spring-boot)