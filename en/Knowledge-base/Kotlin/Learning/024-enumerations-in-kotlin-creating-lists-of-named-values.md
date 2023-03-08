---
title: 024: Enumerations in Kotlin: Creating Lists of Named Values
description: 
published: true
date: 2023-02-16T07:32:59.510Z
tags: 
editor: markdown
dateCreated: 2023-02-16T07:32:57.683Z
---

- [024: Enumeraciones en Kotlin: creación de listas de valores con nombre***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/024-enumerations-in-kotlin-creating-lists-of-named-values)
{.links-list}
- [024：Kotlin 中的枚举：创建命名值列表***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/024-enumerations-in-kotlin-creating-lists-of-named-values)
{.links-list}
- [024: Kotlin의 열거형: 명명된 값 목록 만들기***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/024-enumerations-in-kotlin-creating-lists-of-named-values)
{.links-list}


# Enumerations in Kotlin: Creating Lists of Named Values

Kotlin's enumerations are a powerful tool for creating lists of named values. By using enumerations, you can create type-safe, immutable lists of values that can be used in your code.

Enumerations are declared using the ```enum``` keyword. Each value in an enumeration is called an ```enum constant```. Enum constants are separated by commas.

Here is a simple example of an enumeration in Kotlin:

```kotlin
enum class Color {
    RED,
    GREEN,
    BLUE
}
```

In this example, we have created an enumeration of colors. The ```enum``` keyword is used to declare the enumeration, and the ```class``` keyword is used to create the enum constants.

Enumerations are immutable, meaning that once they are created, they cannot be changed. This makes them safe to use in your code.

Enumerations can be used in a number of ways in Kotlin. In this post, we will take a look at some of the ways you can use enumerations in your code.

## Using Enumerations

Enumerations can be used in a number of ways in Kotlin. In this section, we will take a look at some of the ways you can use enumerations in your code.

### Switch Statements

Enumerations can be used in ```when``` statements in Kotlin. ```When``` statements are a type of ```switch``` statement that allows you to match a value against a list of possible values.

Here is an example of a ```when``` statement that uses an enumeration:

```kotlin
fun getColor(color: Color): String {
    when (color) {
        Color.RED -> return "Red"
        Color.GREEN -> return "Green"
        Color.BLUE -> return "Blue"
    }
}
```

In this example, we have created a function that takes a ```Color``` enum as an argument. We then use a ```when``` statement to match the ```color``` against the list of possible values.

If the ```color``` is ```RED```, the function will return the string ```"Red"```. If the ```color``` is ```GREEN```, the function will return the string ```"Green"```. If the ```color``` is ```BLUE```, the function will return the string ```"Blue"```.

### Iterating Over Enumerations

Enumerations can be iterated over using the ```for``` loop. The ```for``` loop will iterate over all of the enum constants in the enumeration.

Here is an example of how to iterate over an enumeration:

```kotlin
for (color in Color.values()) {
    println(color)
}
```

In this example, we use the ```for``` loop to iterate over the ```Color``` enumeration. We print each value of the enumeration to the console.

This code will print the following to the console:

```
RED
GREEN
BLUE
```

### Checking Enum Values

You can check if a particular value is contained within an enumeration using the ```in``` keyword.

Here is an example of how to check if a value is contained in an enumeration:

```kotlin
if (Color.RED in Color.values()) {
    println("Color.RED is in the Color enumeration")
}
```

In this example, we use the ```in``` keyword to check if the ```Color.RED``` enum constant is contained in the ```Color``` enumeration.

If the ```Color.RED``` enum constant is contained in the ```Color``` enumeration, the code will print the following to the console:

```
Color.RED is in the Color enumeration
```

### Getting Enum Values by Name

You can get an enum constant by its name using the ```valueOf()``` function.

Here is an example of how to get an enum constant by its name:

```kotlin
val color: Color = Color.valueOf("RED")
```

In this example, we use the ```valueOf()``` function to get the ```Color.RED``` enum constant from the ```Color``` enumeration.

### Creating Your Own Enumerations

In addition to the standard Kotlin enumerations, you can also create your own custom enumerations.

Here is an example of how to create a custom enumeration:

```kotlin
enum class MyEnum {
    FIRST_VALUE,
    SECOND_VALUE
}
```

In this example, we have created a custom enumeration called ```MyEnum```. This enumeration contains two values: ```FIRST_VALUE``` and ```SECOND_VALUE```.

You can also create enumerations with custom properties and methods.

Here is an example of how to create an enumeration with a custom property:

```kotlin
enum class MyEnum {
    FIRST_VALUE {
        override val property: Int
            get() = 1
    },
    SECOND_VALUE {
        override val property: Int
            get() = 2
    }

    abstract val property: Int
}
```

In this example, we have created an enumeration with a custom property called ```property```. This property is an ```abstract``` property that must be overridden by each enum constant.

In this example, we have overridden the ```property``` property for the ```FIRST_VALUE``` and ```SECOND_VALUE``` enum constants.

You can also create enumerations with custom methods.

Here is an example of how to create an enumeration with a custom method:

```kotlin
enum class MyEnum {
    FIRST_VALUE {
        override fun method(): String {
            return "First Value"
        }
    },
    SECOND_VALUE {
        override fun method(): String {
            return "Second Value"
        }
    }

    abstract fun method(): String
}
```

In this example, we have created an enumeration with a custom method called ```method()```. This method is an ```abstract``` method that must be overridden by each enum constant.

In this example, we have overridden the ```method()``` method for the ```FIRST_VALUE``` and ```SECOND_VALUE``` enum constants.

Enumerations are a powerful tool for creating lists of named values in Kotlin. By using enumerations, you can create type-safe, immutable lists of values that can be used in your code.