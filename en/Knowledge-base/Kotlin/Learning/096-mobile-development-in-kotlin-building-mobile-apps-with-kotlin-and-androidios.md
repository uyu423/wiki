---
title: 096: Mobile Development in Kotlin: Building Mobile Apps with Kotlin and Android/iOS
description: 
published: true
date: 2023-02-14T12:18:30.920Z
tags: 
editor: markdown
dateCreated: 2023-02-14T12:18:29.047Z
---

- [096: Desarrollo móvil en Kotlin: creación de aplicaciones móviles con Kotlin y Android/iOS***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/096-mobile-development-in-kotlin-building-mobile-apps-with-kotlin-and-androidios)
{.links-list}
- [096：Kotlin 中的移动开发：使用 Kotlin 和 Android/iOS 构建移动应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/096-mobile-development-in-kotlin-building-mobile-apps-with-kotlin-and-androidios)
{.links-list}
- [096: Kotlin으로 모바일 개발: Kotlin 및 Android/iOS로 모바일 앱 빌드***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/096-mobile-development-in-kotlin-building-mobile-apps-with-kotlin-and-androidios)
{.links-list}


# 096: Mobile Development in Kotlin: Building Mobile Apps with Kotlin and Android/iOS

Kotlin is a statically typed programming language that runs on the Java Virtual Machine and can also be compiled to JavaScript source code. Kotlin is developed by JetBrains, the company behind the IntelliJ IDEA Java IDE.

Kotlin was designed to be an improved version of Java, and it offers a number of features that Java does not. Kotlin is fully interoperable with Java, so it can be used to develop Android apps.

In this post, we'll take a look at how to get started with Kotlin and Android development. We'll create a simple "Hello, World!" app and then run it on an Android device.

## Getting Started

To get started, you'll need to install the Kotlin plugin for IntelliJ IDEA. You can do this from within the IDE by going to Preferences > Plugins and searching for "Kotlin."

Once the Kotlin plugin is installed, you can create a new Kotlin project by going to File > New > Project and selecting "Kotlin/JVM" from the list of project templates.

## Creating a Kotlin Project

Once you've created a Kotlin project, you can create a new Kotlin file by going to File > New > Kotlin File/Class.

Let's create a file called "HelloWorld.kt" in the src/ directory of our project. We'll start by adding a main function to our file:

```kotlin
fun main(args: Array<String>) {
    println("Hello, World!")
}
```

This function prints the string "Hello, World!" to the console.

## Running the App

To run our Kotlin app, we'll need to create a run configuration. We can do this by going to Run > Edit Configurations and clicking the "+" button.

From the list of run configuration types, select "Kotlin/JVM." We'll name our configuration "Hello, World!" and set the main class to "HelloWorldKt."

Finally, we'll need to select a device to run our app on. We can do this by going to Run > Edit Configurations and selecting our "Hello, World!" configuration. Under the "Device" drop-down, select the device you want to use.

Now, we're ready to run our Kotlin app on our Android device!