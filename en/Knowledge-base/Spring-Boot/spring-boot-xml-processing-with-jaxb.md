---
title: Spring Boot XML Processing with JAXB
description: 
published: true
date: 2023-02-03T05:58:48.155Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:58:43.292Z
---

- [Procesamiento Spring Boot XML con JAXB***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-xml-processing-with-jaxb)
{.links-list}
- [使用 JAXB 进行 Spring Boot XML 处理***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-xml-processing-with-jaxb)
{.links-list}
- [JAXB를 사용한 Spring Boot XML 처리***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-xml-processing-with-jaxb)
{.links-list}


# Spring Boot XML Processing with JAXB

Java Architecture for XML Binding (JAXB) is a technology that allows Java developers to map Java objects to XML representations. JAXB provides two main features: the ability to marshal Java objects into XML and the ability to unmarshal XML back into Java objects. 

In this article, we'll take a look at how to use JAXB with Spring Boot to process XML files. We'll start with a brief overview of JAXB and then we'll dig into some code examples.

## What is JAXB?

As we mentioned above, JAXB allows you to map Java objects to XML representations and vice versa. JAXB provides annotations that you can use to map Java objects to XML elements. Once you've annotated your Java classes, you can use the JAXB API to marshal (or convert) them into XML. You can also use the JAXB API to unmarshal (or convert) XML back into Java objects. 

JAXB is a standard technology that is part of the Java SE platform. JAXB is also included in Java EE platforms. JAXB has been around for a long time and it's a well-tested and widely-used technology. 

## Using JAXB with Spring Boot

Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run". We'll use Spring Boot in this article to make it easy to get up and running with our XML processing example.

To use JAXB with Spring Boot, you need to add the following dependency to your `pom.xml` file:

```xml
<dependency>
   <groupId>com.sun.xml.bind</groupId>
   <artifactId>jaxb-impl</artifactId>
   <version>2.2.11</version>
</dependency>
```

With this dependency in place, we can now create a Spring Boot application that uses JAXB to process XML.

## Creating a Spring Boot Application

We're going to start by creating a simple Spring Boot application that uses JAXB to marshal and unmarshal XML. To do this, we'll use the `spring-boot-starter-jaxb` dependency. This dependency will pull in all of the dependencies that we need to use JAXB with Spring Boot.

Here's the `pom.xml` file for our project:

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

Note that we've included the `jaxb-api`, `jaxb-impl`, and `jaxb-core` dependencies in addition to the `spring-boot-starter-jaxb` dependency. These dependencies are required for our application to compile.

Now that we have our dependencies in place, let's create a simple Spring Boot application that uses JAXB to marshal and unmarshal XML.

## Marshalling and Unmarshalling XML with JAXB

We're going to start by creating a simple Spring Boot application that uses JAXB to marshal and unmarshal XML. To do this, we'll create a `Person` class that we can use to represent a person in XML. We'll annotate this class with JAXB annotations so that we can marshal it into XML.

Here's the `Person` class:

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

As you can see, we've annotated this class with the `@XmlRootElement` and `@XmlAccessorType` annotations. We've also annotated the `firstName` and `lastName` fields with the `@XmlAttribute` annotation. These annotations tell JAXB how to map the `Person` class to XML.

Now that we have our `Person` class, let's write a simple Spring Boot application that uses JAXB to marshal and unmarshal XML.

Here's the `Application` class:

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

In this class, we've created a `main` method that uses the JAXB API to marshal and unmarshal XML. First, we create a `JAXBContext` and use it to create a `Marshaller`. We set the `JAXB_FORMATTED_OUTPUT` property to `true` so that the XML will be formatted nicely when it's marshalled. 

Next, we create a `Person` object and set the `firstName` and `lastName` fields. We then marshal the `Person` object to XML and print it to the console.

Finally, we create an XML string that represents a `Person`. We then use the `JAXBContext` to create an `Unmarshaller` and use it to unmarshal the XML string back into a `Person` object. We print the `firstName` and `lastName` fields of the `Person` object to the console to verify that it was unmarshalled correctly.

If we run this application, we should see the following output:

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<person firstName="John" lastName="Doe"/>
Jane
Doe
```

As we can see, the XML was marshalled and unmarshalled correctly.

## Conclusion

In this article, we've taken a look at how to use JAXB with Spring Boot to process XML files. We've started with a brief overview of JAXB and then we've dug into some code examples.

JAXB is a well-established technology that is widely used for processing XML in Java applications. JAXB provides an easy way to map Java objects to XML and vice versa. Spring Boot makes it easy to use JAXB in your applications with a few simple dependencies.

This is just a brief introduction to using JAXB with Spring Boot. If you're interested in learning more, check out the following resources:

* [Spring Boot and XML tutorial](https://spring.io/blog/2013/12/19/building-a-restful-web-service-with-xml-payloads)
* [JAXB Tutorial](https://www.javatpoint.com/jaxb-tutorial)
* [Java XML Processing with JAXB](https://www.baeldung.com/jaxb-tutorial)