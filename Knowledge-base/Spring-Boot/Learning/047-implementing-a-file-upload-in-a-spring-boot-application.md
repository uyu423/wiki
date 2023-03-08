---
title: 047: Spring Boot 애플리케이션에서 파일 업로드 구현
description: 
published: true
date: 2023-02-04T13:32:32.037Z
tags: 
editor: markdown
dateCreated: 2023-02-04T13:32:26.493Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [047: Implementing a file upload in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/047-implementing-a-file-upload-in-a-spring-boot-application)
{.links-list}


# Spring Boot 애플리케이션에서 파일 업로드 구현

이 게시물에서는 Spring Boot 애플리케이션에서 파일 업로드를 구현하는 방법을 살펴보겠습니다.

@ConfigurationProperties 주석을 살펴보고 Spring Boot에서 파일 업로드를 구성하는 데 어떻게 사용할 수 있는지 살펴보겠습니다. 그런 다음 사용자가 업로드할 파일을 선택할 수 있는 간단한 HTML 양식을 만듭니다. 마지막으로 파일 업로드를 처리하고 파일을 서버의 디렉터리에 저장하는 컨트롤러를 구현합니다.

## Spring Boot에서 파일 업로드 구성

Spring Boot는 Spring Boot 애플리케이션에서 파일 업로드를 구성하는 데 사용할 수 있는 여러 속성을 제공합니다. 이러한 속성에는 ```spring.servlet.multipart.``` 접두사가 붙습니다.

가장 중요한 속성은 ```spring.servlet.multipart.enabled```입니다. Spring Boot에서 파일 업로드를 활성화하려면 이 속성을 ```true```로 설정해야 합니다.

다음 속성은 ```spring.servlet.multipart.file-size-threshold```입니다. 이 속성은 메모리에 저장될 파일의 크기 임계값을 지정합니다. 이 임계값보다 큰 파일은 디스크의 임시 파일에 기록됩니다.

마지막으로 살펴볼 속성은 ```spring.servlet.multipart.location```입니다. 이 속성은 업로드된 파일이 저장될 서버의 위치를 지정합니다. 이 위치는 애플리케이션이 실행되는 사용자가 쓸 수 있는 디렉토리여야 합니다.

## 파일 업로드를 위한 HTML 양식 만들기

이제 파일 업로드를 위해 Spring Boot를 구성했으므로 사용자가 업로드할 파일을 선택할 수 있는 HTML 양식을 만들어야 합니다.

양식에는 ```file``` 입력 필드와 ```submit``` 버튼이 있어야 합니다. ```file``` 입력 필드에는 ```multiple``` 속성이 ```true```로 설정되어 있어야 합니다. 이렇게 하면 사용자가 업로드할 여러 파일을 선택할 수 있습니다.

```form``` 요소의 ```action``` 속성은 파일 업로드를 처리할 컨트롤러의 URL로 설정되어야 합니다. ```method``` 속성은 ```POST```로 설정되어야 합니다.

## 파일 업로드 컨트롤러 구현

이제 파일 업로드를 위한 양식이 있으므로 파일 업로드를 처리하는 컨트롤러를 구현해야 합니다.

컨트롤러에는 ```/upload``` 값이 있는 ```@PostMapping``` 주석이 있어야 합니다. 그러면 URL ```/upload```가 컨트롤러 메서드에 매핑됩니다.

컨트롤러 메서드에는 ```file``` 값이 있는 ```@RequestParam``` 주석이 있어야 합니다. 이것은 ```file``` 입력 필드를 ```MultipartFile``` 객체에 바인딩합니다.

컨트롤러 메서드에는 ```@ResponseBody``` 주석도 있어야 합니다. 이렇게 하면 컨트롤러 메서드가 업로드된 파일의 내용을 요청에 대한 응답으로 반환하게 됩니다.

마지막으로 컨트롤러 메서드에는 ```/upload``` 값이 있는 ```@RequestMapping``` 주석이 있어야 합니다. 그러면 URL ```/upload```가 컨트롤러 메서드에 매핑됩니다.

## 업로드된 파일 저장

파일이 업로드되면 이전에 구성한 디렉토리에 파일을 저장해야 합니다. ```MultipartFile``` 객체에서 ```transferTo()``` 메서드를 호출하여 이를 수행할 수 있습니다.

```transferTo()``` 메서드는 ```File``` 객체를 인수로 사용합니다. 구성된 위치를 업로드된 파일의 원래 파일 이름과 연결하여 ```File``` 객체를 생성할 수 있습니다.

파일이 전송되면 ```201``` 상태 코드와 함께 ```ResponseEntity``` 객체를 반환하여 파일이 성공적으로 업로드되었음을 나타낼 수 있습니다.

## 결론

이번 포스트에서는 Spring Boot 애플리케이션에서 파일 업로드를 구현하는 방법을 살펴보았습니다. 우리는 @ConfigurationProperties 주석과 Spring Boot에서 파일 업로드를 구성하는 데 어떻게 사용할 수 있는지 살펴보는 것으로 시작했습니다. 그런 다음 사용자가 업로드할 파일을 선택할 수 있는 간단한 HTML 양식을 만들었습니다. 마지막으로 파일 업로드를 처리하고 파일을 서버의 디렉터리에 저장하는 컨트롤러를 구현했습니다.