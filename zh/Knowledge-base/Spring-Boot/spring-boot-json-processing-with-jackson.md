---
title: 使用 Jackson 进行 Spring Boot JSON 处理
description: 
published: true
date: 2023-01-31T13:17:51.644Z
tags: 
editor: markdown
dateCreated: 2023-01-31T13:17:50.059Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Spring Boot JSON Processing with Jackson***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-json-processing-with-jackson)
{.links-list}



# 使用 Jackson 进行 Spring Boot JSON 处理

JSON（JavaScript 对象表示法）是一种轻量级数据交换格式，易于人类读写。 Jackson 是一个强大的 Java 库，用于序列化和反序列化 JSON。

在本文中，我们将了解如何使用 Jackson 将 JSON 转换为 Java 对象，反之亦然。


## Maven 依赖项

首先，我们需要将 Jackson 依赖项添加到我们的 pom.xml 文件中：

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.9.9</version>
</dependency>
```

## 将 JSON 转换为 Java 对象

我们可以使用 ObjectMapper 类的 readValue() 方法将 JSON 字符串转换为 Java 对象。

考虑以下 JSON 字符串：

```json
{
  "name": "John Doe",
  "age": 30,
  "address": {
    "street": "123 Main Street",
    "city": "New York",
    "state": "NY",
    "zip": "10001"
  },
  "phoneNumbers": [
    {
      "type": "home",
      "number": "212 555-1234"
    },
    {
      "type": "work",
      "number": "646 555-4567"
    }
  ]
}
```

我们可以使用 readValue() 方法将此 JSON 字符串转换为 Java Person 对象：

```java
ObjectMapper mapper = new ObjectMapper();
String jsonString = "{\"name\":\"John Doe\",\"age\":30,\"address\":{\"street\":\"123 Main Street\",\"city\":\"New York\",\"state\":\"NY\",\"zip\":\"10001\"},\"phoneNumbers\":[{\"type\":\"home\",\"number\":\"212 555-1234\"},{\"type\":\"work\",\"number\":\"646 555-4567\"}]}";
Person person = mapper.readValue(jsonString, Person.class);
```

`readValue()` 方法有两个参数：JSON 字符串和目标 Java 类。 `Person` 类必须有对应的 JSON 数据字段：

```java
public class Person {
  private String name;
  private int age;
  private Address address;
  private List<PhoneNumber> phoneNumbers;
  
  // getters and setters
}
```

`Address` 和 `PhoneNumber` 类的定义类似：

```java
public class Address {
  private String street;
  private String city;
  private String state;
  private String zip;
  
  // getters and setters
}

public class PhoneNumber {
  private String type;
  private String number;
  
  // getters and setters
}
```

运行上面的代码后，`person` 对象将具有以下数据：

```java
Person person = new Person();
person.setName("John Doe");
person.setAge(30);

Address address = new Address();
address.setStreet("123 Main Street");
address.setCity("New York");
address.setState("NY");
address.setZip("10001");
person.setAddress(address);

List<PhoneNumber> phoneNumbers = new ArrayList<>();

PhoneNumber homePhoneNumber = new PhoneNumber();
homePhoneNumber.setType("home");
homePhoneNumber.setNumber("212 555-1234");
phoneNumbers.add(homePhoneNumber);

PhoneNumber workPhoneNumber = new PhoneNumber();
workPhoneNumber.setType("work");
workPhoneNumber.setNumber("646 555-4567");
phoneNumbers.add(workPhoneNumber);

person.setPhoneNumbers(phoneNumbers);
```

## 将 Java 对象转换为 JSON

我们可以使用 ObjectMapper 类的 writeValueAsString() 方法将 Java 对象转换为 JSON 字符串。

考虑以下 Java `Person` 对象：

```java
Person person = new Person();
person.setName("John Doe");
person.setAge(30);

Address address = new Address();
address.setStreet("123 Main Street");
address.setCity("New York");
address.setState("NY");
address.setZip("10001");
person.setAddress(address);

List<PhoneNumber> phoneNumbers = new ArrayList<>();

PhoneNumber homePhoneNumber = new PhoneNumber();
homePhoneNumber.setType("home");
homePhoneNumber.setNumber("212 555-1234");
phoneNumbers.add(homePhoneNumber);

PhoneNumber workPhoneNumber = new PhoneNumber();
workPhoneNumber.setType("work");
workPhoneNumber.setNumber("646 555-4567");
phoneNumbers.add(workPhoneNumber);

person.setPhoneNumbers(phoneNumbers);
```

我们可以使用 `writeValueAsString()` 方法将此 Java 对象转换为 JSON 字符串：

```java
ObjectMapper mapper = new ObjectMapper();
String jsonString = mapper.writeValueAsString(person);
```

`writeValueAsString()` 方法返回 `person` 对象的 JSON 字符串表示。输出将是以下 JSON 字符串：

```json
{
  "name": "John Doe",
  "age": 30,
  "address": {
    "street": "123 Main Street",
    "city": "New York",
    "state": "NY",
    "zip": "10001"
  },
  "phoneNumbers": [
    {
      "type": "home",
      "number": "212 555-1234"
    },
    {
      "type": "work",
      "number": "646 555-4567"
    }
  ]
}
```

## 结论

在本文中，我们了解了如何使用 Jackson 将 JSON 转换为 Java 对象，反之亦然。 Jackson 是一个强大的 Java 处理 JSON 数据的库。