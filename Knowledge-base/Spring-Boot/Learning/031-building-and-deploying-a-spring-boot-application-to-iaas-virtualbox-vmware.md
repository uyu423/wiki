---
title: 031: IaaS(Virtualbox, VMware)에 Spring Boot 애플리케이션 구축 및 배포
description: 
published: true
date: 2023-02-03T23:32:11.879Z
tags: 
editor: markdown
dateCreated: 2023-02-03T23:32:10.298Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [031: Building and deploying a Spring Boot application to IaaS (Virtualbox, VMware)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/031-building-and-deploying-a-spring-boot-application-to-iaas-virtualbox-vmware)
{.links-list}


# 031: IaaS(Virtualbox, VMware)에 Spring Boot 애플리케이션 빌드 및 배포

이번 포스팅에서는 IaaS(Virtualbox, VMware)에 Spring Boot 애플리케이션을 빌드하고 배포하는 방법에 대해 알아보겠습니다.

Spring Initializr를 사용하여 새로운 Spring Boot 프로젝트를 생성하는 것으로 시작하겠습니다. 프로젝트의 경우 웹 및 Thymeleaf 종속성을 선택해야 합니다.

프로젝트가 생성되면 Thymeleaf 템플릿을 렌더링할 간단한 컨트롤러를 추가합니다.

@Controller public class HomeController { @RequestMapping("/") public String home(Model model) { model.addAttribute("message", "Hello, World!"); 귀국"; } }

템플릿은 컨트롤러에서 전달한 메시지만 표시합니다.

<html> <head> <title>안녕하세요!</title> </head> <body> <p th:text="${message}"></p> </body> </html>

이제 애플리케이션이 완성되었으므로 JAR 파일로 패키징해야 합니다. 프로젝트의 루트 디렉터리에서 다음 명령을 실행하여 이를 수행할 수 있습니다.

./mvnw 패키지

이렇게 하면 target/ 디렉토리에 JAR 파일이 생성됩니다.

이제 이 JAR 파일을 IaaS 공급자에게 배포할 수 있습니다. 새 VM을 만들고 JRE(Java Runtime Environment)를 설치해야 합니다.

VM이 실행되면 JAR 파일을 VM으로 SCP로 전송하고 다음 명령을 사용하여 실행할 수 있습니다.

자바 -jar spring-boot-app.jar

이제 http://{vm-ip-address}:8080에서 애플리케이션에 액세스할 수 있습니다.

그게 전부입니다! 이번 포스트에서는 Spring Boot 애플리케이션을 IaaS(Virtualbox, VMware)에 빌드하고 배포하는 방법을 배웠습니다.