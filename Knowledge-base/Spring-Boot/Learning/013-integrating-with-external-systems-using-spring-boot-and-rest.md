---
title: 013: Spring Boot 및 REST를 사용하여 외부 시스템과 통합
description: 
published: true
date: 2023-02-01T21:36:36.734Z
tags: 
editor: markdown
dateCreated: 2023-02-01T21:36:31.844Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [013: Integrating with external systems using Spring Boot and REST***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/013-integrating-with-external-systems-using-spring-boot-and-rest)
{.links-list}


# 소개

이 게시물에서는 REST를 사용하여 Spring Boot를 외부 시스템과 통합하는 방법을 살펴보겠습니다. 이 작업을 수행하는 방법을 설명하기 위해 간단한 예를 사용합니다.

# 레스트란?

REST는 Representational State Transfer의 약자입니다. 웹 서비스를 생성하는 데 사용할 일련의 제약 조건을 정의하는 소프트웨어 아키텍처 스타일입니다. REST 아키텍처 스타일을 준수하는 웹 서비스를 RESTful 웹 서비스라고 합니다.

# REST를 사용하는 이유

RESTful 웹 서비스는 구축하기 쉽고 확장 가능한 분산 시스템을 지원하는 데 매우 적합합니다. RESTful 웹 서비스는 모든 플랫폼에서 구축할 수 있으며 HTTP 프로토콜을 지원하는 모든 클라이언트에서 사용할 수 있습니다.

# RESTful 웹 서비스를 만드는 방법은 무엇입니까?

RESTful 웹 서비스를 만드는 방법에는 두 가지가 있습니다.

1. JAX-RS 및 Jersey 사용
2. 스프링 부트 사용

이 게시물에서는 Spring Boot를 사용하여 RESTful 웹 서비스를 만드는 방법에 중점을 둘 것입니다.

# 스프링부트란?

Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있는 프레임워크입니다. Spring 기반 애플리케이션을 구성하고 구축하기 위한 독창적인 접근 방식을 제공합니다.

# 스프링 부트를 사용하는 이유

Spring Boot를 사용하면 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다. Spring 기반 애플리케이션을 빌드, 테스트 및 배포하는 데 사용할 수 있는 다양한 기능을 제공합니다.

# Spring Boot를 사용하여 RESTful 웹 서비스를 만드는 방법은 무엇입니까?

다음 도구와 기술을 사용하여 Spring Boot 기반 RESTful 웹 서비스를 만들 것입니다.

1. 자바 8
2. 메이븐 3.3.9
3. 스프링 부트 1.5.4.RELEASE
4. 이클립스 네온.3

# 프로젝트 생성

Spring Initializr를 사용하여 Spring Boot 프로젝트를 생성합니다. 다음 설정을 사용합니다.

1. 그룹: com.example
2. 아티팩트: spring-boot-rest
3. 이름: 스프링 부트 REST
4. 설명: Spring Boot REST 예제
5. 패키지 이름: com.example.springbootrest
6. 포장: 항아리
7. 자바 버전: 1.8
8. 다음 종속성을 선택합니다. Web, JPA, H2

# 프로젝트 구성

우리는 H2를 데이터베이스로 사용할 것입니다. application.properties 파일에서 H2를 구성합니다.

spring.h2.console.enabled=true
spring.h2.console.path=/h2

# 엔터티 만들기

Employee라는 간단한 엔터티를 만듭니다.

@실재
공개 클래스 직원 {

    @ID
    @GeneratedValue
    개인 긴 ID;

    개인 문자열 이름;

    개인 문자열 역할;

    // 게터와 세터
}

# 저장소 생성

직원 엔터티에 대한 간단한 JpaRepository 인터페이스를 만듭니다.

공용 인터페이스 EmployeeRepository 확장 JpaRepository<Employee, Long> {

}

# 서비스 만들기

우리는 간단한 EmployeeService 인터페이스를 생성할 것입니다:

공용 인터페이스 EmployeeService {

    직원 저장(Employee Employee);

    List<Employee> findAll();

    직원 findOne(Long id);

    무효 삭제(긴 ID);
}

# 서비스 구현 만들기

간단한 EmployeeServiceImpl 클래스를 생성합니다.

@서비스
공개 클래스 EmployeeServiceImpl은 EmployeeService를 구현합니다.

    @Autowired
    개인 EmployeeRepository employeeRepository;

    @우세하다
    public Employee save(Employee 직원) {
        return employeeRepository.save(직원);
    }

    @우세하다
    공개 목록<직원> findAll() {
        return employeeRepository.findAll();
    }

    @우세하다
    공개 직원 findOne(Long id) {
        return employeeRepository.findOne(id);
    }

    @우세하다
    공공 무효 삭제(긴 ID) {
        employeeRepository.delete(id);
    }
}

# REST 컨트롤러 생성

우리는 간단한 EmployeeController 클래스를 만들 것입니다:

@RestController
@RequestMapping("/직원")
공개 클래스 EmployeeController {

    @Autowired
    private EmployeeService 직원 서비스;

    @RequestMapping(메서드 = RequestMethod.GET)
    공개 목록<직원> findAll() {
        return employeeService.findAll();
    }

    @RequestMapping(방법 = RequestMethod.POST)
    public Employee save(@RequestBody 직원 직원) {
        return employeeService.save(직원);
    }

    @RequestMapping(방법 = RequestMethod.GET, 값 = "/{id}")
    공개 직원 findOne(@PathVariable Long id) {
        return employeeService.findOne(id);
    }

    @RequestMapping(방법 = RequestMethod.DELETE, 값 = "/{id}")
    공개 무효 삭제(@PathVariable 긴 ID) {
        EmployeeService.delete(id);
    }
}

# REST 컨트롤러 테스트

다음 curl 명령을 사용하여 EmployeeController를 테스트합니다.

직원을 저장하려면:

curl -X POST -H "콘텐츠 유형: 애플리케이션/json" -d '{"이름":"John Smith","role":"Developer"}' http://localhost:8080/employees

모든 직원을 찾으려면:

컬 -X GET http://localhost:8080/employees

ID가 1인 직원을 찾으려면:

컬 -X GET http://localhost:8080/employees/1

ID가 1인 직원을 삭제하려면:

컬 -X DELETE http://localhost:8080/employees/1

# 결론

이번 포스팅에서는 Spring Boot를 이용하여 RESTful 웹 서비스를 생성하는 방법에 대해 알아보았습니다. 프로젝트 생성, 프로젝트 구성, 엔터티 생성, 리포지토리 생성, 서비스 생성, 서비스 구현 생성, REST 컨트롤러 생성 및 REST 컨트롤러 테스트 방법을 살펴보았습니다.