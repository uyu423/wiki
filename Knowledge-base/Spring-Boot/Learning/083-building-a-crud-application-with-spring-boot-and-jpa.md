---
title: 083: Spring Boot와 JPA로 CRUD 애플리케이션 구축
description: 
published: true
date: 2023-02-05T13:32:25.192Z
tags: 
editor: markdown
dateCreated: 2023-02-05T13:32:22.878Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [083: Building a CRUD Application with Spring Boot and JPA***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/083-building-a-crud-application-with-spring-boot-and-jpa)
{.links-list}


083: Spring Boot와 JPA로 CRUD 애플리케이션 구축
==================================================== ======

이 기사에서는 Spring Boot 및 JPA를 사용하여 CRUD 애플리케이션을 빌드하는 방법을 배웁니다.

먼저 리소스 표현 클래스를 만듭니다. 이 클래스는 응용 프로그램에서 데이터를 나타내는 데 사용됩니다.

다음으로 리포지토리 인터페이스를 만듭니다. 이 인터페이스는 데이터에 액세스하는 데 사용됩니다.

마지막으로 컨트롤러를 생성합니다. 이 컨트롤러는 HTTP 요청 및 응답을 처리하는 데 사용됩니다.

리소스 표현 클래스 만들기
------------------------------------------

첫 번째 단계는 리소스 표현 클래스를 만드는 것입니다. 이 클래스는 응용 프로그램에서 데이터를 나타내는 데 사용됩니다.

먼저 `User`라는 클래스를 생성합니다. 이 클래스에는 `id`, `name` 및 `email`의 세 가지 필드가 있습니다.


    공개 클래스 사용자 {
    
        개인 긴 ID;
        개인 문자열 이름;
        개인 문자열 이메일;
    
        // 게터와 세터
    
    }


리포지토리 인터페이스 만들기
----------------------------------

다음으로 리포지토리 인터페이스를 만듭니다. 이 인터페이스는 데이터에 액세스하는 데 사용됩니다.

`UserRepository`라는 인터페이스를 만드는 것으로 시작하겠습니다. 이 인터페이스는 `JpaRepository`를 확장합니다. `JpaRepository`는 CRUD 작업을 제공하는 Spring Data JPA 인터페이스입니다.


    공개 인터페이스 UserRepository 확장 JpaRepository<User, Long> {
    
    }


컨트롤러 만들기
-----------------------

마지막으로 컨트롤러를 생성합니다. 이 컨트롤러는 HTTP 요청 및 응답을 처리하는 데 사용됩니다.

`UserController`라는 클래스를 만드는 것으로 시작하겠습니다. 이 클래스에는 `getAllUsers` 및 `createUser`의 두 가지 메서드가 있습니다.

`getAllUsers` 메서드는 `/users`에 대한 GET 요청을 처리하는 데 사용됩니다. 이 메서드는 데이터베이스의 모든 사용자 목록을 반환합니다.

`createUser` 메서드는 `/users`에 대한 POST 요청을 처리하는 데 사용됩니다. 이 방법은 데이터베이스에 새 사용자를 생성합니다.


    @RestController
    공개 클래스 UserController {
    
        @Autowired
        개인 UserRepository userRepository;
    
        @GetMapping("/사용자")
        공개 목록<사용자> getAllUsers() {
            return userRepository.findAll();
        }
    
        @PostMapping("/사용자")
        공개 사용자 createUser(@RequestBody 사용자 사용자) {
            return userRepository.save(사용자);
        }
    
    }


애플리케이션 테스트
-----------------------

리소스 표현 클래스, 리포지토리 인터페이스 및 컨트롤러를 만들었으므로 이제 애플리케이션을 테스트할 준비가 되었습니다.

`User` 개체를 만드는 것으로 시작하겠습니다.


    사용자 사용자 = 새 사용자();
    user.setName("홍길동");
    user.setEmail("john.doe@example.com");


다음으로 `createUser` 메서드를 호출합니다.


    사용자 = userController.createUser(사용자);


마지막으로 `getAllUsers` 메서드를 호출합니다.


    List<User> 사용자 = userController.getAllUsers();
    assertThat(사용자).contains(사용자);


모든 것이 잘 되었다면 다음 출력이 표시되어야 합니다.


    [
        {
            "ID": 1,
            "이름": "홍길동",
            "이메일": "john.doe@example.com"
        }
    ]


GitHub에서 이 예제의 전체 소스 코드를 찾을 수 있습니다.