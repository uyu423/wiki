---
title: 097: OpenShift로 스프링 부트 애플리케이션 배포
description: 
published: true
date: 2023-02-04T18:17:23.834Z
tags: 
editor: markdown
dateCreated: 2023-02-04T18:17:18.454Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [097: Deploying a Spring Boot Application with OpenShift***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/097-deploying-a-spring-boot-application-with-openshift)
{.links-list}


## 소개

OpenShift는 Red Hat의 PaaS(Platform as a Service) 제품입니다. 개발자가 클라우드 환경에서 애플리케이션을 신속하게 개발, 호스팅 및 확장할 수 있는 온프레미스 애플리케이션 플랫폼입니다.

OpenShift는 Kubernetes를 기반으로 하며 개발자가 애플리케이션 배포, 관리 및 확장을 지원하는 도구 세트를 제공합니다.

이 게시물에서는 OpenShift에서 Spring Boot 애플리케이션을 배포하는 방법을 알아봅니다. 또한 OpenShift 도구를 사용하여 애플리케이션을 관리하고 확장하는 방법도 배웁니다.

## 전제 조건

시작하기 전에 준비해야 할 몇 가지 사항이 있습니다.

- OpenShift 계정. 없는 경우 [여기](https://www.openshift.com/pricing/index.html)에서 무료 평가판에 등록할 수 있습니다.
- 스프링 부트 애플리케이션. 없는 경우 [Spring Initializr](https://start.spring.io/)를 사용하여 간단하게 만들 수 있습니다.
- OpenShift용 [oc](https://docs.openshift.com/container-platform/3.11/cli_reference/get_started_cli.html# installing-the-oc-command-line-interface) 명령줄 인터페이스.

## 애플리케이션 배포

OpenShift 웹 콘솔을 사용하거나 oc 명령줄 인터페이스를 사용하는 두 가지 방법으로 OpenShift에 Spring Boot 애플리케이션을 배포할 수 있습니다.

### OpenShift 웹 콘솔을 사용하여 배포

1. OpenShift 웹 콘솔에 로그인하고 "프로젝트 생성" 버튼을 클릭합니다.

2. 프로젝트 이름을 입력하고 "만들기" 버튼을 클릭합니다.

3. "프로젝트에 추가" 페이지에서 "이미지 배포" 옵션을 선택하고 "이미지 선택" 버튼을 클릭합니다.

4. "이미지 이름" 필드에 Spring Boot 애플리케이션 이미지의 이름을 입력합니다. 이미지가 OpenShift 레지스트리에 없으면 이미지의 전체 URL을 입력할 수 있습니다.

5. "이미지 구성" 섹션에서 애플리케이션 이름, 애플리케이션이 실행될 포트 및 애플리케이션의 jar 파일 경로를 지정합니다.

6. "배포" 버튼을 클릭합니다.

7. "개요" 페이지에서 실행 중인 애플리케이션을 볼 수 있습니다. 애플리케이션 이름을 클릭하면 애플리케이션 페이지로 이동합니다.

8. 신청 페이지에 신청 URL이 표시됩니다. 새 탭에서 응용 프로그램을 열려면 URL을 클릭하십시오.

### oc 명령줄 인터페이스를 사용하여 배포

1. oc login 명령을 사용하여 OpenShift 클러스터에 로그인합니다.

2. oc new-project 명령을 사용하여 새 프로젝트를 만듭니다.

3. oc new-app 명령을 사용하여 애플리케이션을 배포합니다. 애플리케이션의 이름, 애플리케이션이 실행될 포트 및 애플리케이션의 jar 파일 경로를 지정합니다.

4. "개요" 페이지에서 실행 중인 애플리케이션을 볼 수 있습니다. 애플리케이션 이름을 클릭하면 애플리케이션 페이지로 이동합니다.

5. 애플리케이션 페이지에 애플리케이션의 URL이 표시됩니다. 새 탭에서 응용 프로그램을 열려면 URL을 클릭하십시오.

## 애플리케이션 관리

애플리케이션이 배포되면 OpenShift 웹 콘솔 또는 oc 명령줄 인터페이스를 사용하여 관리하고 확장할 수 있습니다.

### OpenShift 웹 콘솔을 사용하여 관리

1. OpenShift 웹 콘솔에서 "애플리케이션" 메뉴를 클릭하고 "배포" 옵션을 선택합니다.

2. "배포" 페이지에 프로젝트의 모든 배포 목록이 표시됩니다. 배포 이름을 클릭하여 배포 페이지로 이동합니다.

3. 배포 페이지에서 복제본 수, 배포 전략 및 롤아웃 기록과 같은 배포 세부 정보를 볼 수 있습니다.

4. 배포를 확장하려면 "확장" 버튼을 클릭하고 원하는 복제본 수를 입력합니다.

5. 새 롤아웃을 트리거하려면 "롤아웃" 버튼을 클릭합니다.

6. 배포를 삭제하려면 "삭제" 버튼을 클릭합니다.

### oc 명령줄 인터페이스를 사용하여 관리

1. oc login 명령을 사용하여 OpenShift 클러스터에 로그인합니다.

2. 프로젝트의 모든 배포를 나열하려면 oc get deployments 명령을 사용합니다.

3. 배포 세부 정보를 얻으려면 oc describe deployment 명령을 사용합니다.

4. 배포를 확장하려면 oc scale deployment 명령을 사용합니다.

5. 새 롤아웃을 트리거하려면 oc rollout latest 명령을 사용합니다.

6. 배포를 삭제하려면 oc delete deployment 명령을 사용합니다.

## 결론

이 게시물에서는 OpenShift에서 Spring Boot 애플리케이션을 배포하는 방법을 배웠습니다. 또한 OpenShift 도구를 사용하여 애플리케이션을 관리하고 확장하는 방법도 배웠습니다.