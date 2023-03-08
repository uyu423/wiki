---
title: Spring Boot 개발의 퍼사드 패턴
description: 
published: true
date: 2023-02-06T07:17:46.721Z
tags: 
editor: markdown
dateCreated: 2023-02-06T07:17:45.132Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [The Facade Pattern in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-facade-pattern-in-spring-boot-development)
{.links-list}


# Spring Boot 개발의 Facade 패턴

Facade 패턴은 복잡한 시스템에 단순화된 인터페이스를 제공하는 소프트웨어 디자인 패턴입니다. 이 패턴은 종종 Singleton, Factory 및 Abstract Factory 패턴과 같은 다른 디자인 패턴과 함께 사용됩니다.

Facade 디자인 패턴은 Spring Boot 애플리케이션에서 특히 유용합니다. Spring Boot는 자동 구성, 스타터 종속성 및 플러그형 Java 구성과 같이 개발을 더욱 복잡하게 만들 수 있는 다양한 기능을 제공합니다. Facade 디자인 패턴은 복잡한 Spring Boot 시스템에 더 간단한 인터페이스를 제공하여 Spring Boot로 개발을 보다 관리하기 쉽게 만드는 데 도움이 될 수 있습니다.

Facade 디자인 패턴은 복잡한 시스템에 단일 인터페이스를 제공하는 데 사용됩니다. 이 패턴은 종종 Singleton, Factory 및 Abstract Factory 패턴과 같은 다른 디자인 패턴과 함께 사용됩니다. Facade 디자인 패턴은 Spring Boot 애플리케이션에서 특히 유용합니다. Spring Boot는 자동 구성, 스타터 종속성 및 플러그형 Java 구성과 같이 개발을 더욱 복잡하게 만들 수 있는 다양한 기능을 제공합니다. Facade 디자인 패턴은 복잡한 Spring Boot 시스템에 더 간단한 인터페이스를 제공하여 Spring Boot로 개발을 보다 관리하기 쉽게 만드는 데 도움이 될 수 있습니다.

다음은 Spring Boot 애플리케이션에서 Facade 디자인 패턴을 사용하는 방법의 예입니다. 이 예제에서는 Spring Boot Starter Jdbc 및 Spring Boot Starter 웹 종속성을 사용합니다. 이러한 종속성은 pom.xml 파일에 다음 줄을 추가하여 Spring Boot 애플리케이션에 추가할 수 있습니다.

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>

<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

이 예제에서는 MySQL Connector/J JDBC 드라이버도 사용합니다. 이 드라이버는 pom.xml 파일에 다음 행을 추가하여 Spring Boot 애플리케이션에 추가할 수 있습니다.

```xml
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
</dependency>
```

Facade 디자인 패턴의 예제 코드는 아래와 같습니다. 이 코드는 Facade를 사용하여 MySQL 데이터베이스에 액세스하는 간단한 Spring Boot 애플리케이션을 보여줍니다. Facade는 @Component 주석이 달린 Java 클래스로 구현됩니다. Facade 클래스에는 @Autowired 주석이 달린 메서드가 있습니다. 이 메서드는 DataSource를 Facade에 주입하는 데 사용됩니다. Facade 클래스에는 @PostConstruct 주석이 달린 메서드도 있습니다. 이 메서드는 Facade를 초기화하는 데 사용됩니다. initialize() 메서드는 JdbcTemplate을 생성하고 템플릿의 DataSource를 설정합니다. Facade 클래스에는 데이터베이스를 쿼리하고 결과를 반환하는 데 사용되는 getData() 메서드가 있습니다. getData() 메서드는 JdbcTemplate을 사용하여 데이터베이스를 쿼리하고 결과를 반환합니다.

```java
@Component
public class Facade {

  private DataSource dataSource;
  private JdbcTemplate jdbcTemplate;

  @Autowired
  public void setDataSource(DataSource dataSource) {
    this.dataSource = dataSource;
  }

  @PostConstruct
  public void initialize() {
    this.jdbcTemplate = new JdbcTemplate(this.dataSource);
  }

  public List<Map<String, Object>> getData() {
    String sql = "SELECT * FROM data";
    return this.jdbcTemplate.queryForList(sql);
  }
}
```

다음은 Facade를 사용하는 Spring Boot 애플리케이션의 코드입니다. 응용 프로그램의 코드는 다음과 같습니다. 이 코드는 @SpringBootApplication 주석이 달린 SpringBootApplication 클래스를 생성합니다. @SpringBootApplication 주석은 자동 구성 및 구성 요소 검색을 활성화하는 데 사용됩니다. 이 코드는 DataSource bean도 생성합니다. DataSource bean은 DataSource를 Facade에 삽입하는 데 사용됩니다. 이 코드는 또한 Facade 빈을 생성합니다. Facade 빈은 Facade를 Spring Boot 애플리케이션에 주입하는 데 사용됩니다. 이 코드에는 Spring Boot 애플리케이션을 시작하는 데 사용되는 main() 메서드도 있습니다.

```java
@SpringBootApplication
public class Application {

  @Bean
  public DataSource dataSource() {
    // TODO: Configure DataSource
    return null;
  }

  @Bean
  public Facade facade() {
    return new Facade();
  }

  public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
  }
}
```

다음은 Facade를 사용하는 Spring Boot 애플리케이션의 코드입니다. 응용 프로그램의 코드는 다음과 같습니다. 이 코드는 @SpringBootApplication 주석이 달린 SpringBootApplication 클래스를 생성합니다. @SpringBootApplication 주석은 자동 구성 및 구성 요소 검색을 활성화하는 데 사용됩니다. 이 코드는 DataSource bean도 생성합니다. DataSource bean은 DataSource를 Facade에 삽입하는 데 사용됩니다. 이 코드는 또한 Facade 빈을 생성합니다. Facade 빈은 Facade를 Spring Boot 애플리케이션에 주입하는 데 사용됩니다. 이 코드에는 Spring Boot 애플리케이션을 시작하는 데 사용되는 main() 메서드도 있습니다.

다음은 Facade를 사용하는 Spring Boot 애플리케이션의 코드입니다. 응용 프로그램의 코드는 다음과 같습니다. 이 코드는 @SpringBootApplication 주석이 달린 SpringBootApplication 클래스를 생성합니다. @SpringBootApplication 주석은 자동 구성 및 구성 요소 검색을 활성화하는 데 사용됩니다. 이 코드는 DataSource bean도 생성합니다. DataSource bean은 DataSource를 Facade에 삽입하는 데 사용됩니다. 이 코드는 또한 Facade 빈을 생성합니다. Facade 빈은 Facade를 Spring Boot 애플리케이션에 주입하는 데 사용됩니다. 이 코드에는 Spring Boot 애플리케이션을 시작하는 데 사용되는 main() 메서드도 있습니다.

다음은 Facade를 사용하는 Spring Boot 애플리케이션의 코드입니다. 응용 프로그램의 코드는 다음과 같습니다. 이 코드는 @SpringBootApplication 주석이 달린 SpringBootApplication 클래스를 생성합니다. @SpringBootApplication 주석은 자동 구성 및 구성 요소 검색을 활성화하는 데 사용됩니다. 이 코드는 DataSource bean도 생성합니다. DataSource bean은 DataSource를 Facade에 삽입하는 데 사용됩니다. 이 코드는 또한 Facade 빈을 생성합니다. Facade 빈은 Facade를 Spring Boot 애플리케이션에 주입하는 데 사용됩니다. 이 코드에는 Spring Boot 애플리케이션을 시작하는 데 사용되는 main() 메서드도 있습니다.

다음은 Facade를 사용하는 Spring Boot 애플리케이션의 코드입니다. 응용 프로그램의 코드는 다음과 같습니다. 이 코드는 @SpringBootApplication 주석이 달린 SpringBootApplication 클래스를 생성합니다. @SpringBootApplication 주석은 자동 구성 및 구성 요소 검색을 활성화하는 데 사용됩니다. 이 코드는 DataSource bean도 생성합니다. DataSource bean은 DataSource를 Facade에 삽입하는 데 사용됩니다. 이 코드는 또한 Facade 빈을 생성합니다. Facade 빈은 Facade를 Spring Boot 애플리케이션에 주입하는 데 사용됩니다. 이 코드에는 Spring Boot 애플리케이션을 시작하는 데 사용되는 main() 메서드도 있습니다.

다음은 Facade를 사용하는 Spring Boot 애플리케이션의 코드입니다. 응용 프로그램의 코드는 다음과 같습니다. 이 코드는 @SpringBootApplication 주석이 달린 SpringBootApplication 클래스를 생성합니다. @SpringBootApplication 주석은 자동 구성 및 구성 요소 검색을 활성화하는 데 사용됩니다. 이 코드는 DataSource bean도 생성합니다. DataSource bean은 DataSource를 Facade에 삽입하는 데 사용됩니다. 이 코드는 또한 Facade 빈을 생성합니다. Facade 빈은 Facade를 Spring Boot 애플리케이션에 주입하는 데 사용됩니다. 이 코드에는 Spring Boot 애플리케이션을 시작하는 데 사용되는 main() 메서드도 있습니다.


## 참조

1. 디자인 패턴: Erich Gamma, John Vlissides, Ralph Johnson 및 Richard Helm의 재사용 가능한 객체 지향 소프트웨어 요소(Addison-Wesley, 1995)

2. 스프링 부트 참조 문서: https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/

3. MySQL 커넥터/J JDBC 드라이버: https://dev.mysql.com/doc/connector-j/5.1/en/