---
title: 013: Integrating with external systems using Spring Boot and REST
description: 
published: true
date: 2023-02-01T21:36:34.270Z
tags: 
editor: markdown
dateCreated: 2023-02-01T21:36:31.850Z
---

- [013: Integración con sistemas externos usando Spring Boot y REST***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/013-integrating-with-external-systems-using-spring-boot-and-rest)
{.links-list}
- [013：使用 Spring Boot 和 REST 与外部系统集成***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/013-integrating-with-external-systems-using-spring-boot-and-rest)
{.links-list}
- [013: Spring Boot 및 REST를 사용하여 외부 시스템과 통합***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/013-integrating-with-external-systems-using-spring-boot-and-rest)
{.links-list}


# Introduction

In this post, we will look at how to integrate Spring Boot with external systems using REST. We will use a simple example to illustrate how this can be done.

# What is REST?

REST is an acronym for Representational State Transfer. It is a software architectural style that defines a set of constraints to be used for creating web services. Web services that conform to the REST architectural style are called RESTful web services.

# Why use REST?

RESTful web services are easy to build and they are well suited for supporting scalable, distributed systems. RESTful web services can be built on any platform and they can be consumed by any client that supports the HTTP protocol.

# How to create a RESTful web service?

There are two ways to create a RESTful web service:

1. Using JAX-RS and Jersey
2. Using Spring Boot

In this post, we will focus on how to create a RESTful web service using Spring Boot.

# What is Spring Boot?

Spring Boot is a framework that makes it easy to create stand-alone, production-grade Spring-based applications. It provides a opinionated approach to configuring and building Spring-based applications.

# Why use Spring Boot?

Spring Boot makes it easy to create stand-alone, production-grade Spring-based applications. It provides a wide range of features that can be used to build, test, and deploy Spring-based applications.

# How to create a RESTful web service using Spring Boot?

We will use the following tools and technologies to create our Spring Boot-based RESTful web service:

1. Java 8
2. Maven 3.3.9
3. Spring Boot 1.5.4.RELEASE
4. Eclipse Neon.3

# Creating the Project

We will use Spring Initializr to generate our Spring Boot project. We will use the following settings:

1. Group: com.example
2. Artifact: spring-boot-rest
3. Name: Spring Boot REST
4. Description: Spring Boot REST Example
5. Package Name: com.example.springbootrest
6. Packaging: Jar
7. Java Version: 1.8
8. Select the following dependencies: Web, JPA, H2

# Configuring the Project

We will use H2 as our database. We will configure H2 in the application.properties file:

spring.h2.console.enabled=true
spring.h2.console.path=/h2

# Creating the Entity

We will create a simple entity called Employee:

@Entity
public class Employee {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    private String role;

    // Getters and setters
}

# Creating the Repository

We will create a simple JpaRepository interface for our Employee entity:

public interface EmployeeRepository extends JpaRepository<Employee, Long> {

}

# Creating the Service

We will create a simple EmployeeService interface:

public interface EmployeeService {

    Employee save(Employee employee);

    List<Employee> findAll();

    Employee findOne(Long id);

    void delete(Long id);
}

# Creating the Service Implementation

We will create a simple EmployeeServiceImpl class:

@Service
public class EmployeeServiceImpl implements EmployeeService {

    @Autowired
    private EmployeeRepository employeeRepository;

    @Override
    public Employee save(Employee employee) {
        return employeeRepository.save(employee);
    }

    @Override
    public List<Employee> findAll() {
        return employeeRepository.findAll();
    }

    @Override
    public Employee findOne(Long id) {
        return employeeRepository.findOne(id);
    }

    @Override
    public void delete(Long id) {
        employeeRepository.delete(id);
    }
}

# Creating the REST Controller

We will create a simple EmployeeController class:

@RestController
@RequestMapping("/employees")
public class EmployeeController {

    @Autowired
    private EmployeeService employeeService;

    @RequestMapping(method = RequestMethod.GET)
    public List<Employee> findAll() {
        return employeeService.findAll();
    }

    @RequestMapping(method = RequestMethod.POST)
    public Employee save(@RequestBody Employee employee) {
        return employeeService.save(employee);
    }

    @RequestMapping(method = RequestMethod.GET, value = "/{id}")
    public Employee findOne(@PathVariable Long id) {
        return employeeService.findOne(id);
    }

    @RequestMapping(method = RequestMethod.DELETE, value = "/{id}")
    public void delete(@PathVariable Long id) {
        employeeService.delete(id);
    }
}

# Testing the REST Controller

We will use the following curl commands to test our EmployeeController:

To save an employee:

curl -X POST -H "Content-Type: application/json" -d '{"name":"John Smith","role":"Developer"}' http://localhost:8080/employees

To find all employees:

curl -X GET http://localhost:8080/employees

To find an employee with id 1:

curl -X GET http://localhost:8080/employees/1

To delete an employee with id 1:

curl -X DELETE http://localhost:8080/employees/1

# Conclusion

In this post, we looked at how to create a RESTful web service using Spring Boot. We saw how to create the project, configure the project, create the entity, create the repository, create the service, create the service implementation, create the REST controller, and test the REST controller.