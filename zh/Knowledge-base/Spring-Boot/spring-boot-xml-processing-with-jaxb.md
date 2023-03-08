---
title: 使用 JAXB 进行 Spring Boot XML 处理
description: 
published: true
date: 2023-02-03T05:58:44.955Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:58:43.289Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot XML Processing with JAXB***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-xml-processing-with-jaxb)
{.links-list}


# 使用 JAXB 进行 Spring Boot XML 处理

Java XML 绑定体系结构 (JAXB) 是一种允许 Java 开发人员将 Java 对象映射到 XML 表示的技术。 JAXB 提供了两个主要特性：将 Java 对象编组为 XML 的能力以及将 XML 解编回 Java 对象的能力。

在本文中，我们将了解如何使用 JAXB 和 Spring Boot 来处理 XML 文件。我们将从 JAXB 的简要概述开始，然后我们将深入研究一些代码示例。

## 什么是 JAXB？

正如我们上面提到的，JAXB 允许您将 Java 对象映射到 XML 表示，反之亦然。 JAXB 提供了可用于将 Java 对象映射到 XML 元素的注释。对 Java 类进行注释后，您可以使用 JAXB API 将它们编组（或转换）为 XML。您还可以使用 JAXB API 将 XML 解组（或转换）回 Java 对象。

JAXB 是一种标准技术，是 Java SE 平台的一部分。 JAXB 也包含在 Java EE 平台中。 JAXB 已经存在很长时间了，它是一项经过充分测试和广泛使用的技术。

## 在 Spring Boot 中使用 JAXB

Spring Boot 可以轻松创建独立的、生产级的基于 Spring 的应用程序，您可以“直接运行”。我们将在本文中使用 Spring Boot，以便轻松启动和运行我们的 XML 处理示例。

要将 JAXB 与 Spring Boot 一起使用，您需要将以下依赖项添加到您的 `pom.xml` 文件中：

```xml
<dependency>
   <groupId>com.sun.xml.bind</groupId>
   <artifactId>jaxb-impl</artifactId>
   <version>2.2.11</version>
</dependency>
```

有了这个依赖，我们现在可以创建一个使用 JAXB 来处理 XML 的 Spring Boot 应用程序。

## 创建一个 Spring Boot 应用程序

我们将从创建一个简单的 Spring Boot 应用程序开始，该应用程序使用 JAXB 来编组和解组 XML。为此，我们将使用“spring-boot-starter-jaxb”依赖项。此依赖项将引入我们将 JAXB 与 Spring Boot 结合使用所需的所有依赖项。

这是我们项目的“pom.xml”文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>spring-boot-jaxb-example</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>jar</packaging>

    <name>spring-boot-jaxb-example</name>
    <description>Example project for Spring Boot</description>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.4.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jaxb</artifactId>
        </dependency>

        <dependency>
            <groupId>javax.xml.bind</groupId>
            <artifactId>jaxb-api</artifactId>
            <version>2.3.0</version>
        </dependency>

        <dependency>
            <groupId>com.sun.xml.bind</groupId>
            <artifactId>jaxb-impl</artifactId>
            <version>2.3.0</version>
        </dependency>

        <dependency>
            <groupId>com.sun.xml.bind</groupId>
            <artifactId>jaxb-core</artifactId>
            <version>2.3.0</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>


</project>

```

请注意，除了 spring-boot-starter-jaxb 依赖项之外，我们还包括了 jaxb-api、jaxb-impl 和 jaxb-core 依赖项。我们的应用程序需要这些依赖项才能编译。

现在我们已经有了我们的依赖项，让我们创建一个简单的 Spring Boot 应用程序，它使用 JAXB 来编组和解组 XML。

## 使用 JAXB 编组和解组 XML

我们将从创建一个简单的 Spring Boot 应用程序开始，该应用程序使用 JAXB 来编组和解组 XML。为此，我们将创建一个 Person 类，我们可以用它来表示 XML 中的人。我们将使用 JAXB 注释对此类进行注释，以便我们可以将其编组为 XML。

这是 Person 类：

```java
package com.example.xml;

import javax.xml.bind.annotation.XmlAccessType;
import javax.xml.bind.annotation.XmlAccessorType;
import javax.xml.bind.annotation.XmlAttribute;
import javax.xml.bind.annotation.XmlRootElement;

@XmlRootElement(name = "person")
@XmlAccessorType(XmlAccessType.FIELD)
public class Person {

    @XmlAttribute
    private String firstName;

    @XmlAttribute
    private String lastName;

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

}
```

如您所见，我们已经使用“@XmlRootElement”和“@XmlAccessorType”注释对此类进行了注释。我们还使用“@XmlAttribute”注解对“firstName”和“lastName”字段进行了注解。这些注释告诉 JAXB 如何将 `Person` 类映射到 XML。

现在我们有了 Person 类，让我们编写一个简单的 Spring Boot 应用程序，它使用 JAXB 来编组和解组 XML。

这是“应用程序”类：

```java
package com.example.xml;

import java.io.StringReader;

import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBException;
import javax.xml.bind.Marshaller;
import javax.xml.bind.Unmarshaller;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

	public static void main(String[] args) throws JAXBException {
		SpringApplication.run(Application.class, args);
		
		JAXBContext jaxbContext = JAXBContext.newInstance(Person.class);
		Marshaller marshaller = jaxbContext.createMarshaller();
		marshaller.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
		
		Person person = new Person();
		person.setFirstName("John");
		person.setLastName("Doe");
		
		marshaller.marshal(person, System.out);
		
		String xml = "<person firstName=\"Jane\" lastName=\"Doe\"/>";
		
		Unmarshaller unmarshaller = jaxbContext.createUnmarshaller();
		Person person2 = (Person) unmarshaller.unmarshal(new StringReader(xml));
		
		System.out.println(person2.getFirstName());
		System.out.println(person2.getLastName());
	}

}
```

在这个类中，我们创建了一个“main”方法，它使用 JAXB API 来编组和解组 XML。首先，我们创建一个 JAXBContext 并使用它来创建一个 Marshaller。我们将“JAXB_FORMATTED_OUTPUT”属性设置为“true”，以便 XML 在编组时能够很好地格式化。

接下来，我们创建一个 Person 对象并设置 firstName 和 lastName 字段。然后我们将 Person 对象编组为 XML 并将其打印到控制台。

最后，我们创建一个表示“Person”的 XML 字符串。然后，我们使用 `JAXBContext` 创建一个 `Unmarshaller` 并使用它将 XML 字符串解组回 `Person` 对象。我们将 Person 对象的 firstName 和 lastName 字段打印到控制台以验证它是否已正确解组。

如果我们运行这个应用程序，我们应该看到以下输出：

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<person firstName="John" lastName="Doe"/>
Jane
Doe
```

如我们所见，XML 已正确编组和解组。

## 结论

在本文中，我们了解了如何结合使用 JAXB 和 Spring Boot 来处理 XML 文件。我们首先简要概述了 JAXB，然后深入研究了一些代码示例。

JAXB 是一种成熟的技术，广泛用于在 Java 应用程序中处理 XML。 JAXB 提供了一种将 Java 对象映射到 XML 的简单方法，反之亦然。 Spring Boot 使得在应用程序中使用 JAXB 变得简单，只需几个简单的依赖项。

这只是对将 JAXB 与 Spring Boot 结合使用的简要介绍。如果您有兴趣了解更多信息，请查看以下资源：

* [Spring Boot 和 XML 教程](https://spring.io/blog/2013/12/19/building-a-restful-web-service-with-xml-payloads)
* [JAXB 教程](https://www.javatpoint.com/jaxb-tutorial)
* [使用 JAXB 进行 Java XML 处理](https://www.baeldung.com/jaxb-tutorial)