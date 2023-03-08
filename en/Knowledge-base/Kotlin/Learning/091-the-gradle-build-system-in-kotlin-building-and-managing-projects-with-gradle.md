---
title: 091: The Gradle Build System in Kotlin: Building and Managing Projects with Gradle
description: 
published: true
date: 2023-02-17T21:06:41.386Z
tags: 
editor: markdown
dateCreated: 2023-02-17T21:06:34.669Z
---

- [091: Kotlin의 Gradle 빌드 시스템: Gradle로 프로젝트 빌드 및 관리***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/091-the-gradle-build-system-in-kotlin-building-and-managing-projects-with-gradle)
{.links-list}


# 091: The Gradle Build System in Kotlin: Building and Managing Projects with Gradle

Gradle is a build system written in Kotlin that can build and manage projects of any size. It is an open source project that is actively maintained by a community of developers.

## Why use Gradle?

There are many reasons to use Gradle as your build system. Gradle is designed to be flexible and extensible. It has a rich plugin ecosystem that allows you to add new functionality to your build. Gradle is also much faster than other build systems, such as Apache Maven.

## Getting Started

To get started with Gradle, you need to create a `build.gradle` file in the root directory of your project. This file defines the build configuration for your project.

```groovy
apply plugin: 'java'

repositories {
    jcenter()
}

dependencies {
    compile group: 'org.apache.commons', name: 'commons-lang3', version: '3.5'
}
```

The `apply plugin: 'java'` line applies the Java plugin to your project. This plugin adds support for compiling Java code and packaging it into JAR files.

The `repositories` block defines where Gradle should look for dependencies. In this example, we are using the JCenter repository.

The `dependencies` block defines the dependencies for our project. We are depending on the Apache Commons Lang library.

To build our project, we can run the `gradle build` command. This will compile our Java code and package it into a JAR file. The JAR file will be placed in the `build/libs` directory.

## Wrapper

Gradle provides a wrapper that allows you to run Gradle without installing it on your system. The wrapper is a Gradle script that is packaged with your project. To use the wrapper, you need to add the following to your `build.gradle` file:

```groovy
apply plugin: 'java'

task wrapper(type: Wrapper) {
    gradleVersion = '2.9'
}
```

The `wrapper` task will generate a Gradle wrapper script (`gradlew`) and a properties file (`gradle/wrapper/gradle-wrapper.properties`). These files should be added to your version control system.

To build your project using the wrapper, you can run the `gradlew build` command.

## Tasks

Gradle tasks are used to perform actions, such as compiling code, running tests, or packaging applications. Tasks have a name and a type. The name of a task is used to identify it and the type defines the actions that the task will perform.

In the following example, we have a task named `compile` of type `JavaCompile`. This task will compile the Java code in the `src/main/java` directory.

```groovy
task compile(type: JavaCompile) {
    source = sourceSets.main.java
    classpath = configurations.compile
}
```

Tasks can also depend on other tasks. In the following example, the `compile` task depends on the `classes` task. This means that the `classes` task will be executed before the `compile` task.

```groovy
task compile(type: JavaCompile) {
    dependsOn 'classes'
    source = sourceSets.main.java
    classpath = configurations.compile
}
```

## Plugins

Gradle plugins are used to extend the functionality of Gradle. There are many plugins available for different languages and tools. In the following example, we are using the `java` plugin to add support for compiling Java code.

```groovy
apply plugin: 'java'

repositories {
    jcenter()
}

dependencies {
    compile group: 'org.apache.commons', name: 'commons-lang3', version: '3.5'
}
```

To apply a plugin, we use the `apply plugin: 'name'` syntax. In the example above, we are applying the `java` plugin.

## Conclusion

In this post, we have covered the basics of using Gradle to build and manage projects. Gradle is a powerful build system that is fast, flexible, and extensible. It has a rich plugin ecosystem that allows you to add new functionality to your build.