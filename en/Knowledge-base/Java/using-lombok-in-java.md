---
title: Using Lombok in Java
description: 
published: true
date: 2023-01-31T09:05:39.262Z
tags: 
editor: markdown
dateCreated: 2023-01-31T09:05:35.711Z
---

- [자바에서 롬복 사용하기***Korean** version of this document is available*](/ko/Knowledge-base/Java/using-lombok-in-java)
{.links-list}
- [Java でロンボクを使用する***Japanese** version of this document is available*](/ja/Knowledge-base/Java/using-lombok-in-java)
{.links-list}
- [在 Java 中使用龙目岛***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Java/using-lombok-in-java)
{.links-list}




# Using Lombok in Java

Lombok is a library that can be used to reduce boilerplate code in Java. It is used to automatically generate getters, setters, toString, hashCode, and equals methods, as well as constructors. Lombok is open source and available under the MIT license.

## Installation

Lombok can be installed as a plugin in your IDE or added to your project build path.

### IDE Plugins

#### Eclipse

There is a Lombok plugin available for Eclipse. To install it, start Eclipse and go to Help > Eclipse Marketplace. Search for Lombok and install the plugin.

#### IntelliJ IDEA

There is a Lombok plugin available for IntelliJ IDEA. To install it, start IntelliJ IDEA and go to File > Settings. In the settings window, go to Plugins and click on Browse repositories. Search for Lombok and install the plugin.

### Build Path

If you are using Lombok in a project that will be built with Maven, you can add Lombok to the project build path by adding the following dependency to the pom.xml file:

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.16.20</version>
    <scope>provided</scope>
</dependency>
```

If you are using Lombok in a project that will be built with Gradle, you can add Lombok to the project build path by adding the following dependency to the build.gradle file:

```groovy
dependencies {
    compileOnly 'org.projectlombok:lombok:1.16.20'
}
```

## Usage

To use Lombok in your Java code, you need to annotate the fields that you want to generate getters, setters, and constructors for. For example:

```java
import lombok.Data;

@Data
public class Person {
    private String name;
    private int age;
}
```

The @Data annotation will generate getters, setters, and constructors for all fields in the Person class.

If you only want to generate getters and setters for a field, you can use the @Getter and @Setter annotations:

```java
import lombok.Getter;
import lombok.Setter;

public class Person {
    @Getter
    @Setter
    private String name;

    private int age;
}
```

If you only want to generate a constructor for a class, you can use the @RequiredArgsConstructor annotation:

```java
import lombok.RequiredArgsConstructor;

@RequiredArgsConstructor
public class Person {
    private final String name;
    private final int age;
}
```

The @RequiredArgsConstructor annotation will generate a constructor with parameters for all fields that are marked as final or that have the @NonNull annotation.

If you want to generate a toString method for a class, you can use the @ToString annotation:

```java
import lombok.ToString;

@ToString
public class Person {
    private String name;
    private int age;
}
```

If you want to generate a hashCode method for a class, you can use the @HashCode annotation:

```java
import lombok.HashCode;

@HashCode
public class Person {
    private String name;
    private int age;
}
```

If you want to generate an equals method for a class, you can use the @EqualsAndHashCode annotation:

```java
import lombok.EqualsAndHashCode;

@EqualsAndHashCode
public class Person {
    private String name;
    private int age;
}
```

## Pros and Cons

Lombok is a very useful tool that can help to reduce boilerplate code in Java. However, there are some potential drawbacks to using Lombok.

First, Lombok generates code that is not visible in the source code. This can make it difficult to debug problems that arise from the generated code.

Second, Lombok can make code less readable. For example, the @Data annotation will generate a lot of code, which can make the source code more difficult to understand.

Third, Lombok can make it difficult to use certain Java tools, such as code coverage tools. This is because the Lombok generated code is not visible in the source code.

Fourth, Lombok can make it difficult to migrate code to a new version of Java. This is because the Lombok generated code is specific to the version of Java that it was compiled with.

Finally, Lombok is not widely used. This means that there is less documentation and support available for Lombok.

## Conclusion

Lombok is a library that can be used to reduce boilerplate code in Java. It is used to automatically generate getters, setters, toString, hashCode, and equals methods, as well as constructors. Lombok is open source and available under the MIT license.

Lombok is a very useful tool that can help to reduce boilerplate code in Java. However, there are some potential drawbacks to using Lombok. First, Lombok generates code that is not visible in the source code. This can make it difficult to debug problems that arise from the generated code. Second, Lombok can make code less readable. For example, the @Data annotation will generate a lot of code, which can make the source code more difficult to understand. Third, Lombok can make it difficult to use certain Java tools, such as code coverage tools. This is because the Lombok generated code is not visible in the source code. Fourth, Lombok can make it difficult to migrate code to a new version of Java. This is because the Lombok generated code is specific to the version of Java that it was compiled with. Finally, Lombok is not widely used. This means that there is less documentation and support available for Lombok.