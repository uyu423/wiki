---
title: Spring Boot JSON Processing with Jackson
description: 
published: true
date: 2023-01-31T13:17:53.735Z
tags: 
editor: markdown
dateCreated: 2023-01-31T13:17:50.051Z
---

- [Jackson을 사용한 Spring Boot JSON 처리***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-json-processing-with-jackson)
{.links-list}
- [Jackson を使用した Spring Boot JSON 処理***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/spring-boot-json-processing-with-jackson)
{.links-list}
- [使用 Jackson 进行 Spring Boot JSON 处理***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-json-processing-with-jackson)
{.links-list}



# Spring Boot JSON Processing with Jackson

JSON (JavaScript Object Notation) is a lightweight data-interchange format that is easy for humans to read and write. Jackson is a powerful Java library to serialize and deserialize JSON.

In this article, we'll look at how to use Jackson to convert JSON to Java objects and vice versa.


## Maven Dependencies

First, we need to add the Jackson dependencies to our pom.xml file:

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.9.9</version>
</dependency>
```

## Converting JSON to Java Objects

We can use the `readValue()` method of the `ObjectMapper` class to convert a JSON string to a Java object.

Consider the following JSON string:

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

We can convert this JSON string to a Java `Person` object using the `readValue()` method:

```java
ObjectMapper mapper = new ObjectMapper();
String jsonString = "{\"name\":\"John Doe\",\"age\":30,\"address\":{\"street\":\"123 Main Street\",\"city\":\"New York\",\"state\":\"NY\",\"zip\":\"10001\"},\"phoneNumbers\":[{\"type\":\"home\",\"number\":\"212 555-1234\"},{\"type\":\"work\",\"number\":\"646 555-4567\"}]}";
Person person = mapper.readValue(jsonString, Person.class);
```

The `readValue()` method takes two arguments: the JSON string and the target Java class. The `Person` class must have corresponding fields for the JSON data:

```java
public class Person {
  private String name;
  private int age;
  private Address address;
  private List<PhoneNumber> phoneNumbers;
  
  // getters and setters
}
```

The `Address` and `PhoneNumber` classes are similarly defined:

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

After running the code above, the `person` object will have the following data:

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

## Converting Java Objects to JSON

We can use the `writeValueAsString()` method of the `ObjectMapper` class to convert a Java object to a JSON string.

Consider the following Java `Person` object:

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

We can convert this Java object to a JSON string using the `writeValueAsString()` method:

```java
ObjectMapper mapper = new ObjectMapper();
String jsonString = mapper.writeValueAsString(person);
```

The `writeValueAsString()` method returns a JSON string representation of the `person` object. The output will be the following JSON string:

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

## Conclusion

In this article, we've looked at how to use Jackson to convert JSON to Java objects and vice versa. Jackson is a powerful library for processing JSON data in Java.