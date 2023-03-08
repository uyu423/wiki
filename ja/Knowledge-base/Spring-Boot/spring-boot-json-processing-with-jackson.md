---
title: Jackson を使用した Spring Boot JSON 処理
description: 
published: true
date: 2023-01-31T13:17:51.712Z
tags: 
editor: markdown
dateCreated: 2023-01-31T13:17:50.052Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Spring Boot JSON Processing with Jackson***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-json-processing-with-jackson)
{.links-list}



# Jacksonを使用したSpring Boot JSONの処理

JSON（JavaScript Object Notation）は、人間が簡単に読み書きできる軽量データ交換形式です。 Jacksonは、JSONを直列化および逆シリアル化する強力なJavaライブラリです。

この記事では、Jacksonを使用してJSONをJavaオブジェクトに、またはその逆に変換する方法について説明します。


## Mavenの依存関係

まず、pom.xmlファイルにJacksonの依存関係を追加する必要があります。

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.9.9</version>
</dependency>
```

## JSONをJavaオブジェクトに変換

ObjectMapperクラスのreadValue（）メソッドを使用して、JSON文字列をJavaオブジェクトに変換できます。

次のJSON文字列を考えてみましょう。

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

`readValue()` メソッドを使用して、この JSON 文字列を Java `Person` オブジェクトに変換できます。

```java
ObjectMapper mapper = new ObjectMapper();
String jsonString = "{\"name\":\"John Doe\",\"age\":30,\"address\":{\"street\":\"123 Main Street\",\"city \":\"New York\",\"state\":\"NY\",\"zip\":\"10001\"},\"phoneNumbers\":[{\"type\":\ "home\",\"number\":\"212 555-1234\"},{\"type\":\"work\",\"number\":\"646 555-4567\"}] } ";
Person person = mapper.readValue(jsonString, Person.class);
```

`readValue()` メソッドは、JSON 文字列とターゲット Java クラスの 2 つの引数を使用します。 `Person`クラスにはJSONデータに対応するフィールドが必要です。

```java
public class Person {
  private String name;
  private int age;
  private Address address;
  private List<PhoneNumber> phoneNumbers;
  
  // ゲッターとセッター
}
```

`Address`と`PhoneNumber`クラスは同様に定義されています。

```java
public class Address {
  private String street;
  private String city;
  private String state;
  private String zip;
  
  // ゲッターとセッター
}

public class PhoneNumber {
  private String type;
  private String number;
  
  // ゲッターとセッター
}
```

上記のコードを実行した後、 `person`オブジェクトは次のデータを持ちます。

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

List<PhoneNumber> phoneNumbers = new ArrayList <>（）;

PhoneNumber homePhoneNumber = new PhoneNumber();
homePhoneNumber.setType("home");
homePhoneNumber.setNumber("212 555-1234");
phoneNumbers.add（homePhoneNumber）;

PhoneNumber workPhoneNumber = new PhoneNumber();
workPhoneNumber.setType("work");
workPhoneNumber.setNumber("646 555-4567");
phoneNumbers.add（workPhoneNumber）;

person.setPhoneNumbers（phoneNumbers）;
```

## JavaオブジェクトをJSONに変換

ObjectMapperクラスのwriteValueAsString（）メソッドを使用して、JavaオブジェクトをJSON文字列に変換できます。

次のJava `Person`オブジェクトを考えてみましょう。

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

List<PhoneNumber> phoneNumbers = new ArrayList <>（）;

PhoneNumber homePhoneNumber = new PhoneNumber();
homePhoneNumber.setType("home");
homePhoneNumber.setNumber("212 555-1234");
phoneNumbers.add（homePhoneNumber）;

PhoneNumber workPhoneNumber = new PhoneNumber();
workPhoneNumber.setType("work");
workPhoneNumber.setNumber("646 555-4567");
phoneNumbers.add（workPhoneNumber）;

person.setPhoneNumbers（phoneNumbers）;
```

`writeValueAsString()` メソッドを使用して、この Java オブジェクトを JSON 文字列に変換できます。

```java
ObjectMapper mapper = new ObjectMapper();
String jsonString = mapper.writeValueAsString(person);
```

`writeValueAsString()` メソッドは `person` オブジェクトの JSON 文字列表現を返します。出力は次のJSON文字列です。

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

##結論

この記事では、Jacksonを使用してJSONをJavaオブジェクトに、またはその逆に変換する方法について説明しました。 JacksonはJavaでJSONデータを処理するための強力なライブラリです。