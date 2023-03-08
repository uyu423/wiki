---
title: 백엔드 개발을 위한 ORM 및 Auto-Scaling
description: 
published: true
date: 2023-02-17T18:04:16.653Z
tags: 
editor: markdown
dateCreated: 2023-01-30T12:17:11.405Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [ORM and Auto-scaling for Backend Development***English** version of this document is available*](/en/Knowledge-base/Backend/orm-and-auto-scaling-for-backend-development)
{.links-list}
 


# 백엔드 개발을 위한 ORM 및 Auto-Scaling

이 기사에서는 백엔드 개발을 위한 두 가지 중요한 개념인 ORM(Object Relational Mapping)과 자동 크기 조정에 대해 살펴보겠습니다.

## ORM

ORM은 개발자가 객체를 사용하여 데이터베이스 작업을 할 수 있게 해주는 기술입니다. 즉, 개체와 데이터베이스 테이블 간의 매핑을 제공합니다. 이 매핑은 두 가지 방법으로 수행할 수 있습니다.

- **주석 기반 매핑**: 이 접근 방식에서 개발자는 클래스와 데이터베이스 테이블 간의 매핑을 지정하는 메타데이터로 Java 클래스에 주석을 추가합니다.

- **XML 기반 매핑**: 이 접근 방식에서는 개발자가 XML 문서에 매핑을 지정합니다. 이 문서는 ORM 도구에서 데이터베이스 스키마와 Java 클래스를 생성하는 데 사용됩니다.

ORM을 사용하면 다음과 같은 몇 가지 이점이 있습니다.

- **개발이 더 빠르고 쉬워집니다**: 개발자는 애플리케이션의 비즈니스 논리에 집중하고 ORM 도구가 데이터베이스 상호 작용을 처리하도록 할 수 있습니다.

- **작성해야 하는 코드의 양을 줄입니다**: ORM 도구는 데이터베이스 상호 작용을 위한 SQL 코드를 생성할 수 있으므로 개발자가 직접 이 코드를 작성할 필요가 없습니다.

- **응용 프로그램의 이식성을 높입니다**: 데이터베이스 상호 작용이 ORM 도구에 의해 처리되기 때문에 필요한 경우 응용 프로그램을 다른 데이터베이스로 쉽게 마이그레이션할 수 있습니다.

Hibernate, EclipseLink 및 iBatis와 같은 여러 ORM 도구를 사용할 수 있습니다. 이 기사에서는 Hibernate에 초점을 맞출 것입니다.

### 최대 절전 모드

Hibernate는 주석 기반 및 XML 기반 매핑을 모두 제공하는 널리 사용되는 ORM 도구입니다. 또한 캐싱 및 지연 로딩 지원과 같은 여러 가지 다른 기능도 있습니다.

 Hibernate를 사용하여 Java 클래스를 데이터베이스 테이블에 매핑하는 방법을 살펴보겠습니다. 다음 Java 클래스를 예로 사용합니다.

```java
public class Employee {
    private Long id;
    private String name;
    private Integer age;
    private Double salary;
    
    // Getters and setters...
}
```

그리고 이를 다음 데이터베이스 테이블에 매핑합니다.

```sql
CREATE TABLE employee (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    age INTEGER,
    salary REAL
);
```

매핑은 두 가지 방법으로 수행할 수 있습니다.

- **주석 기반 매핑**:

  ```java
  @Entity
  @Table(name="employee")
  public class Employee {
      @Id
      @Column(name="id")
      private Long id;
  
      @Column(name="name")
      private String name;
  
      @Column(name="age")
      private Integer age;
  
      @Column(name="salary")
      private Double salary;
  
      // Getters and setters...
  }
  ```

- **XML 기반 매핑**:

  ```xml
  <hibernate-mapping>
      <class name="Employee" table="employee">
          <id name="id" column="id">
              <generator class="native"/>
          </id>
          <property name="name" column="name"/>
          <property name="age" column="age"/>
          <property name="salary" column="salary"/>
      </class>
  </hibernate-mapping>
  ```

두 경우 모두 Employee 클래스가 매핑될 데이터베이스 테이블의 이름을 지정해야 합니다. 또한 Employee 클래스의 각 필드에 대한 매핑을 지정해야 합니다. id 필드의 경우 테이블의 기본 키이고 데이터베이스에서 생성됨(자동 증가)을 지정해야 합니다.

매핑이 완료되면 직원을 삽입, 업데이트, 삭제 및 쿼리하는 코드를 작성할 수 있습니다.

```java
// Insert an employee
Employee emp = new Employee();
emp.setName("John Smith");
emp.setAge(30);
emp.setSalary(45000.0);

Session session = sessionFactory.openSession();
session.beginTransaction();

session.save(emp);

session.getTransaction().commit();
session.close();

// Update an employee
emp.setSalary(50000.0);

session = sessionFactory.openSession();
session.beginTransaction();

session.update(emp);

session.getTransaction().commit();
session.close();

// Delete an employee
session = sessionFactory.openSession();
session.beginTransaction();

session.delete(emp);

session.getTransaction().commit();
session.close();

// Query employees
List<Employee> employees = session.createQuery("from Employee").list();

for (Employee e : employees) {
    System.out.println(e.getName() + " " + e.getAge() + " " + e.getSalary());
}
```

위의 코드 스니펫에서 먼저 직원을 데이터베이스에 삽입합니다. 그런 다음 직원의 급여를 업데이트하고 마지막으로 직원을 삭제합니다. 또한 데이터베이스를 쿼리하여 모든 직원 목록을 얻습니다.

## 자동 크기 조정

자동 확장은 개발자가 애플리케이션을 수평으로 확장할 수 있도록 하는 기술입니다. 즉, 개발자는 응용 프로그램에 대한 로드가 증가할 때 응용 프로그램에 새 서버를 추가할 수 있습니다. 이는 단일 서버의 리소스를 늘리는 수직 확장과 대조됩니다.

자동 크기 조정을 사용하면 두 가지 이점이 있습니다.

- **응용 프로그램이 더 많은 부하를 처리할 수 있습니다**: 필요에 따라 새 서버를 추가할 수 있으므로 응용 프로그램은 성능 문제 없이 더 많은 트래픽을 처리할 수 있습니다.

- **더 비용 효율적입니다**: 필요에 따라 새 서버를 추가하고 제거할 수 있으므로 개발자는 사용한 리소스에 대해서만 비용을 지불합니다.

자동 크기 조정은 수동 또는 자동으로 수행할 수 있습니다. 이 문서에서는 자동 자동 크기 조정에 중점을 둘 것입니다.

### 자동 자동 크기 조정

자동 자동 크기 조정에는 도구를 사용하여 애플리케이션의 로드를 모니터링하고 필요에 따라 서버를 추가 및 제거하는 작업이 포함됩니다. Apache httpd, nginx 및 HAProxy와 같은 여러 도구를 사용할 수 있습니다. 이 기사에서는 Apache httpd에 중점을 둘 것입니다.

Apache httpd는 자동 크기 조정 애플리케이션을 만드는 데 사용할 수 있는 널리 사용되는 웹 서버입니다. 필요에 따라 서버를 추가하고 제거하는 데 사용할 수 있는 mod_cluster라는 모듈이 있습니다.

mod_cluster 모듈은 다음과 같이 작동합니다.

- **애플리케이션의 부하를 모니터링합니다**: 모듈이 주기적으로 애플리케이션에 요청을 보내 응답 시간을 확인합니다. 응답 시간이 너무 길면 애플리케이션에 과부하가 걸리고 새 서버를 추가해야 함을 의미합니다.

- **필요에 따라 서버를 추가하고 제거합니다**: 모듈은 mod_cluster 관리 인터페이스에 요청하여 응용 프로그램에 새 서버를 추가할 수 있습니다. 마찬가지로 더 이상 필요하지 않은 서버를 제거할 수 있습니다.

mod_cluster 모듈을 사용하여 자동 확장 애플리케이션을 만드는 방법을 살펴보겠습니다. 다음 Apache httpd 구성을 사용합니다.

```apache
<VirtualHost *:80>
    ServerName www.example.com
    
    <Directory /var/www/html>
        Require all granted
    </Directory>
    
    <Location /cluster-manager>
        SetHandler cluster-manager
    </Location>
    
    <Proxy balancer://mycluster>
        BalancerMember http://localhost:8000
        BalancerMember http://localhost:8001
    </Proxy>
    
    <Proxy *>
        Order deny,allow
        Allow from all
    </Proxy>
    
    ProxyPass / balancer://mycluster/
    ProxyPassReverse / balancer://mycluster/
</VirtualHost>
```

위의 구성에서 www.example.com 도메인에 대한 요청을 처리할 가상 호스트를 정의했습니다. 또한 두 개의 서버(localhost:8000 및 localhost:8001)를 포함하는 프록시 밸런서를 정의했습니다. 마지막으로 필요에 따라 서버를 추가하고 제거하도록 mod_cluster를 구성했습니다.

이제 Apache httpd 서버에서 제공할 간단한 PHP 애플리케이션을 작성해 보겠습니다.

```php
<?php
$server = $_SERVER['SERVER_ADDR'];
echo "Hello, World! I'm running on $server";
?>
```

그리고 우리는 그것을 두 개의 서버에서 실행할 것입니다:

- 로컬호스트:8000
- 로컬호스트:8001

사용자가 www.example.com 웹사이트를 방문하면 다음 페이지가 표시됩니다.

```
Hello, World! I'm running on 127.0.0.1
```

더 많은 요청을 만들어 애플리케이션의 로드를 늘리면 mod_cluster는 필요에 따라 새 서버를 추가합니다. 예를 들어 초당 10개의 요청을 만들면 mod_cluster는 두 개의 새 서버를 추가합니다.

## 결론

이 기사에서는 백엔드 개발을 위한 두 가지 중요한 개념인 ORM과 자동 크기 조정에 대해 살펴보았습니다. 우리는 ORM을 사용하여 Java 클래스를 데이터베이스 테이블에 매핑하는 방법과 자동 확장을 사용하여 필요에 따라 애플리케이션에 새 서버를 추가하는 방법을 살펴보았습니다.