---
title: Spring Boot의 CQRS(Command Query Responsibility Segregation) 패턴
description: 
published: true
date: 2023-02-01T15:03:44.438Z
tags: 
editor: markdown
dateCreated: 2023-02-01T15:03:42.627Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [The Command Query Responsibility Segregation (CQRS) Pattern in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-command-query-responsibility-segregation-cqrs-pattern-in-spring-boot)
{.links-list}


# Spring Boot의 CQRS(Command Query Responsibility Segregation) 패턴

명령 쿼리 책임 분리(CQRS)는 명령 처리 책임(시스템 상태를 변경하는 요청)과 쿼리 처리 책임(시스템에서 정보를 반환하는 요청)을 분리하는 아키텍처 패턴입니다.

이러한 관심사의 분리는 향상된 성능, 확장성 및 유지 관리성과 같은 여러 가지 이점을 제공할 수 있습니다.

CQRS 아키텍처에서 명령은 일반적으로 쿼리를 처리하는 서비스와 별도의 서비스에서 처리됩니다. 이러한 분리는 다양한 방법으로 구현할 수 있지만 일반적인 접근 방식은 명령으로 액세스하는 데이터와 쿼리로 액세스하는 데이터를 저장하기 위해 서로 다른 데이터베이스 테이블을 사용하는 것입니다.

Spring Boot는 웹 애플리케이션 구축에 널리 사용되는 Java 프레임워크입니다. "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 만드는 편리한 방법을 제공합니다.

이 기사에서는 Spring Boot 애플리케이션에서 CQRS 아키텍처를 구현하는 방법을 살펴보겠습니다. 이러한 응용 프로그램과 관련된 다양한 구성 요소를 살펴보는 것으로 시작하겠습니다. 그런 다음 CQRS를 사용하는 간단한 예제 애플리케이션을 구현합니다.

## CQRS 애플리케이션의 구성 요소

CQRS 애플리케이션에는 일반적으로 다음 구성 요소가 있습니다.

- **명령:** 시스템 상태를 변경하는 요청입니다. 예제 응용 프로그램에는 작업을 만들고 업데이트하는 명령이 있습니다.
- **쿼리:** 시스템에서 정보를 반환하는 요청입니다. 예제 응용 프로그램에는 모든 작업 목록을 가져오고 특정 작업의 세부 정보를 가져오는 쿼리가 있습니다.
- **명령 서비스:** 명령을 처리하는 서비스입니다. 예제 응용 프로그램에서 이 서비스는 명령 유효성 검사 및 실행을 담당합니다.
- **쿼리 서비스:** 쿼리를 처리하는 서비스입니다. 예제 응용 프로그램에서 이 서비스는 쿼리를 실행하고 호출자에게 결과를 반환하는 역할을 합니다.
- **저장소:** 데이터 저장소에 액세스하기 위한 인터페이스를 제공하는 데이터 액세스 계층입니다. 예제 애플리케이션에서는 작업 데이터에 액세스하기 위해 리포지토리를 사용합니다.
- **모델:** 애플리케이션의 도메인 모델입니다. 예제 애플리케이션에서 작업은 유일한 모델 개체입니다.


## Spring Boot로 CQRS 애플리케이션 구현

이제 CQRS 애플리케이션의 다양한 구성 요소를 살펴보았으므로 CQRS를 사용하는 간단한 예제 애플리케이션을 구현해 보겠습니다.

우리의 예제 애플리케이션은 작업 관리자가 될 것입니다. 사용자는 작업을 생성하고 자신이나 다른 사용자에게 할당할 수 있습니다. 또한 작업을 완료로 표시할 수 있습니다.

명령 서비스를 구현하는 것으로 시작하겠습니다. 이 서비스는 명령의 유효성 검사 및 실행을 담당합니다.

### 명령 서비스

명령 서비스에는 다음과 같은 방법이 있습니다.

- **createTask(Task task)**: 이 메서드는 작업을 생성하는 데 사용됩니다.
- **updateTask(Task task)**: 이 메서드는 작업을 업데이트하는 데 사용됩니다.
- **markTaskAsComplete(String taskId)**: 이 메서드는 작업을 완료로 표시하는 데 사용됩니다.

**TaskCommandService**라는 클래스에서 이러한 메서드를 구현합니다. 이 클래스는 클래스를 서비스 구성 요소로 표시하는 Spring 주석인 **@Service**로 주석이 지정됩니다.

```java
@Service
public class TaskCommandService {

    public void createTask(Task task) {
        // validate the task
        // save the task
    }

    public void updateTask(Task task) {
        // validate the task
        // save the task
    }

    public void markTaskAsComplete(String taskId) {
        // validate the task
        // mark the task as complete
        // save the task
    }
}
```

보시다시피 **createTask** 및 **updateTask** 메서드는 **Task** 객체를 매개변수로 받아들입니다. 이 개체는 생성 또는 업데이트 중인 작업에 대한 데이터를 보유하는 데 사용됩니다.

**markTaskAsComplete** 메소드는 태스크 ID를 매개변수로 허용합니다. 이 작업 ID는 완료된 것으로 표시될 작업을 조회하는 데 사용됩니다.

이러한 각 메서드는 **validate** 메서드에 대한 호출로 시작합니다. 이 유효성 검사 메서드는 전달된 데이터의 유효성 검사를 담당합니다. 다음 섹션에서 이 메서드를 구현할 것입니다.

### 명령 유효성 검사

**validate** 메서드는 명령 서비스 메서드에 전달되는 데이터의 유효성을 검사합니다. **TaskCommandValidator**라는 클래스에서 이 메서드를 구현합니다. 이 클래스는 클래스를 구성 요소로 표시하는 Spring 주석인 **@Component**로 주석이 지정됩니다.

```java
@Component
public class TaskCommandValidator {

    public void validate(Task task) {
        // validate the task
    }

    public void validate(String taskId) {
        // validate the task ID
    }
}
```

보시다시피 이 클래스에는 두 가지 유효성 검사 메서드가 있습니다. 이러한 메서드 중 하나는 **Task** 개체를 매개 변수로 허용합니다. 이 방법은 작업 생성 및 업데이트를 위한 데이터의 유효성을 검사하는 데 사용됩니다.

다른 유효성 검사 메서드는 작업 ID를 매개 변수로 허용합니다. 이 메서드는 작업을 완료로 표시하기 위한 작업 ID의 유효성을 검사하는 데 사용됩니다.

실제 응용 프로그램에서 이러한 유효성 검사 메서드에는 데이터 유효성 검사를 위한 논리가 포함됩니다. 이 예의 목적을 위해 비워 두겠습니다.

### 쿼리 서비스

쿼리 서비스에는 다음 메서드가 있습니다.

- **getAllTasks()**: 이 메서드는 모든 작업 목록을 가져오는 데 사용됩니다.
- **getTaskById(String taskId)**: 이 메서드는 특정 작업의 세부 정보를 가져오는 데 사용됩니다.

**TaskQueryService**라는 클래스에서 이러한 메서드를 구현합니다. 이 클래스는 **@Service**로 주석 처리됩니다.

```java
@Service
public class TaskQueryService {

    public List<Task> getAllTasks() {
        // execute query
        // return results
    }

    public Task getTaskById(String taskId) {
        // execute query
        // return results
    }
}
```

보시다시피 **getAllTasks** 메서드는 **Task** 개체 목록을 반환합니다. 이 목록에는 시스템의 모든 작업에 대한 데이터가 포함됩니다.

**getTaskById** 메서드는 단일 **Task** 개체를 반환합니다. 이 개체에는 지정된 ID를 가진 작업에 대한 데이터가 포함됩니다.

### 저장소

리포지토리는 데이터 저장소에 액세스하기 위한 인터페이스를 제공하는 데이터 액세스 계층입니다. 예제 애플리케이션에서는 작업 데이터에 액세스하기 위해 리포지토리를 사용합니다.

**TaskRepository**라는 클래스에 저장소를 구현할 것입니다. 이 클래스는 클래스를 리포지토리 구성 요소로 표시하는 Spring 주석인 **@Repository**로 주석이 지정됩니다.

```java
@Repository
public class TaskRepository {

    public void save(Task task) {
        // save the task
    }

    public Task findById(String id) {
        // find the task
        // return the task
    }

    public List<Task> findAll() {
        // find all tasks
        // return the tasks
    }
}
```

보시다시피 이 리포지토리에는 작업을 저장, 찾기 및 삭제하는 메서드가 있습니다.

### 모델

모델은 애플리케이션의 도메인 모델입니다. 예제 애플리케이션에서 작업은 유일한 모델 개체입니다.

**Task**라는 클래스에서 작업 모델을 구현합니다. 이 클래스는 클래스를 엔티티로 표시하는 JPA 주석인 **@Entity**로 주석 처리됩니다.

```java
@Entity
public class Task {

    @Id
    private String id;

    private String name;

    private String description;

    private boolean complete;

    // getters and setters
}
```

보시다시피 이 작업 모델에는 ID, 이름, 설명 및 완료의 네 가지 필드가 있습니다. id 필드는 필드를 엔티티의 기본 키로 표시하는 JPA 주석인 **@Id**로 주석 처리됩니다.

### 함께 모아서

이제 CQRS 애플리케이션의 다양한 구성 요소를 구현했으므로 모두 함께 배치하고 작동 방식을 살펴보겠습니다.

작업을 생성하여 시작하겠습니다. 이를 위해 먼저 **Task** 개체를 만들고 작업에 대한 데이터로 채웁니다. 그런 다음 이 개체를 **TaskCommandService**의 **createTask** 메서드에 전달합니다.

```java
Task task = new Task();
task.setName("Write example");
task.setDescription("Write an example of the CQRS pattern");

taskCommandService.createTask(task);
```

그러면 시스템에 새 작업이 생성됩니다.

이제 모든 작업 목록을 얻고 싶다고 가정해 보겠습니다. 이를 위해 **TaskQueryService**의 **getAllTasks** 메서드를 호출합니다.

```java
List<Task> tasks = taskQueryService.getAllTasks();
```

그러면 시스템의 모든 작업 목록이 반환됩니다.

마지막으로 작업을 완료로 표시하고 싶다고 가정해 보겠습니다. 이를 위해 먼저 ID로 작업을 가져옵니다. 그런 다음 **TaskCommandService**의 **markTaskAsComplete** 메서드를 호출합니다.

```java
Task task = taskQueryService.getTaskById("1");

taskCommandService.markTaskAsComplete(task.getId());
```

이렇게 하면 ID가 "1"인 작업이 완료된 것으로 표시됩니다.

## 결론

이 기사에서는 CQRS(Command Query Responsibility Segregation) 패턴과 이를 Spring Boot 애플리케이션에서 구현하는 방법을 살펴보았습니다.

또한 이 패턴이 향상된 성능, 확장성 및 유지 관리성과 같은 몇 가지 이점을 제공하는 방법도 확인했습니다.

CQRS에 대해 자세히 알아보려면 다음 리소스를 추천합니다.

- [CQRS: 좋은 놈, 나쁜 놈, 그리고 추한 놈](https://martinfowler.com/bliki/CQRS.html)
- [명령 쿼리 책임 분리](https://en.wikipedia.org/wiki/Command%E2%80%93query_separation)
- [CQRS를 사용하는 이유는?](https://docs.microsoft.com/en-us/azure/architecture/patterns/cqrs)