---
title: 用于后端开发的 ORM 和自动缩放
description: 
published: true
date: 2023-02-17T18:04:25.060Z
tags: 
editor: markdown
dateCreated: 2023-01-30T12:17:11.428Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [ORM and Auto-scaling for Backend Development***English** version of this document is available*](/en/Knowledge-base/Backend/orm-and-auto-scaling-for-backend-development)
{.links-list}
 


# 用于后端开发的 ORM 和自动缩放

在本文中，我们将了解后端开发的两个重要概念：ORM（对象关系映射）和自动缩放。

## 对象关系管理

ORM 是一种允许开发人员使用对象处理数据库的技术。换句话说，它提供了对象和数据库表之间的映射。这种映射可以通过两种方式完成：

- **基于注释的映射**：在这种方法中，开发人员使用指定类和数据库表之间映射的元数据来注释他们的 Java 类。

- **基于 XML 的映射**：在这种方法中，开发人员在 XML 文档中指定映射。然后 ORM 工具使用该文档来生成数据库模式和 Java 类。

使用 ORM 有几个好处：

- **它使开发更快、更容易**：开发人员可以专注于他们应用程序的业务逻辑，让 ORM 工具处理数据库交互。

- **它减少了需要编写的代码量**：ORM工具可以生成与数据库交互的SQL代码，这意味着开发人员不必自己编写这些代码。

- **它使应用程序更具可移植性**：由于数据库交互由 ORM 工具处理，因此如果需要，应用程序可以轻松迁移到不同的数据库。

有多种 ORM 工具可用，例如 Hibernate、EclipseLink 和 iBatis。在本文中，我们将重点关注 Hibernate。

### 休眠

Hibernate 是一种流行的 ORM 工具，它提供基于注释和基于 XML 的映射。它还具有许多其他功能，例如支持缓存和延迟加载。

 让我们看一下如何使用 Hibernate 将 Java 类映射到数据库表。我们将使用以下 Java 类作为示例：

```java
public class Employee {
    private Long id;
    private String name;
    private Integer age;
    private Double salary;
    
    // Getters and setters...
}
```

我们会将其映射到以下数据库表：

```sql
CREATE TABLE employee (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    age INTEGER,
    salary REAL
);
```

映射可以通过两种方式完成：

- **基于注释的映射**：

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

- **基于 XML 的映射**：

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

在这两种情况下，我们都需要指定 Employee 类将映射到的数据库表的名称。我们还需要为 Employee 类中的每个字段指定映射。对于 id 字段，我们需要指定它是表的主键，并且它是由数据库生成的（自增）。

映射完成后，我们可以编写代码来插入、更新、删除和查询员工：

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

在上面的代码片段中，我们首先将一个员工插入到数据库中。然后，我们更新员工的薪水，最后，我们删除员工。我们还查询数据库以获取所有员工的列表。

## 自动缩放

自动缩放是一种允许开发人员水平缩放其应用程序的技术。换句话说，它允许开发人员在应用程序负载增加时向其应用程序添加新服务器。这与垂直扩展形成对比，后者涉及增加单个服务器的资源。

使用自动缩放有两个好处：

- **它允许应用程序处理更多负载**：由于可以根据需要添加新服务器，因此应用程序可以处理更多流量而不会出现性能问题。

- **更具成本效益**：由于可以根据需要添加和删除新服务器，开发人员只需为他们使用的资源付费。

自动缩放可以手动或自动完成。在本文中，我们将重点关注自动自动缩放。

### 自动自动缩放

自动自动缩放涉及使用工具来监视应用程序上的负载并根据需要添加和删除服务器。有多种工具可用，例如 Apache httpd、nginx 和 HAProxy。在本文中，我们将重点关注 Apache httpd。

Apache httpd 是一种流行的 Web 服务器，可用于创建自动缩放应用程序。它有一个名为 mod_cluster 的模块，可用于根据需要添加和删除服务器。

mod_cluster 模块的工作原理如下：

- **它监控应用程序的负载**：模块定期向应用程序发送请求以检查响应时间。如果响应时间过长，说明应用负载过重，需要增加新的服务器。

- **它根据需要添加和删除服务器**：该模块可以通过向 mod_cluster 管理接口发出请求来向应用程序添加新服务器。同样，它可以删除不再需要的服务器。

让我们来看看如何使用 mod_cluster 模块来创建自动缩放应用程序。我们将使用以下 Apache httpd 配置：

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

在上面的配置中，我们定义了一个虚拟主机，它将为 www.example.com 域的请求提供服务。我们还定义了一个包含两个服务器的代理平衡器：localhost:8000 和 localhost:8001。最后，我们配置了 mod_cluster 以根据需要添加和删除服务器。

现在让我们编写一个简单的 PHP 应用程序，它将由 Apache httpd 服务器提供服务：

```php
<?php
$server = $_SERVER['SERVER_ADDR'];
echo "Hello, World! I'm running on $server";
?>
```

我们将在两台服务器上运行它：

- 本地主机：8000
- 本地主机：8001

当用户访问 www.example.com 网站时，他们将看到以下页面：

```
Hello, World! I'm running on 127.0.0.1
```

如果我们通过发出更多请求来增加应用程序的负载，mod_cluster 将根据需要添加新服务器。例如，如果我们每秒发出 10 个请求，mod_cluster 将添加两个新服务器。

## 结论

在本文中，我们了解了后端开发的两个重要概念：ORM 和自动缩放。我们已经了解了如何使用 ORM 将 Java 类映射到数据库表，以及如何使用自动缩放来根据需要向应用程序添加新服务器。