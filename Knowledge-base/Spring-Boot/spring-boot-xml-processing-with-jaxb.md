---
title: JAXB를 사용한 Spring Boot XML 처리
description: 
published: true
date: 2023-02-03T05:58:44.901Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:58:43.283Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot XML Processing with JAXB***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-xml-processing-with-jaxb)
{.links-list}


# JAXB를 사용한 스프링 부트 XML 처리

JAXB(Java Architecture for XML Binding)는 Java 개발자가 Java 개체를 XML 표현에 매핑할 수 있도록 하는 기술입니다. JAXB는 Java 객체를 XML로 마샬링하는 기능과 XML을 다시 Java 객체로 언마샬링하는 기능의 두 가지 주요 기능을 제공합니다.

이 기사에서는 JAXB를 Spring Boot와 함께 사용하여 XML 파일을 처리하는 방법을 살펴보겠습니다. JAXB에 대한 간략한 개요부터 시작한 다음 몇 가지 코드 예제를 자세히 살펴보겠습니다.

## JAXB란?

위에서 언급했듯이 JAXB를 사용하면 Java 개체를 XML 표현에 매핑하거나 그 반대로 매핑할 수 있습니다. JAXB는 Java 객체를 XML 요소에 매핑하는 데 사용할 수 있는 주석을 제공합니다. Java 클래스에 주석을 달면 JAXB API를 사용하여 XML로 마샬링(또는 변환)할 수 있습니다. 또한 JAXB API를 사용하여 XML을 다시 Java 객체로 언마샬링(또는 변환)할 수 있습니다.

JAXB는 Java SE 플랫폼의 일부인 표준 기술입니다. JAXB는 Java EE 플랫폼에도 포함되어 있습니다. JAXB는 오랫동안 사용되어 왔으며 잘 테스트되고 널리 사용되는 기술입니다.

## 스프링 부트와 함께 JAXB 사용

Spring Boot를 사용하면 "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다. 이 기사에서는 Spring Boot를 사용하여 XML 처리 예제를 쉽게 시작하고 실행할 수 있습니다.

Spring Boot에서 JAXB를 사용하려면 `pom.xml` 파일에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
   <groupId>com.sun.xml.bind</groupId>
   <artifactId>jaxb-impl</artifactId>
   <version>2.2.11</version>
</dependency>
```

이 종속성이 있으면 이제 JAXB를 사용하여 XML을 처리하는 Spring Boot 애플리케이션을 만들 수 있습니다.

## 스프링 부트 애플리케이션 만들기

JAXB를 사용하여 XML을 마샬링 및 언마샬링하는 간단한 Spring Boot 애플리케이션을 만드는 것으로 시작하겠습니다. 이를 위해 `spring-boot-starter-jaxb` 종속성을 사용합니다. 이 종속성은 Spring Boot에서 JAXB를 사용하는 데 필요한 모든 종속성을 가져옵니다.

다음은 우리 프로젝트의 `pom.xml` 파일입니다.

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

`spring-boot-starter-jaxb` 종속성 외에도 `jaxb-api`, `jaxb-impl` 및 `jaxb-core` 종속성을 포함했습니다. 이러한 종속성은 애플리케이션을 컴파일하는 데 필요합니다.

이제 종속 항목이 준비되었으므로 JAXB를 사용하여 XML을 마샬링 및 언마샬링하는 간단한 Spring Boot 애플리케이션을 만들어 보겠습니다.

## JAXB로 XML 마샬링 및 언마샬링

JAXB를 사용하여 XML을 마샬링 및 언마샬링하는 간단한 Spring Boot 애플리케이션을 만드는 것으로 시작하겠습니다. 이를 위해 XML에서 사람을 나타내는 데 사용할 수 있는 `Person` 클래스를 만듭니다. 이 클래스를 XML로 마샬링할 수 있도록 JAXB 주석으로 이 클래스에 주석을 달 것입니다.

다음은 `Person` 클래스입니다.

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

보시다시피 `@XmlRootElement` 및 `@XmlAccessorType` 주석으로 이 클래스에 주석을 달았습니다. 또한 `@XmlAttribute` 주석으로 `firstName` 및 `lastName` 필드에 주석을 추가했습니다. 이러한 주석은 JAXB에게 `Person` 클래스를 XML에 매핑하는 방법을 알려줍니다.

이제 `Person` 클래스가 있으므로 JAXB를 사용하여 XML을 마샬링 및 언마샬링하는 간단한 Spring Boot 애플리케이션을 작성해 보겠습니다.

다음은 `Application` 클래스입니다.

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

이 클래스에서는 JAXB API를 사용하여 XML을 마샬링 및 언마샬링하는 `main` 메서드를 만들었습니다. 먼저 `JAXBContext`를 생성하고 이를 사용하여 `Marshaller`를 생성합니다. JAXB_FORMATTED_OUTPUT` 속성을 `true`로 설정하여 마샬링될 때 XML이 제대로 형식화되도록 합니다.

다음으로 `Person` 개체를 만들고 `firstName` 및 `lastName` 필드를 설정합니다. 그런 다음 `Person` 객체를 XML로 마샬링하고 콘솔에 출력합니다.

마지막으로 `Person`을 나타내는 XML 문자열을 만듭니다. 그런 다음 `JAXBContext`를 사용하여 `Unmarshaller`를 생성하고 이를 사용하여 XML 문자열을 다시 `Person` 객체로 언마샬링합니다. `Person` 개체의 `firstName` 및 `lastName` 필드를 콘솔에 출력하여 제대로 마샬링되지 않았는지 확인합니다.

이 애플리케이션을 실행하면 다음 출력이 표시됩니다.

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<person firstName="John" lastName="Doe"/>
Jane
Doe
```

보시다시피 XML은 올바르게 마샬링 및 마샬링 해제되었습니다.

## 결론

이 기사에서는 JAXB를 Spring Boot와 함께 사용하여 XML 파일을 처리하는 방법을 살펴보았습니다. JAXB에 대한 간략한 개요부터 시작한 다음 몇 가지 코드 예제를 살펴보았습니다.

JAXB는 Java 애플리케이션에서 XML을 처리하는 데 널리 사용되는 잘 정립된 기술입니다. JAXB는 Java 개체를 XML에 매핑하거나 그 반대로 매핑하는 쉬운 방법을 제공합니다. Spring Boot를 사용하면 몇 가지 간단한 종속성으로 애플리케이션에서 JAXB를 쉽게 사용할 수 있습니다.

이것은 Spring Boot와 함께 JAXB를 사용하는 방법에 대한 간략한 소개입니다. 자세히 알아보려면 다음 리소스를 확인하세요.

* [Spring Boot 및 XML 튜토리얼](https://spring.io/blog/2013/12/19/building-a-restful-web-service-with-xml-payloads)
* [JAXB 튜토리얼](https://www.javatpoint.com/jaxb-tutorial)
* [JAXB를 이용한 자바 XML 처리](https://www.baeldung.com/jaxb-tutorial)