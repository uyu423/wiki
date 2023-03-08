---
title: 086: Kotlin on Android: Building Android Apps with Kotlin
description: 
published: true
date: 2023-02-15T12:18:07.835Z
tags: 
editor: markdown
dateCreated: 2023-02-15T12:17:59.349Z
---

- [086: Kotlin en Android: creación de aplicaciones de Android con Kotlin***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/086-kotlin-on-android-building-android-apps-with-kotlin)
{.links-list}
- [086：Android 上的 Kotlin：使用 Kotlin 构建 Android 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/086-kotlin-on-android-building-android-apps-with-kotlin)
{.links-list}
- [086: Android의 Kotlin: Kotlin으로 Android 앱 빌드***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/086-kotlin-on-android-building-android-apps-with-kotlin)
{.links-list}


# 086: Kotlin on Android: Building Android Apps with Kotlin

Kotlin is a powerful programming language that can be used to build Android apps. In this post, we will take a look at how to get started with Kotlin on Android.

## Installing Kotlin

To get started with Kotlin on Android, you first need to install the Kotlin plugin. You can do this from within Android Studio by going to File > Settings > Plugins and searching for the Kotlin plugin. Once you have installed the plugin, you will need to restart Android Studio.

Once Android Studio has restarted, you will be able to create a new Kotlin project. To do this, go to File > New > New Project and select the Kotlin option from the list of project types.

## Creating a Kotlin Project

Once you have installed the Kotlin plugin, you can create a new Kotlin project. To do this, go to File > New > New Project and select the Kotlin option from the list of project types.

When you create a new Kotlin project, you will be asked to specify the name and location of the project, as well as the project SDK. Once you have specified these details, click the Finish button to create the project.

## Creating a Kotlin File

Once you have created a Kotlin project, you can create a Kotlin file. To do this, go to File > New > Kotlin File/Class.

When you create a new Kotlin file, you will be asked to specify the name and location of the file. You will also be asked to specify the Kotlin file type. There are four Kotlin file types:

- Kotlin Class
- Kotlin File
- Kotlin Object
- Kotlin Interface

Once you have specified the name and location of the file, click the Finish button to create the file.

## Writing Kotlin Code

Now that you have created a Kotlin project and a Kotlin file, you are ready to start writing Kotlin code.

Kotlin code is written in files with the .kt extension. Kotlin files can contain one or more top-level declarations. A top-level declaration is a declaration that is not inside a class, object, or interface.

Kotlin has a rich set of features that make it a great choice for developing Android apps. Some of these features include:

- Null safety
- Extension functions
- Data classes
- Coroutines

In the next section, we will take a look at some of these features in more detail.

## Null Safety

One of the most important features of Kotlin is null safety. Null safety is a feature that prevents null pointer exceptions from occurring.

To make a variable null safe, you need to use the ? operator. For example, the following code will not compile because the name variable can be null:

```kotlin
var name: String = "John"
name = null
```

To make the code null safe, you need to use the ? operator:

```kotlin
var name: String? = "John"
name = null
```

Now the code will compile because the name variable can be null.

## Extension Functions

Another important feature of Kotlin is extension functions. Extension functions allow you to extend a class with new functionality without having to subclass it.

For example, suppose you have a class with an isEmpty() function that returns true if the class is empty and false if it is not. You can extend this class with a new isNotEmpty() function that returns the opposite of isEmpty():

```kotlin
fun isNotEmpty(): Boolean {
    return !isEmpty()
}
```

To use the new function, you simply need to call it on an instance of the class:

```kotlin
val list = ArrayList<String>()
list.isNotEmpty() // returns false
```

## Data Classes

Kotlin also has support for data classes. Data classes are classes that are designed to hold data. They are similar to JavaBeans, but they are much simpler to create and use.

To create a data class, you need to use the data keyword:

```kotlin
data class User(val name: String, val age: Int)
```

This code creates a data class with two properties: name and age. The properties are declared using the val keyword, which means they are read-only.

To create an instance of the data class, you simply need to call the constructor:

```kotlin
val user = User("John", 30)
```

To access the properties of the data class, you can use the dot notation:

```kotlin
user.name // returns "John"
user.age // returns 30
```

Data classes also have a number of useful functions, such as toString(), hashCode(), and equals():

```kotlin
user.toString() // returns "User(name=John, age=30)"
user.hashCode() // returns -1234
user.equals(other) // returns true if the two objects are equal
```

## Coroutines

Coroutines are a new feature in Kotlin that make it easier to write asynchronous code. Coroutines are similar to threads, but they are much lighter weight and they can be suspended without blocking a thread.

To use coroutines, you need to import the kotlinx.coroutines package:

```kotlin
import kotlinx.coroutines.*
```

Then, you can use the launch() function to launch a new coroutine:

```kotlin
GlobalScope.launch {
    // suspendable code
}
```

Inside the launch() function, you can write suspendable code. This code can be suspended without blocking a thread.

To suspend a coroutine, you can use the delay() function:

```kotlin
GlobalScope.launch {
    delay(1000) // suspend for 1 second
    // resume here
}
```

The delay() function takes a time argument in milliseconds. The coroutine will be resumed after the specified time has elapsed.

You can also use the yield() function to suspend a coroutine and allow other coroutines to run:

```kotlin
GlobalScope.launch {
    yield() // suspend and allow other coroutines to run
    // resume here
}
```

## Conclusion

In this post, we have looked at how to get started with Kotlin on Android. We have seen how to install the Kotlin plugin, create a Kotlin project, and write Kotlin code. We have also seen some of the features that make Kotlin a great choice for developing Android apps.