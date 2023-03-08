---
title: 013：使用 Spring Boot 和 REST 与外部系统集成
description: 
published: true
date: 2023-02-01T21:36:36.734Z
tags: 
editor: markdown
dateCreated: 2023-02-01T21:36:31.843Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [013: Integrating with external systems using Spring Boot and REST***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/013-integrating-with-external-systems-using-spring-boot-and-rest)
{.links-list}


# 介绍

在本文中，我们将研究如何使用 REST 将 Spring Boot 与外部系统集成。我们将使用一个简单的例子来说明如何做到这一点。

# 什么是休息？

REST 是 Representational State Transfer 的缩写。它是一种软件架构风格，定义了一组用于创建 Web 服务的约束。符合 REST 架构风格的 Web 服务称为 RESTful Web 服务。

# 为什么要使用 REST？

RESTful Web 服务易于构建，并且非常适合支持可扩展的分布式系统。 RESTful Web 服务可以构建在任何平台上，并且它们可以被任何支持 HTTP 协议的客户端使用。

# 如何创建 RESTful Web 服务？

有两种创建 RESTful Web 服务的方法：

1. 使用 JAX-RS 和 Jersey
2. 使用 Spring Boot

在本文中，我们将重点介绍如何使用 Spring Boot 创建 RESTful Web 服务。

# 什么是 Spring Boot？

Spring Boot 是一个框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序。它提供了一种自以为是的方法来配置和构建基于 Spring 的应用程序。

# 为什么要使用 Spring Boot？

Spring Boot 可以轻松创建独立的、生产级的基于 Spring 的应用程序。它提供了广泛的功能，可用于构建、测试和部署基于 Spring 的应用程序。

# 如何使用 Spring Boot 创建 RESTful Web 服务？

我们将使用以下工具和技术来创建基于 Spring Boot 的 RESTful Web 服务：

1.Java 8
2.行家3.3.9
3. Spring Boot 1.5.4.RELEASE
4. Eclipse 霓虹灯.3

# 创建项目

我们将使用 Spring Initializr 来生成我们的 Spring Boot 项目。我们将使用以下设置：

1.组：com.example
2.神器：spring-boot-rest
3.名称：Spring Boot REST
4.说明：Spring Boot REST实例
5.包名：com.example.springbootrest
6. 包装：广口瓶
7.Java版本：1.8
8. 选择以下依赖项：Web、JPA、H2

# 配置项目

我们将使用 H2 作为我们的数据库。我们将在 application.properties 文件中配置 H2：

spring.h2.console.enabled=true
spring.h2.console.path=/h2

# 创建实体

我们将创建一个名为 Employee 的简单实体：

@实体
公共课员工{

    @ID
    @生成值
    私人长号；

    私有字符串名称；

    私有字符串角色；

    // 获取器和设置器
}

# 创建存储库

我们将为我们的 Employee 实体创建一个简单的 JpaRepository 接口：

public interface EmployeeRepository extends JpaRepository<Employee, Long> {

}

# 创建服务

我们将创建一个简单的 EmployeeService 接口：

公共接口员工服务{

    员工保存（员工员工）；

    列表<员工> findAll();

    员工 findOne(长 id);

    void delete(Long id);
}

# 创建服务实现

我们将创建一个简单的 EmployeeServiceImpl 类：

@服务
公共类 EmployeeServiceImpl 实现 EmployeeService {

    @Autowired
    私人雇员资料库雇员资料库；

    @覆盖
    公共雇员保存（雇员雇员）{
        返回 employeeRepository.save(employee);
    }

    @覆盖
    公共列表<员工> findAll() {
        返回 employeeRepository.findAll();
    }

    @覆盖
    public Employee findOne(Long id) {
        返回 employeeRepository.findOne(id);
    }

    @覆盖
    public void delete(Long id) {
        employeeRepository.delete(id);
    }
}

# 创建 REST 控制器

我们将创建一个简单的 EmployeeController 类：

@RestController
@RequestMapping("/雇员")
公共类 EmployeeController {

    @Autowired
    私有 EmployeeService 雇员服务；

    @RequestMapping(方法= RequestMethod.GET)
    公共列表<员工> findAll() {
        返回 employeeService.findAll();
    }

    @RequestMapping(方法= RequestMethod.POST)
    public Employee save(@RequestBody Employee 雇员) {
        返回 employeeService.save(employee);
    }

    @RequestMapping(method = RequestMethod.GET, value = "/{id}")
    public Employee findOne(@PathVariable Long id) {
        返回 employeeService.findOne(id);
    }

    @RequestMapping(method = RequestMethod.DELETE, value = "/{id}")
    public void delete(@PathVariable Long id) {
        employeeService.delete(id);
    }
}

# 测试 REST 控制器

我们将使用以下 curl 命令来测试我们的 EmployeeController：

要保存员工：

curl -X POST -H "Content-Type: application/json" -d '{"name":"John Smith","role":"Developer"}' http://localhost:8080/employees

查找所有员工：

curl -X GET http://localhost:8080/employees

查找 ID 为 1 的员工：

curl -X GET http://localhost:8080/employees/1

删除 ID 为 1 的员工：

curl -X DELETE http://localhost:8080/employees/1

# 结论

在本文中，我们了解了如何使用 Spring Boot 创建 RESTful Web 服务。我们看到了如何创建项目、配置项目、创建实体、创建存储库、创建服务、创建服务实现、创建 REST 控制器以及测试 REST 控制器。