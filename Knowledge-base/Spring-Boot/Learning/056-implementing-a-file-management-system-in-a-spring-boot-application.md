---
title: 056: Spring Boot 애플리케이션에서 파일 관리 시스템 구현
description: 
published: true
date: 2023-02-03T20:17:31.198Z
tags: 
editor: markdown
dateCreated: 2023-02-03T20:17:29.559Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [056: Implementing a file management system in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/056-implementing-a-file-management-system-in-a-spring-boot-application)
{.links-list}


# Spring Boot 애플리케이션에서 파일 관리 시스템 구현

Spring Boot는 독립 실행형 프로덕션 등급 Spring 애플리케이션을 만들 수 있는 Java 기반 프레임워크입니다. 이 게시물에서는 Spring Boot 애플리케이션에서 파일 관리 시스템을 구현하는 방법을 보여줍니다.

## 전제 조건

- Java 개발 경험이 있으신 분
- Spring Framework 사용 경험이 있으신 분

## 시작하기

먼저 새로운 Spring Boot 프로젝트를 생성해야 합니다. [Spring Initializr](https://start.spring.io/)를 사용하여 이를 수행할 수 있습니다.

![스프링 이니셜라이저](https://i.imgur.com/hmvkF9r.png)

프로젝트 세부 정보를 입력합니다.

- 그룹: com.example
- 아티팩트: 파일 관리 시스템
- 명칭 : 파일관리시스템
- 설명 : Spring Boot로 구현된 파일 관리 시스템
- 패키지 이름: com.example.filemanagementsystem
- 유형: 메이븐 프로젝트
- 포장: 항아리
- 자바 버전: 8
- 다음 종속성을 선택합니다.
  - 웹
  - 백리향
  - 롬복

"프로젝트 생성"을 클릭하여 프로젝트를 다운로드합니다.

## 프로젝트 구조

프로젝트가 생성되면 다음과 같은 프로젝트 구조가 있어야 합니다.

```
.
├── pom.xml
└── src
    └── main
        ├── java
        │   └── com
        │       └── example
        │           └── filemanagementsystem
        │               ├── FileManagementSystemApplication.java
        │               ├── controller
        │               │   └── FileController.java
        │               └── model
        │                   └── File.java
        └── resources
            ├── application.properties
            └── templates
                └── index.html
```

## 파일 관리 시스템 구현

이제 기본 프로젝트가 설정되었으므로 파일 관리 시스템 구현을 시작할 수 있습니다.

### 모델 만들기

파일 관리 시스템은 관리 중인 파일에 대한 정보를 저장해야 합니다. `File` 모델을 생성하여 이를 수행할 수 있습니다.

```java
@Data
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class File {

    private String name;
    private String type;
    private long size;
}
```

[Lombok](https://projectlombok.org/) 라이브러리의 `@Data` 주석은 게터, 세터 및 toString 메서드를 생성합니다. `@Builder` 주석을 사용하면 빌더 패턴을 사용하여 `File` 개체를 만들 수 있습니다. `@NoArgsConstructor` 및 `@AllArgsConstructor` 주석은 각각 no-args 생성자와 모든 필드를 인수로 사용하는 생성자를 생성합니다.

### 컨트롤러 만들기

다음으로 파일 관리 시스템에 대한 요청을 처리할 컨트롤러를 만들어야 합니다. `FileController`를 생성하여 이를 수행할 수 있습니다.

```java
@Slf4j
@Controller
@RequestMapping("/files")
public class FileController {

    @GetMapping
    public String listFiles(Model model) {
        // TODO: Implement this method
        return "index";
    }

    @PostMapping
    public String uploadFile(@RequestParam("file") MultipartFile file) {
        // TODO: Implement this method
        return "redirect:/files";
    }

    @GetMapping("/{id}")
    public ResponseEntity<Resource> downloadFile(@PathVariable String id) {
        // TODO: Implement this method
        return null;
    }
}
```

Lombok 라이브러리의 `@Slf4j` 주석은 로거를 생성합니다. `@Controller` 주석은 이 클래스를 컨트롤러로 표시합니다. `@RequestMapping` 주석은 컨트롤러의 모든 메서드를 `/files` 경로에 매핑합니다.

`listFiles` 메소드는 `/files` 경로에 대한 GET 요청을 처리합니다. 매개변수로 `Model` 개체를 사용하고 렌더링해야 하는 템플릿을 나타내는 문자열을 반환합니다.

`uploadFile` 메소드는 `/files` 경로에 대한 POST 요청을 처리합니다. 이는 `MultipartFile` 개체를 매개변수로 사용하고 렌더링해야 하는 템플릿을 나타내는 문자열을 반환합니다.

`downloadFile` 메서드는 `/files/{id}` 경로에 대한 GET 요청을 처리합니다. 문자열 ID를 매개변수로 사용하고 요청된 파일을 포함하는 `ResponseEntity` 개체를 반환합니다.

### 템플릿 만들기

파일 관리 시스템에 대해 두 개의 템플릿을 생성해야 합니다. 하나는 파일 나열용이고 다른 하나는 파일 업로드용입니다. `src/main/resources/templates` 디렉토리에 `index.html` 파일을 생성하여 이를 수행할 수 있습니다.

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>File Management System</title>
</head>
<body>
    <h1>File Management System</h1>

    <table>
        <thead>
            <tr>
                <th>Name</th>
                <th>Type</th>
                <th>Size</th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            <tr th:each="file : ${files}">
                <td th:text="${file.name}"></td>
                <td th:text="${file.type}"></td>
                <td th:text="${file.size}"></td>
                <td><a href="/files/[[${file.id}]]">Download</a></td>
            </tr>
        </tbody>
    </table>

    <form method="post" enctype="multipart/form-data">
        <div>
            <label>File:</label>
            <input type="file" name="file"/>
        </div>
        <div>
            <button type="submit">Upload</button>
        </div>
    </form>
</body>
</html>
```

이 템플릿은 업로드된 모든 파일을 나열하고 새 파일을 업로드하기 위한 양식을 제공합니다.

### 스프링 부트 설정

`application.properties` 파일에서 몇 가지를 구성해야 합니다.

```properties
spring.thymeleaf.mode=HTML5
spring.thymeleaf.encoding=UTF-8
spring.thymeleaf.content-type=text/html
server.port=8080
```

`spring.thymeleaf.mode`, `spring.thymeleaf.encoding` 및 `spring.thymeleaf.content-type` 속성은 각각 HTML5, UTF-8 인코딩 및 텍스트/html 콘텐츠 유형을 사용하도록 Thymeleaf를 구성합니다. `server.port` 속성은 서버가 포트 8080에서 실행되도록 구성합니다.

## 애플리케이션 실행

이제 애플리케이션을 실행하고 테스트할 수 있습니다.

먼저 프로젝트를 빌드해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
$ ./mvnw clean package
```

다음으로 다음 명령을 사용하여 애플리케이션을 실행할 수 있습니다.

```
$ java -jar target/file-management-system-0.0.1-SNAPSHOT.jar
```

이제 http://localhost:8080에서 파일 관리 시스템에 액세스할 수 있습니다.

## 결론

이 게시물에서는 Spring Boot 애플리케이션에서 파일 관리 시스템을 구현하는 방법을 보여주었습니다.