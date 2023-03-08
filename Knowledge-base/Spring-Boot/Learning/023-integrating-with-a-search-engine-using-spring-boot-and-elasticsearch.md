---
title: 023: Spring Boot 및 Elasticsearch를 사용하여 검색 엔진과 통합
description: 
published: true
date: 2023-02-03T15:32:38.228Z
tags: 
editor: markdown
dateCreated: 2023-02-03T15:32:36.505Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [023: Integrating with a search engine using Spring Boot and Elasticsearch***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/023-integrating-with-a-search-engine-using-spring-boot-and-elasticsearch)
{.links-list}


# Spring Boot와 Elasticsearch를 이용한 검색엔진 연동

이 게시물에서는 Elasticsearch를 사용하여 Spring Boot 애플리케이션을 검색 엔진과 통합하는 방법을 알아봅니다.

## 엘라스틱서치란?

Elasticsearch는 Apache Lucene에 구축된 분산형 RESTful 검색 및 분석 엔진입니다. 대규모 데이터 세트에 대한 전체 텍스트 검색 및 분석을 구현하기 위한 강력한 기능 세트를 제공합니다.

## Elasticsearch를 사용하는 이유는 무엇인가요?

Elasticsearch는 사용 용이성, 확장성 및 성능으로 인해 검색 엔진을 구현하는 데 널리 사용되는 선택입니다.

## 엘라스틱서치 설정

Elasticsearch를 사용하기 전에 먼저 설정해야 합니다.

Elasticsearch를 설정하는 방법에는 두 가지가 있습니다.

1. [공식 웹사이트](https://www.elastic.co/downloads/elasticsearch)에서 Elasticsearch를 다운로드하여 설치합니다.
2. [Docker 이미지](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html)를 사용합니다.

이 게시물에서는 Docker 이미지를 사용합니다.

## 엘라스틱서치 실행

Elasticsearch Docker 이미지를 실행하려면 다음 명령을 사용하십시오.

```
$ docker run -d -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.4.0
```

이렇게 하면 포트 9200에서 Elasticsearch 7.4.0을 실행하는 컨테이너가 시작됩니다.

## 엘라스틱서치에 연결하기

이제 Elasticsearch가 실행 중이므로 Spring Boot 애플리케이션에서 이를 사용할 수 있습니다.

Spring Boot에서 Elasticsearch에 연결하려면 `pom.xml`에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-elasticsearch</artifactId>
</dependency>
```

이 종속성은 애플리케이션에서 Elasticsearch에 연결하고 이를 사용하는 데 필요한 라이브러리를 추가합니다.

## Elasticsearch 구성

프로젝트에 `spring-boot-starter-data-elasticsearch` 종속성이 있으면 Elasticsearch를 구성해야 합니다.

`application.properties` 파일에 다음 속성을 추가하여 Elasticsearch를 구성할 수 있습니다.

```properties
spring.data.elasticsearch.cluster-nodes=localhost:9300
spring.data.elasticsearch.cluster-name=docker-cluster
```

이렇게 하면 'localhost:9300'에서 실행 중인 Elasticsearch 클러스터에 연결하도록 애플리케이션이 구성됩니다.

## 스프링 부트 애플리케이션 만들기

이제 Elasticsearch를 설정하고 구성했으므로 이를 사용하는 Spring Boot 애플리케이션을 만들 수 있습니다.

`User` 클래스를 생성하는 것으로 시작하겠습니다:

```java
@Document(indexName = "user", type = "user")
public class User {

    @Id
    private String id;

    private String name;

    private Integer age;

    // getters and setters
}
```

이 클래스는 애플리케이션의 사용자를 나타냅니다. `@Document`로 주석을 달았습니다. 이는 Spring Data Elasticsearch에 이것이 Elasticsearch에서 인덱싱되어야 하는 문서임을 알려줍니다.

또한 `id` 필드에 `@Id`로 주석을 달았습니다. 이는 이 문서의 고유 식별자임을 Spring Data Elasticsearch에 알려줍니다.

다음으로 `UserRepository` 인터페이스를 만듭니다.

```java
public interface UserRepository extends ElasticsearchRepository<User, String> {

}
```

이 인터페이스는 Elasticsearch와 상호 작용하기 위한 강력한 메서드 세트를 제공하는 'ElasticsearchRepository'를 확장합니다.

마지막으로 `UserService` 클래스를 만듭니다.

```java
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public void saveUser(User user) {
        userRepository.save(user);
    }

    public void deleteUser(User user) {
        userRepository.delete(user);
    }

    public Iterable<User> getAllUsers() {
        return userRepository.findAll();
    }

    public User getUserById(String id) {
        return userRepository.findById(id).orElse(null);
    }
}
```

이 클래스는 애플리케이션에서 사용자를 생성, 검색 및 삭제하는 방법을 제공합니다. `@Service`로 주석을 달았습니다. 이것은 이것이 Spring 컨테이너에 의해 관리되어야 하는 서비스 bean임을 Spring에게 알려줍니다.

또한 `userRepository` 필드에 `@Autowired`로 주석을 달았습니다. 이것은 bean이 생성될 때 이 필드에 `UserRepository`의 인스턴스를 주입하도록 Spring에 지시합니다.

## 문서 생성 및 인덱싱

이제 Spring Boot 애플리케이션이 설정되었으므로 Elasticsearch에서 문서 생성 및 인덱싱을 시작할 수 있습니다.

`User` 인스턴스를 생성하는 것으로 시작하겠습니다:

```java
User user = new User();
user.setId("1");
user.setName("John Doe");
user.setAge(20);
```

다음으로 이 사용자를 데이터베이스에 저장합니다.

```java
userService.saveUser(user);
```

이렇게 하면 사용자가 데이터베이스에 저장되고 Elasticsearch에서 문서를 인덱싱합니다.

## 문서 검색

Elasticsearch에서 문서를 인덱싱하면 문서 검색을 시작할 수 있습니다.

Elasticsearch는 문서 검색을 위한 강력한 쿼리 DSL(도메인별 언어)을 제공합니다.

`UserRepository`에서 `search()` 메서드를 사용하여 검색 쿼리를 실행할 수 있습니다.

```java
SearchQuery searchQuery = new NativeSearchQueryBuilder()
        .withQuery(QueryBuilders.queryStringQuery("John Doe"))
        .build();

List<User> users = userRepository.search(searchQuery).getContent();
```

이 쿼리는 "John Doe" 구가 포함된 모든 문서를 검색합니다.

`search()` 메서드는 검색 쿼리 결과가 포함된 `SearchResponse` 개체를 반환합니다. `getContent()` 메서드를 사용하여 검색 쿼리와 일치하는 `User` 개체 목록을 가져올 수 있습니다.

## 문서 업데이트

Elasticsearch를 사용하여 문서를 업데이트할 수도 있습니다.

문서를 업데이트하려면 먼저 데이터베이스에서 검색해야 합니다.

```java
User user = userService.getUserById("1");
```

다음으로 문서를 업데이트합니다.

```java
user.setAge(21);
```

마지막으로 업데이트된 문서를 데이터베이스에 저장합니다.

```java
userService.saveUser(user);
```

이렇게 하면 데이터베이스와 Elasticsearch에서 문서가 업데이트됩니다.

## 문서 삭제

Elasticsearch를 사용하여 문서를 삭제할 수도 있습니다.

문서를 삭제하려면 먼저 데이터베이스에서 검색해야 합니다.

```java
User user = userService.getUserById("1");
```

다음으로 문서를 삭제합니다.

```java
userService.deleteUser(user);
```

이렇게 하면 데이터베이스와 Elasticsearch에서 문서가 삭제됩니다.

## 결론

이번 포스트에서는 Elasticsearch를 사용하여 Spring Boot 애플리케이션을 검색 엔진과 통합하는 방법을 배웠습니다. Elasticsearch에서 문서를 생성, 인덱싱, 업데이트 및 삭제하는 방법도 배웠습니다.