---
title: 021: Annotation Processing in Kotlin: Generating Code at Compile Time
description: 
published: true
date: 2023-02-01T16:44:23.948Z
tags: 
editor: markdown
dateCreated: 2023-02-01T16:44:19.776Z
---

- [021: Procesamiento de anotaciones en Kotlin: generación de código en tiempo de compilación***Spanish** version of this document is available*](/es/Knowledge-base/Kotlin/Learning/021-annotation-processing-in-kotlin-generating-code-at-compile-time)
{.links-list}
- [021: Kotlin의 주석 처리: 컴파일 시 코드 생성***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/021-annotation-processing-in-kotlin-generating-code-at-compile-time)
{.links-list}
- [021：Kotlin 中的注释处理：在编译时生成代码***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/021-annotation-processing-in-kotlin-generating-code-at-compile-time)
{.links-list}


# 021: Annotation Processing in Kotlin: Generating Code at Compile Time

Kotlin is a statically typed programming language that runs on the JVM. It is fully interoperable with Java and can be used to develop Android apps. Kotlin also has excellent support for annotation processing.

Annotation processing is a way to generate code at compile time. It is often used to create code that is not easily expressible in the source code of the programming language. For example, annotation processing can be used to generate code for data binding, to create Android Parcelables, or to generate code for Dagger 2.

In this article, we will look at how to use annotation processing in Kotlin to generate code for a simple data binding library. We will also look at how to use the kotlin-apt plugin to do annotation processing.

## What is Annotation Processing?

Annotation processing is a way to generate code at compile time. Annotation processors are programs that read the source code of a program and generate code based on the annotations present in the source code.

Annotations are a way to add metadata to a program. In Kotlin, annotations are added to a program using the `@` symbol. For example, the `@Override` annotation can be used to annotate a method that overrides a method in a superclass.

 Annotations can also be used to add metadata to a class. In Kotlin, a class can be annotated with the `@Deprecated` annotation to indicate that the class is deprecated and should not be used.

Annotations can also be used to add metadata to a package. In Kotlin, a package can be annotated with the `@file:JvmName` annotation to indicate that the package should be compiled to a Java class with the given name.

Annotations can also be used to add metadata to a file. In Kotlin, a file can be annotated with the `@file:Suppress("unused")` annotation to indicate that the compiler should not generate warnings for unused variables in the file.

## How to Use Annotation Processing in Kotlin

Annotation processing is a way to generate code at compile time. In Kotlin, annotation processing is done using the kotlin-apt plugin. The kotlin-apt plugin is a Kotlin compiler plugin that adds support for annotation processing.

To use the kotlin-apt plugin, you need to add the following to your `build.gradle` file:

```groovy
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
        classpath "com.google.auto.service:auto-service:1.0-rc4"
    }
}

apply plugin: 'kotlin-apt'

dependencies {
    apt "com.google.auto.service:auto-service:1.0-rc4"
}
```

The kotlin-apt plugin adds an `apt` configuration to the `build.gradle` file. The `apt` configuration is used to configure the annotation processors that will be used. In the example above, the `auto-service` annotation processor is configured.

The `auto-service` annotation processor is used to generate code for the `@AutoService` annotation. The `@AutoService` annotation is used to annotate a class that should be registered with an `auto-service` provider.

The `auto-service` provider is a service that provides a list of classes that have been annotated with the `@AutoService` annotation. The `auto-service` provider can be used to generate code for a service provider interface (SPI).

In the example above, the `@AutoService` annotation is used to annotate a class that should be registered with the `auto-service` provider. The `auto-service` provider will generate code for the `com.google.auto.service.AutoService` interface.

The `com.google.auto.service.AutoService` interface is an SPI that is used to register classes with the `auto-service` provider. The `auto-service` provider will use the `com.google.auto.service.AutoService` interface to generate code for the `META-INF/services/` file.

The `META-INF/services/` file is used to store a list of classes that have been registered with the `auto-service` provider. The `META-INF/services/` file is used by the `java.util.ServiceLoader` to load classes from a service provider.

In the example above, the `META-INF/services/` file will contain the following:

```
com.google.auto.service.AutoService
com.example.MyClass
```

The `java.util.ServiceLoader` will use the `META-INF/services/` file to load the `com.example.MyClass` class. The `com.example.MyClass` class will be registered with the `auto-service` provider.

The `auto-service` provider will generate code for the `com.google.auto.service.AutoService` interface. The `com.google.auto.service.AutoService` interface is used to register classes with the `auto-service` provider.

In the example above, the `com.google.auto.service.AutoService` interface is used to register the `com.example.MyClass` class with the `auto-service` provider. The `auto-service` provider will generate code for the `META-INF/services/` file.

The `META-INF/services/` file is used to store a list of classes that have been registered with the `auto-service` provider. The `META-INF/services/` file is used by the `java.util.ServiceLoader` to load classes from a service provider.

In the example above, the `META-INF/services/` file will contain the following:

```
com.google.auto.service.AutoService
com.example.MyClass
```

The `java.util.ServiceLoader` will use the `META-INF/services/` file to load the `com.example.MyClass` class. The `com.example.MyClass` class will be registered with the `auto-service` provider.

## Conclusion

Annotation processing is a way to generate code at compile time. In Kotlin, annotation processing is done using the kotlin-apt plugin. The kotlin-apt plugin is a Kotlin compiler plugin that adds support for annotation processing.

The kotlin-apt plugin adds an `apt` configuration to the `build.gradle` file. The `apt` configuration is used to configure the annotation processors that will be used. In the example above, the `auto-service` annotation processor is configured.

The `auto-service` annotation processor is used to generate code for the `@AutoService` annotation. The `@AutoService` annotation is used to annotate a class that should be registered with an `auto-service` provider.

The `auto-service` provider is a service that provides a list of classes that have been annotated with the `@AutoService` annotation. The `auto-service` provider can be used to generate code for a service provider interface (SPI).

In the example above, the `@AutoService` annotation is used to annotate a class that should be registered with the `auto-service` provider. The `auto-service` provider will generate code for the `com.google.auto.service.AutoService` interface.

The `com.google.auto.service.AutoService` interface is an SPI that is used to register classes with the `auto-service` provider. The `auto-service` provider will use the `com.google.auto.service.AutoService` interface to generate code for the `META-INF/services/` file.

The `META-INF/services/` file is used to store a list of classes that have been registered with the `auto-service` provider. The `META-INF/services/` file is used by the `java.util.ServiceLoader` to load classes from a service provider.

In the example above, the `META-INF/services/` file will contain the following:

```
com.google.auto.service.AutoService
com.example.MyClass
```

The `java.util.ServiceLoader` will use the `META-INF/services/` file to load the `com.example.MyClass` class. The `com.example.MyClass` class will be registered with the `auto-service` provider.

The `auto-service` provider will generate code for the `com.google.auto.service.AutoService` interface. The `com.google.auto.service.AutoService` interface is used to register classes with the `auto-service` provider.

In the example above, the `com.google.auto.service.AutoService` interface is used to register the `com.example.MyClass` class with the `auto-service` provider. The `auto-service` provider will generate code for the `META-INF/services/` file.

The `META-INF/services/` file is used to store a list of classes that have been registered with the `auto-service` provider. The `META-INF/services/` file is used by the `java.util.ServiceLoader` to load classes from a service provider.

In the example above, the `META-INF/services/` file will contain the following:

```
com.google.auto.service.AutoService
com.example.MyClass
```

The `java.util.ServiceLoader` will use the `META-INF/services/` file to load the `com.example.MyClass` class. The `com.example.MyClass` class will be registered with the `auto-service` provider.