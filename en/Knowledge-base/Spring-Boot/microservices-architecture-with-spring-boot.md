---
title: Microservices Architecture with Spring Boot
description: 
published: true
date: 2023-02-17T18:01:30.669Z
tags: 
editor: markdown
dateCreated: 2023-01-30T02:54:59.142Z
---

- [Spring Boot를 사용한 마이크로서비스 아키텍처***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/microservices-architecture-with-spring-boot)
{.links-list}


Microservices have been a popular architectural style for building cloud applications for some time. Spring Boot is a framework that makes it easy to create stand-alone, production-grade Spring-based Applications that you can "just run". In this post, we'll take a look at how to use Spring Boot to build a microservices architecture.

We'll start with a simple example of a monolithic application. Then we'll refactor it to use a microservices architecture. We'll use Spring Boot to make it easy to build and run our microservices.

## Monolithic Architecture

In a monolithic application, all the components are tightly coupled and share the same database. This makes it easy to develop, deploy, and test the application. However, it also makes it difficult to scale the application.

![Monolithic Architecture](https://springframework.guru/wp-content/uploads/2015/06/monolitic-architecture.png)

Let's say we have a monolithic application that has a Order Service and a Customer Service. The Order Service has a RestController that exposes an endpoint to create an order. The Customer Service has a RestController that exposes an endpoint to create a customer.

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

The OrderService has a method to create an order. The CustomerService has a method to create a customer. Both methods call a DAO to persist the data to the database.

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

In a monolithic architecture, all the components are tightly coupled. This makes it easy to develop, deploy, and test the application. However, it also makes it difficult to scale the application.

## Microservices Architecture

In a microservices architecture, the components are loosely coupled and each service has its own database. This makes it easy to scale the application, but it also makes it more difficult to develop, deploy, and test the application.

![Microservices Architecture](https://springframework.guru/wp-content/uploads/2015/06/microservices-architecture.png)

Let's say we have a microservices architecture that has a Order Service and a Customer Service. The Order Service has a RestController that exposes an endpoint to create an order. The Customer Service has a RestController that exposes an endpoint to create a customer.

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

The OrderService has a method to create an order. The CustomerService has a method to create a customer. Both methods call a DAO to persist the data to the database.

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

DAO classes are interface-based and use the JdbcTemplate to query the database. The OrderDao has a method to create an order. The CustomerDao has a method to create a customer.

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

In a microservices architecture, the components are loosely coupled. This makes it easy to scale the application, but it also makes it more difficult to develop, deploy, and test the application.

## Using Spring Boot

Spring Boot makes it easy to create stand-alone, production-grade Spring-based Applications that you can "just run". It also makes it easy to create microservices.

Let's say we want to create a microservices architecture with a Order Service and a Customer Service. We can use Spring Boot to create the services.

First, we'll create a Maven project with a parent POM that defines the dependencies for both services.

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

Next, we'll create the Order Service. We'll create a Spring Boot application class and a RestController.

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

The OrderService has a method to create an order. The method calls a DAO to persist the data to the database.

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

DAO classes are interface-based and use the JdbcTemplate to query the database. The OrderDao has a method to create an order.

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

We can create the Customer Service in the same way.

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

We can package each service as a JAR file and run it with the java -jar command.

```
$ java -jar order-service.jar
```

```
$ java -jar customer-service.jar
```