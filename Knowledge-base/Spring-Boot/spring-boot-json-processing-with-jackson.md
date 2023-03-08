---
title: Jackson을 사용한 Spring Boot JSON 처리
description: 
published: true
date: 2023-01-31T13:17:51.766Z
tags: 
editor: markdown
dateCreated: 2023-01-31T13:17:50.052Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Spring Boot JSON Processing with Jackson***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-json-processing-with-jackson)
{.links-list}



# Jackson을 사용한 Spring Boot JSON 처리

JSON(JavaScript Object Notation)은 사람이 쉽게 읽고 쓸 수 있는 가벼운 데이터 교환 형식입니다. Jackson은 JSON을 직렬화 및 역직렬화하는 강력한 Java 라이브러리입니다.

이 기사에서는 Jackson을 사용하여 JSON을 Java 객체로 또는 그 반대로 변환하는 방법을 살펴보겠습니다.


## 메이븐 종속성

먼저 pom.xml 파일에 Jackson 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.9.9</version>
</dependency>
```

## JSON을 Java 객체로 변환

`ObjectMapper` 클래스의 `readValue()` 메소드를 사용하여 JSON 문자열을 Java 객체로 변환할 수 있습니다.

다음 JSON 문자열을 고려하십시오.

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

`readValue()` 메서드를 사용하여 이 JSON 문자열을 Java `Person` 개체로 변환할 수 있습니다.

```java
ObjectMapper mapper = new ObjectMapper();
String jsonString = "{\"name\":\"John Doe\",\"age\":30,\"address\":{\"street\":\"123 Main Street\",\"city\":\"New York\",\"state\":\"NY\",\"zip\":\"10001\"},\"phoneNumbers\":[{\"type\":\"home\",\"number\":\"212 555-1234\"},{\"type\":\"work\",\"number\":\"646 555-4567\"}]}";
Person person = mapper.readValue(jsonString, Person.class);
```

`readValue()` 메서드는 JSON 문자열과 대상 Java 클래스의 두 가지 인수를 사용합니다. `Person` 클래스에는 JSON 데이터에 해당하는 필드가 있어야 합니다.

```java
public class Person {
  private String name;
  private int age;
  private Address address;
  private List<PhoneNumber> phoneNumbers;
  
  // getters and setters
}
```

`Address` 및 `PhoneNumber` 클래스는 유사하게 정의됩니다.

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

위의 코드를 실행한 후 `person` 객체는 다음 데이터를 갖게 됩니다.

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

## Java 개체를 JSON으로 변환

`ObjectMapper` 클래스의 `writeValueAsString()` 메소드를 사용하여 Java 객체를 JSON 문자열로 변환할 수 있습니다.

다음 Java `Person` 개체를 고려하십시오.

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

`writeValueAsString()` 메서드를 사용하여 이 Java 객체를 JSON 문자열로 변환할 수 있습니다.

```java
ObjectMapper mapper = new ObjectMapper();
String jsonString = mapper.writeValueAsString(person);
```

`writeValueAsString()` 메서드는 `person` 개체의 JSON 문자열 표현을 반환합니다. 출력은 다음 JSON 문자열입니다.

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

## 결론

이 기사에서는 Jackson을 사용하여 JSON을 Java 객체로 또는 그 반대로 변환하는 방법을 살펴보았습니다. Jackson은 Java에서 JSON 데이터를 처리하기 위한 강력한 라이브러리입니다.