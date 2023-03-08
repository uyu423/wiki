---
title: 092: The IntelliJ IDEA in Kotlin: Developing Kotlin Code with the IntelliJ IDEA IDE
description: 
published: true
date: 2023-02-17T21:32:36.561Z
tags: 
editor: markdown
dateCreated: 2023-02-17T21:32:29.090Z
---

- [092: Kotlin의 IntelliJ IDEA: IntelliJ IDEA IDE로 Kotlin 코드 개발***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/092-the-intellij-idea-in-kotlin-developing-kotlin-code-with-the-intellij-idea-ide)
{.links-list}


# 092: The IntelliJ IDEA in Kotlin: Developing Kotlin Code with the IntelliJ IDEA IDE

Kotlin is a JVM language created by JetBrains, the makers of the IntelliJ IDEA IDE. Kotlin is a statically typed language that runs on the JVM and can be used for developing Android apps, server-side applications, and much more.

In this post, we'll take a look at how to develop Kotlin code using the IntelliJ IDEA IDE. We'll cover the following topics:

* Setting up the Kotlin plugin in IntelliJ IDEA
* Creating a Kotlin project in IntelliJ IDEA
* Writing Kotlin code in IntelliJ IDEA
* Running Kotlin code in IntelliJ IDEA

## Setting up the Kotlin plugin in IntelliJ IDEA

The Kotlin plugin is not bundled with IntelliJ IDEA by default. However, it's easy to install the Kotlin plugin.

To install the Kotlin plugin:

1. Open IntelliJ IDEA and go to _File > Settings_.
2. In the _Settings_ window, go to _Plugins_.
3. In the _Plugins_ window, click on the _Browse repositories_ button.
4. In the _Browse Repositories_ window, search for `kotlin`.
5. In the search results, select the _Kotlin_ plugin and click on the _Install_ button.
6. In the _Install Plugin_ window, click on the _Restart IntelliJ IDEA_ button.

After restarting IntelliJ IDEA, the Kotlin plugin will be installed and ready to use.

## Creating a Kotlin project in IntelliJ IDEA

Now that we have the Kotlin plugin installed, let's create a Kotlin project.

To create a Kotlin project:

1. Open IntelliJ IDEA and go to _File > New > Project_.
2. In the _New Project_ window, select _Kotlin > Kotlin/JVM_ and click on the _Next_ button.
3. In the _New Kotlin/JVM Project_ window, enter a _Project name_ and click on the _Finish_ button.

A new Kotlin project will be created with the following structure:

```
src/
    main/
        kotlin/
            Main.kt
    test/
        kotlin/
            MainTest.kt
```

## Writing Kotlin code in IntelliJ IDEA

Now that we have a Kotlin project, let's write some Kotlin code.

Open the `Main.kt` file and replace the contents with the following code:

```kotlin
fun main(args: Array<String>) {
    println("Hello, world!")
}
```

This code prints "Hello, world!" to the console.

To run this code:

1. Go to _Run > Run 'Main'_.
2. In the _Run/Debug Configurations_ window, click on the _Run_ button.

The code will be compiled and run, and the output will be displayed in the _Run_ window.

## Running Kotlin code in IntelliJ IDEA

We can also run Kotlin code from the IntelliJ IDEA _Run_ window.

To run Kotlin code from the _Run_ window:

1. Go to _Run > Run 'Main'_.
2. In the _Run/Debug Configurations_ window, click on the _Run_ button.
3. In the _Run_ window, type `println("Hello, world!")` and press _Enter_.

The code will be compiled and run, and the output will be displayed in the _Run_ window.

## Conclusion

In this post, we've seen how to develop Kotlin code using the IntelliJ IDEA IDE. We've covered how to install the Kotlin plugin, how to create a Kotlin project, how to write Kotlin code, and how to run Kotlin code.