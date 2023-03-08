---
title: 동적 프로그래밍을 위한 Java의 Reflection API 활용
description: 
published: true
date: 2023-03-05T17:32:52.413Z
tags: 
editor: markdown
dateCreated: 2023-03-05T17:32:45.137Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Leveraging Java's Reflection API for Dynamic Programming***English** document is available*](/en/Knowledge-base/Java/leveraging-java-s-reflection-api-for-dynamic-programming)
{.links-list}

동적 프로그래밍을 위한 Java의 Reflection API 활용

Java의 Reflection API는 개발자가 실행 중인 Java 프로그램의 동작을 검사하고 조작할 수 있는 강력한 도구입니다. 이 API를 사용하면 변화하는 요구 사항 및 런타임 조건에 적응할 수 있는 동적 애플리케이션을 만들 수 있습니다. 이 기사에서는 Java Reflection의 기본 사항, 핵심 개념 및 이를 사용하여 동적 애플리케이션을 구축하는 방법을 살펴봅니다.

### 자바 리플렉션이란?

리플렉션은 프로그램이 Java 개체의 런타임 동작을 검사하고 수정할 수 있도록 하는 Java의 기능입니다. 개발자가 동적 응용 프로그램을 만들 수 있는 강력하고 유연한 도구입니다. 리플렉션을 사용하면 런타임에 클래스의 구조, 해당 필드, 메서드 및 생성자를 검사할 수 있습니다. 이를 통해 개발자는 다음을 수행할 수 있습니다.

- 클래스의 새 객체를 동적으로 생성
- 동적으로 클래스의 필드 및 메서드에 액세스
- 런타임 시 클래스의 동작 수정

Java Reflection은 구조에 관계없이 모든 클래스에서 작동할 수 있는 일반 코드를 개발자가 작성할 수 있는 방법을 제공합니다. 이는 Reflection API가 클래스의 구조를 검사하고 컴파일 시 알 수 없는 경우에도 해당 필드, 메서드 및 생성자를 결정할 수 있기 때문입니다.

### 반사의 핵심 개념

#### 클래스 개체

Java의 클래스 개체는 런타임 시 클래스 또는 인터페이스를 나타냅니다. Java의 모든 개체에는 Class 개체에 대한 참조가 있습니다. 객체의 Class 객체에 대한 참조를 얻으려면 getClass() 메서드를 사용할 수 있습니다. 예를 들어:

```java
Object obj = new String("Hello World");
Class<? extends Object> clazz = obj.getClass();
```

#### 리플렉션 API

Java의 Reflection API는 java.lang.reflect 패키지에 포함되어 있습니다. 개발자가 런타임에 Java 프로그램의 동작을 검사하고 조작할 수 있도록 하는 여러 클래스와 인터페이스를 제공합니다. 주요 클래스 중 일부는 다음과 같습니다.

- 클래스: 런타임 시 클래스 또는 인터페이스를 나타냅니다.
- 필드: 클래스 또는 인터페이스의 필드를 나타냅니다.
- 메소드: 클래스 또는 인터페이스의 메소드를 나타냅니다.
- 생성자: 클래스의 생성자를 나타냅니다.

#### 필드 및 메소드 액세스

Java Reflection은 런타임 시 클래스의 필드 및 메서드에 액세스하는 방법을 제공합니다. Class 클래스의 getField() 및 getMethod() 메서드를 사용하여 Field 또는 Method 객체에 대한 참조를 얻을 수 있습니다. 예를 들어:

```java
class MyClass {
  private String name;
  public void setName(String name) {
    this.name = name;
  }
  public String getName() {
    return this.name;
  }
}

MyClass obj = new MyClass();
Class<? extends MyClass> clazz = obj.getClass();
Field field = clazz.getDeclaredField("name"); // Access the field "name"
Method method = clazz.getDeclaredMethod("setName", String.class); // Access the method "setName"
```

Field 또는 Method 객체에 대한 참조를 얻은 후에는 set() 및 get() 메서드를 사용하여 필드 값을 수정 또는 검색하거나 메서드를 호출할 수 있습니다. 예를 들어:

```java
field.setAccessible(true); // Set the field accessible
field.set(obj, "John Doe"); // Set the value of the field "name"
method.invoke(obj, "Jane Doe"); // Invoke the method "setName"
String name = (String) field.get(obj); // Get the value of the field "name"
```

#### 동적으로 개체 만들기

Java Reflection은 클래스의 객체를 동적으로 생성하는 방법을 제공합니다. Class 클래스의 newInstance() 메서드를 사용하여 클래스의 새 인스턴스를 만들 수 있습니다. 예를 들어:

```java
Class<MyClass> clazz = MyClass.class;
MyClass obj = clazz.newInstance();
```

컴파일 타임에 이름을 알 수 없는 클래스의 개체를 만들 수도 있습니다. 예를 들어:

```java
Class<?> clazz = Class.forName("com.example.MyClass");
Object obj = clazz.newInstance();
```

#### 클래스 동작 수정

Java Reflection은 런타임에 클래스의 동작을 수정하는 방법도 제공합니다. AccessibleObject 클래스의 setAccessible() 메서드를 사용하여 필드, 메서드 또는 생성자의 접근성 플래그를 설정할 수 있습니다. 예를 들어:

```java
class MyClass {
  private String name;
}

MyClass obj = new MyClass();
Class<? extends MyClass> clazz = obj.getClass();
Field field = clazz.getDeclaredField("name");
field.setAccessible(true); // Set the field accessible
```

### 리플렉션 사용의 이점

Java Reflection을 사용하면 변화하는 요구 사항과 런타임 조건에 적응할 수 있는 동적 애플리케이션을 만들 수 있습니다. Reflection을 사용하면 얻을 수 있는 몇 가지 이점은 다음과 같습니다.

- 구조에 관계없이 모든 클래스에서 작동할 수 있는 일반 코드 생성
- 비공개 또는 보호되는 클래스의 필드 및 메서드에 액세스
- 컴파일 타임에 클래스 이름을 알 수 없는 경우에도 동적으로 클래스의 객체 생성
- 런타임 시 클래스의 동작 수정

### 결론

이 기사에서는 Java Reflection의 기본 사항, 핵심 개념 및 이를 사용하여 동적 애플리케이션을 구축하는 방법을 살펴보았습니다. Reflection을 사용하여 클래스의 필드와 메서드에 액세스하고 클래스의 개체를 동적으로 생성하고 런타임에 클래스의 동작을 수정하는 방법을 살펴보았습니다. Reflection을 사용하여 개발자는 사용자의 변화하는 요구 사항을 충족할 수 있는 유연하고 적응 가능한 응용 프로그램을 만들 수 있습니다.

### 외부 리소스

자세한 내용은 Java Reflection에 대한 몇 가지 외부 리소스를 참조하세요.

- [자바 리플렉션 튜토리얼](https://www.baeldung.com/java-reflection)
- [오라클 자바 리플렉션 가이드](https://docs.oracle.com/javase/tutorial/reflect/)
- [Java Reflection Cheat Sheet](https://www.owasp.org/index.php/Java_Reflection_Cheat_Sheet)