---
title: JPA 및 Hibernate로 빠른 시작
description: 
published: true
date: 2023-02-17T18:01:23.667Z
tags: 
editor: markdown
dateCreated: 2023-01-30T01:14:08.294Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Quick Started with JPA and Hibernate***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/quick-started-with-jpa-and-hibernate)
{.links-list}


JPA와 Hibernate는 Java 업계에서 가장 인기 있는 지속성 기술 중 두 가지입니다. JPA는 관계형 데이터베이스의 데이터에 액세스하고 데이터를 관리하기 위한 API를 정의하는 사양입니다. 최대 절전 모드는 사양에 추가 기능을 추가하는 JPA 사양의 구현입니다.

이 빠른 시작에서는 JPA 및 Hibernate를 사용하여 관계형 데이터베이스에서 데이터를 유지하는 방법을 보여줍니다. MySQL 데이터베이스에 데이터를 저장하는 간단한 Java 애플리케이션을 작성합니다. 응용 프로그램에는 사용자라는 단일 엔터티가 있습니다. 각 사용자는 이름, 성 및 이메일 주소를 갖게 됩니다.

먼저 IDE에서 새 프로젝트를 만들어야 합니다. Eclipse를 사용하고 있지만 모든 IDE가 가능합니다. 새 프로젝트를 만들고 프로젝트에 다음 종속성을 추가합니다.

- HWQL
- JPA
- JTA

이러한 종속성은 Maven Central에서 찾을 수 있습니다.

다음으로 User 엔터티를 만듭니다. JPA의 엔터티는 @Entity 주석으로 주석이 달린 POJO입니다. 각 엔터티에는 @Id 주석이 달린 기본 키가 있어야 합니다. User 엔터티는 다음과 같습니다.

```java
@Entity
public class User {

    @Id
    private Long id;

    private String firstName;
    private String lastName;
    private String email;

    // Getters and setters...
}
```

이제 엔터티가 있으므로 JPA 리포지토리를 만들어야 합니다. JPA 저장소는 JpaRepository 인터페이스를 확장하는 인터페이스입니다. 엔터티를 검색하고 유지하기 위한 메서드를 제공합니다. UserRepository는 다음과 같습니다.

```java
public interface UserRepository extends JpaRepository<User, Long> {

}
```

이제 리포지토리가 있으므로 이를 사용하여 데이터를 유지하는 서비스를 작성할 수 있습니다. 우리 서비스에는 새로운 사용자를 생성하는 방법과 모든 사용자를 검색하는 방법이 있습니다. 다음과 같이 표시됩니다.

```java
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public User createUser(User user) {
        return userRepository.save(user);
    }

    public List<User> getUsers() {
        return userRepository.findAll();
    }
}
```

마지막으로 서비스 메서드를 REST 끝점으로 노출하는 REST 컨트롤러를 작성합니다. 컨트롤러는 다음과 같습니다.

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @Autowired
    private UserService userService;

    @PostMapping
    public User createUser(@RequestBody User user) {
        return userService.createUser(user);
    }

    @GetMapping
    public List<User> getUsers() {
        return userService.getUsers();
    }
}
```

그게 다야! 이제 관계형 데이터베이스에서 데이터를 유지하기 위해 JPA와 Hibernate를 사용하는 간단한 Java 애플리케이션을 작성했습니다.