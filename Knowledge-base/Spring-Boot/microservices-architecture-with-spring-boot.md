---
title: Spring Boot를 사용한 마이크로서비스 아키텍처
description: 
published: true
date: 2023-02-17T18:01:32.114Z
tags: 
editor: markdown
dateCreated: 2023-01-30T02:54:59.143Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Microservices Architecture with Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/microservices-architecture-with-spring-boot)
{.links-list}


마이크로서비스는 한동안 클라우드 애플리케이션을 구축하기 위한 인기 있는 아키텍처 스타일이었습니다. Spring Boot는 "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 쉽게 만들 수 있는 프레임워크입니다. 이 게시물에서는 Spring Boot를 사용하여 마이크로 서비스 아키텍처를 구축하는 방법을 살펴보겠습니다.

모놀리식 애플리케이션의 간단한 예부터 시작하겠습니다. 그런 다음 마이크로서비스 아키텍처를 사용하도록 리팩토링합니다. Spring Boot를 사용하여 마이크로 서비스를 쉽게 구축하고 실행할 수 있습니다.

## 모놀리식 아키텍처

모놀리식 애플리케이션에서는 모든 구성 요소가 밀접하게 결합되어 동일한 데이터베이스를 공유합니다. 따라서 애플리케이션을 쉽게 개발, 배포 및 테스트할 수 있습니다. 그러나 응용 프로그램을 확장하기가 어렵습니다.

![모놀리식 아키텍처](https://springframework.guru/wp-content/uploads/2015/06/monolitic-architecture.png)

주문 서비스와 고객 서비스가 있는 모놀리식 애플리케이션이 있다고 가정해 보겠습니다. 주문 서비스에는 주문을 생성하기 위해 끝점을 노출하는 RestController가 있습니다. 고객 서비스에는 고객을 생성하기 위해 끝점을 노출하는 RestController가 있습니다.

```java
@RestController
public class OrderController {
    
    @Autowired
    private OrderService orderService;

    @PostMapping("/orders")
    public Order createOrder(@RequestBody Order order) {
        return orderService.createOrder(order);
    }
}
```

```java
@RestController
public class CustomerController {
    
    @Autowired
    private CustomerService customerService;

    @PostMapping("/customers")
    public Customer createCustomer(@RequestBody Customer customer) {
        return customerService.createCustomer(customer);
    }
}
```

OrderService에는 주문을 생성하는 메서드가 있습니다. CustomerService에는 고객을 만드는 방법이 있습니다. 두 방법 모두 DAO를 호출하여 데이터를 데이터베이스에 유지합니다.

```java
@Service
public class OrderService {

    @Autowired
    private OrderDao orderDao;

    public Order createOrder(Order order) {
        // do some business logic
        return orderDao.createOrder(order);
    }
}
```

```java
@Service
public class CustomerService {

    @Autowired
    private CustomerDao customerDao;

    public Customer createCustomer(Customer customer) {
        // do some business logic
        return customerDao.createCustomer(customer);
    }
}
```

모놀리식 아키텍처에서는 모든 구성 요소가 긴밀하게 결합됩니다. 따라서 애플리케이션을 쉽게 개발, 배포 및 테스트할 수 있습니다. 그러나 응용 프로그램을 확장하기가 어렵습니다.

## 마이크로서비스 아키텍처

마이크로 서비스 아키텍처에서 구성 요소는 느슨하게 결합되어 있으며 각 서비스에는 자체 데이터베이스가 있습니다. 이렇게 하면 응용 프로그램을 쉽게 확장할 수 있지만 응용 프로그램을 개발, 배포 및 테스트하기가 더 어려워집니다.

![마이크로서비스 아키텍처](https://springframework.guru/wp-content/uploads/2015/06/microservices-architecture.png)

주문 서비스와 고객 서비스가 있는 마이크로서비스 아키텍처가 있다고 가정해 보겠습니다. 주문 서비스에는 주문을 생성하기 위해 끝점을 노출하는 RestController가 있습니다. 고객 서비스에는 고객을 생성하기 위해 끝점을 노출하는 RestController가 있습니다.

```java
@RestController
public class OrderController {
    
    @Autowired
    private OrderService orderService;

    @PostMapping("/orders")
    public Order createOrder(@RequestBody Order order) {
        return orderService.createOrder(order);
    }
}
```

```java
@RestController
public class CustomerController {
    
    @Autowired
    private CustomerService customerService;

    @PostMapping("/customers")
    public Customer createCustomer(@RequestBody Customer customer) {
        return customerService.createCustomer(customer);
    }
}
```

OrderService에는 주문을 생성하는 메서드가 있습니다. CustomerService에는 고객을 만드는 방법이 있습니다. 두 방법 모두 DAO를 호출하여 데이터를 데이터베이스에 유지합니다.

```java
@Service
public class OrderService {

    @Autowired
    private OrderDao orderDao;

    public Order createOrder(Order order) {
        // do some business logic
        return orderDao.createOrder(order);
    }
}
```

```java
@Service
public class CustomerService {

    @Autowired
    private CustomerDao customerDao;

    public Customer createCustomer(Customer customer) {
        // do some business logic
        return customerDao.createCustomer(customer);
    }
}
```

DAO 클래스는 인터페이스 기반이며 JdbcTemplate을 사용하여 데이터베이스를 쿼리합니다. OrderDao에는 주문을 생성하는 방법이 있습니다. CustomerDao에는 고객을 생성하는 방법이 있습니다.

```java
public interface OrderDao {

    public Order createOrder(Order order);
}
```

```java
public interface CustomerDao {

    public Customer createCustomer(Customer customer);
}
```

```java
@Repository
public class OrderDaoImpl implements OrderDao {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    public Order createOrder(Order order) {
        // use JdbcTemplate to query the database
        return null;
    }
}
```

```java
@Repository
public class CustomerDaoImpl implements CustomerDao {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    public Customer createCustomer(Customer customer) {
        // use JdbcTemplate to query the database
        return null;
    }
}
```

마이크로서비스 아키텍처에서 구성 요소는 느슨하게 결합됩니다. 이렇게 하면 응용 프로그램을 쉽게 확장할 수 있지만 응용 프로그램을 개발, 배포 및 테스트하기가 더 어려워집니다.

## 스프링 부트 사용

Spring Boot를 사용하면 "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다. 또한 마이크로서비스를 쉽게 만들 수 있습니다.

주문 서비스와 고객 서비스로 마이크로서비스 아키텍처를 만들고 싶다고 가정해 보겠습니다. Spring Boot를 사용하여 서비스를 만들 수 있습니다.

먼저 두 서비스의 종속성을 정의하는 상위 POM이 있는 Maven 프로젝트를 만듭니다.

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.0.3.RELEASE</version>
</parent>

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

다음으로 주문 서비스를 생성합니다. Spring Boot 애플리케이션 클래스와 RestController를 생성합니다.

```java
@SpringBootApplication
public class OrderServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(OrderServiceApplication.class, args);
    }
}
```

```java
@RestController
public class OrderController {
    
    @Autowired
    private OrderService orderService;

    @PostMapping("/orders")
    public Order createOrder(@RequestBody Order order) {
        return orderService.createOrder(order);
    }
}
```

OrderService에는 주문을 생성하는 메서드가 있습니다. 이 메서드는 DAO를 호출하여 데이터를 데이터베이스에 유지합니다.

```java
@Service
public class OrderService {

    @Autowired
    private OrderDao orderDao;

    public Order createOrder(Order order) {
        // do some business logic
        return orderDao.createOrder(order);
    }
}
```

DAO 클래스는 인터페이스 기반이며 JdbcTemplate을 사용하여 데이터베이스를 쿼리합니다. OrderDao에는 주문을 생성하는 방법이 있습니다.

```java
public interface OrderDao {

    public Order createOrder(Order order);
}
```

```java
@Repository
public class OrderDaoImpl implements OrderDao {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    public Order createOrder(Order order) {
        // use JdbcTemplate to query the database
        return null;
    }
}
```

동일한 방식으로 고객 서비스를 만들 수 있습니다.

```java
@SpringBootApplication
public class CustomerServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(CustomerServiceApplication.class, args);
    }
}
```

```java
@RestController
public class CustomerController {
    
    @Autowired
    private CustomerService customerService;

    @PostMapping("/customers")
    public Customer createCustomer(@RequestBody Customer customer) {
        return customerService.createCustomer(customer);
    }
}
```

```java
@Service
public class CustomerService {

    @Autowired
    private CustomerDao customerDao;

    public Customer createCustomer(Customer customer) {
        // do some business logic
        return customerDao.createCustomer(customer);
    }
}
```

```java
public interface CustomerDao {

    public Customer createCustomer(Customer customer);
}
```

```java
@Repository
public class CustomerDaoImpl implements CustomerDao {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    public Customer createCustomer(Customer customer) {
        // use JdbcTemplate to query the database
        return null;
    }
}
```

각 서비스를 JAR 파일로 패키징하고 java -jar 명령으로 실행할 수 있습니다.

```
$ java -jar order-service.jar
```

```
$ java -jar customer-service.jar
```