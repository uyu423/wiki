---
title: Spring WebFlux를 사용한 리액티브 프로그래밍
description: 
published: true
date: 2023-01-31T19:04:52.651Z
tags: 
editor: markdown
dateCreated: 2023-01-31T19:04:48.921Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Reactive Programming with Spring WebFlux***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/reactive-programming-with-spring-webflux)
{.links-list}



# Spring WebFlux를 사용한 리액티브 프로그래밍

리액티브 프로그래밍은 데이터 스트림 및 변경 전파와 관련된 선언적 프로그래밍 패러다임입니다. 즉, 정적(예: 배열) 또는 동적(예: 이벤트 이미터) 데이터 스트림을 쉽게 표현할 수 있고 애플리케이션이 데이터 스트림의 변경 사항에 반응할 수 있음을 의미합니다.

더 반응적이고 탄력적인 애플리케이션에 대한 수요가 증가함에 따라 반응형 프로그래밍의 필요성이 대두되었습니다. 과거에는 애플리케이션이 단일 코드베이스에 모든 기능이 포함된 모놀리식으로 구축되는 경우가 많았습니다. 이로 인해 코드베이스의 한 부분이 변경되면 다른 부분에서 예기치 않은 결과가 발생할 수 있으므로 응답성을 달성하기가 어렵습니다.

리액티브 프로그래밍은 애플리케이션의 서로 다른 부분을 분리하고 독립적으로 구축할 수 있는 보다 모듈화된 접근 방식을 허용합니다. 이렇게 하면 코드베이스의 한 부분을 변경해도 다른 부분에 영향을 줄 가능성이 적어 반응형 애플리케이션을 더 쉽게 만들 수 있습니다.

Spring WebFlux는 Reactor 프로젝트 위에 구축된 반응형 웹 프레임워크입니다. 응답성과 탄력성이 더 뛰어나고 다른 반응성 라이브러리와 쉽게 통합할 수 있는 웹 애플리케이션을 구축할 수 있습니다.

이 기사에서는 Spring WebFlux를 사용하여 반응형 웹 애플리케이션을 빌드하는 방법을 살펴봅니다. 또한 반응적 접근 방식을 사용할 때 얻을 수 있는 몇 가지 이점에 대해서도 살펴보겠습니다.

## 리액티브 프로그래밍이란?

리액티브 프로그래밍은 데이터 스트림 및 변경 전파와 관련된 선언적 프로그래밍 패러다임입니다. 즉, 정적(예: 배열) 또는 동적(예: 이벤트 이미터) 데이터 스트림을 쉽게 표현할 수 있고 애플리케이션이 데이터 스트림의 변경 사항에 반응할 수 있음을 의미합니다.

더 반응적이고 탄력적인 애플리케이션에 대한 수요가 증가함에 따라 반응형 프로그래밍의 필요성이 대두되었습니다. 과거에는 애플리케이션이 단일 코드베이스에 모든 기능이 포함된 모놀리식으로 구축되는 경우가 많았습니다. 이로 인해 코드베이스의 한 부분이 변경되면 다른 부분에서 예기치 않은 결과가 발생할 수 있으므로 응답성을 달성하기가 어렵습니다.

리액티브 프로그래밍은 애플리케이션의 서로 다른 부분을 분리하고 독립적으로 구축할 수 있는 보다 모듈화된 접근 방식을 허용합니다. 이렇게 하면 코드베이스의 한 부분을 변경해도 다른 부분에 영향을 줄 가능성이 적어 반응형 애플리케이션을 더 쉽게 만들 수 있습니다.

리액티브 프로그래밍은 이벤트 및 이벤트 핸들러 개념을 중심으로 애플리케이션을 설계하는 방식인 옵저버 패턴을 기반으로 합니다. 옵저버 패턴에서 객체(주제라고 함)는 옵저버 목록을 유지하고 흥미로운 일이 발생하면 이를 알립니다. 그런 다음 관찰자는 적절한 조치를 취할 수 있습니다.

![리액티브 프로그래밍](https://i.imgur.com/EwP52Uv.png)

리액티브 프로그래밍에서 데이터 스트림은 주제이고 관찰자는 데이터의 소비자입니다. 소비자는 적합하다고 판단되는 방식으로 데이터에 반응하도록 선택할 수 있습니다.

리액티브 프로그래밍은 함수형 프로그래밍에 뿌리를 두고 있으며 많은 동일한 원칙을 공유합니다. 특히, 리액티브 프로그래밍은 프로그래머가 어떻게 일어나야 하는지가 아니라 일어나기를 원하는 것을 선언하는 선언적 프로그래밍의 아이디어를 기반으로 합니다.

## 스프링 웹플럭스란?

Spring WebFlux는 Reactor 프로젝트 위에 구축된 반응형 웹 프레임워크입니다. 응답성과 탄력성이 더 뛰어나고 다른 반응성 라이브러리와 쉽게 통합할 수 있는 웹 애플리케이션을 구축할 수 있습니다.

Spring WebFlux는 전통적인 Spring MVC 모델의 대안입니다. 전통적인 모델에서 웹 요청은 단일 스레드에 의해 처리되고 스레드가 완료되면 응답이 반환됩니다. 응답을 기다리는 동안 스레드가 차단되므로 성능 문제가 발생할 수 있습니다.

반응형 모델에서 웹 요청은 비차단 스레드에 의해 처리되고 응답은 즉시 반환됩니다. 이렇게 하면 응답을 기다리는 동안 스레드가 차단되지 않으므로 성능이 향상됩니다.

![스프링 웹플럭스](https://i.imgur.com/5B6qDfu.png)

Spring WebFlux는 생산자가 소비자가 처리할 수 있는 것보다 더 많은 데이터를 생성하지 않도록 데이터 흐름을 관리하는 방법인 백프레셔(backpressure)도 지원합니다. 이것은 소비자가 압도되는 것을 방지하기 때문에 소비자가 생산자를 따라갈 수 없는 상황에서 중요합니다.

백프레셔는 리액티브 프로그래밍을 위한 표준 세트인 리액티브 스트림 사양에 의해 관리됩니다. Spring WebFlux는 Reactive Streams 사양을 구현하고 즉시 배압 지원을 제공합니다.

## 시작하기

이 섹션에서는 Spring WebFlux를 시작하는 방법을 살펴보겠습니다. 사용자 목록을 표시하는 간단한 웹 응용 프로그램을 만듭니다.

### 전제 조건

시작하기 전에 다음 도구가 설치되어 있는지 확인해야 합니다.

* 자바 8 이상
* 메이븐 3.5 이상

### 프로젝트 만들기

Spring Initializr 도구를 사용하여 프로젝트를 생성할 수 있습니다. 이 도구를 사용하면 프로젝트에 필요한 종속성을 선택하고 프로젝트 구조를 생성할 수 있습니다.

다음 종속성을 선택해야 합니다.

* 웹 - 이 종속성은 WebFlux 프레임워크를 포함하며 웹 애플리케이션을 구축하는 데 필요합니다.
* Lombok - 이 종속성은 상용구 코드를 줄이는 데 사용되며 선택 사항입니다.

종속성이 선택되면 프로젝트 구조를 생성할 수 있습니다.

### 종속성 추가

다음으로, 이전 단계에서 선택한 종속성을 `pom.xml` 파일에 추가해야 합니다.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-webflux</artifactId>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>
```

### 사용자 모델 만들기

사용자 데이터를 나타내는 모델을 만들어야 합니다. `src/main/java/com/example` 디렉토리에 `User.java` 파일을 생성하여 이를 수행할 수 있습니다.

```java
@Data
public class User {
    private String id;
    private String name;
    private String email;
}
```

Lombok 라이브러리의 `@Data` 주석을 사용하여 상용구 코드를 줄였습니다. 이 주석은 게터, 세터 및 toString 메서드를 생성합니다.

### 사용자 서비스 만들기

다음으로 사용자 데이터를 가져오는 서비스를 만들어야 합니다. `src/main/java/com/example` 디렉토리에 `UserService.java` 파일을 생성하여 이를 수행할 수 있습니다.

```java
@Service
public class UserService {
    private List<User> users = new ArrayList<>();

    public UserService() {
        this.users.add(new User("1", "John Doe", "john.doe@example.com"));
        this.users.add(new User("2", "Jane Doe", "jane.doe@example.com"));
    }

    public List<User> getUsers() {
        return this.users;
    }
}
```

이 서비스에서는 데이터를 가져오는 데 사용할 수 있는 사용자 목록을 만들었습니다.

### 사용자 컨트롤러 만들기

다음으로 웹 요청을 처리할 컨트롤러를 만들어야 합니다. `src/main/java/com/example` 디렉토리에 `UserController.java` 파일을 생성하여 이를 수행할 수 있습니다.

```java
@RestController
@RequestMapping("/users")
public class UserController {
    private UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping
    public Flux<User> getUsers() {
        return this.userService.getUsers()
                .stream()
                .map(user -> User.builder()
                        .id(user.getId())
                        .name(user.getName())
                        .email(user.getEmail())
                        .build())
                .collect(Collectors.toList())
                .flux();
    }
}
```

이 컨트롤러에서 `/users` 경로를 `getUsers()` 메서드에 매핑했습니다. 이 메서드는 서비스에서 사용자 목록을 가져와서 `Flux`로 반환합니다.

'플럭스'는 비동기적으로 내보낼 수 있는 데이터 스트림입니다. RxJava의 Observable과 유사합니다.

### 애플리케이션 실행

이제 다음 명령을 실행하여 애플리케이션을 실행할 수 있습니다.

```
./mvnw spring-boot:run
```

그러면 `http://localhost:8080/users`에서 애플리케이션에 액세스할 수 있습니다.

## 결론

이 기사에서는 Spring WebFlux를 사용하여 반응형 웹 애플리케이션을 빌드하는 방법을 살펴보았습니다. 우리는 또한 반응적 접근 방식을 사용할 때 얻을 수 있는 몇 가지 이점에 대해서도 살펴보았습니다.

리액티브 프로그래밍에 대해 자세히 알아보려면 다음 리소스를 참조하세요.

* [리액티브 프로그래밍](https://en.wikipedia.org/wiki/Reactive_programming)
* [리액티브 스트림](http://www.reactive-streams.org/)
* [리액터](https://projectreactor.io/)
* [스프링 웹플럭스](https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html)