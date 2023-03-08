---
title: 090: Annotation Processing in Kotlin: Generating Code at Compile-Time with Annotation Processing
description: 
published: true
date: 2023-02-16T05:18:14.392Z
tags: 
editor: markdown
dateCreated: 2023-02-16T05:18:12.414Z
---

- [090: Procesamiento de anotaciones en Kotlin: generación de código en tiempo de compilación con procesamiento de anotaciones***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/090-annotation-processing-in-kotlin-generating-code-at-compile-time-with-annotation-processing)
{.links-list}
- [090：Kotlin 中的注释处理：在编译时使用注释处理生成代码***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/090-annotation-processing-in-kotlin-generating-code-at-compile-time-with-annotation-processing)
{.links-list}
- [090: Kotlin의 주석 처리: 주석 처리를 통해 컴파일 타임에 코드 생성***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/090-annotation-processing-in-kotlin-generating-code-at-compile-time-with-annotation-processing)
{.links-list}


# Annotation Processing in Kotlin: Generating Code at Compile-Time with Annotation Processing

Annotation processing is a powerful tool for code generation in Kotlin. By using annotation processors, we can generate code at compile-time, which can be used in our Kotlin applications.

In this post, we'll take a look at how to use annotation processors to generate code in Kotlin. We'll explore what annotation processors are and how they work. We'll also look at how to write our own annotation processors and use them in our Kotlin applications.

## What are Annotation Processors?

Annotation processors are programs that run during the compilation of our code and generate code based on the annotations present in our code. We can use annotation processors to generate boilerplate code, to validate our code, or to perform any other task that can be automated.

Annotation processors are written in Kotlin or Java and are run using the kotlinc compiler. We can write our own annotation processors or use ones that are provided by third-party libraries.

## How do Annotation Processors Work?

Annotation processors are run by the kotlinc compiler when it compiles our code. The kotlinc compiler first compiles the code without running the annotation processors. This allows the annotation processors to access the source code and the compiled bytecode.

After the initial compilation, the kotlinc compiler runs the annotation processors. The annotation processors can then generate code, which is compiled and added to the final output of the compilation.

## Writing our own Annotation Processor

Let's write our own annotation processor to generate boilerplate code. We'll start by creating a new Kotlin project in IntelliJ IDEA.

![Create Kotlin Project](https://i.imgur.com/p0lC5Nq.png)

We'll name our project "Annotation Processor" and we'll leave the default settings for the project structure.

![Project Structure](https://i.imgur.com/gY0CWt6.png)

Next, we'll create a new Kotlin file in the `src/main/kotlin` directory. We'll name this file "GenerateBoilerplate.kt".

In this file, we'll write our annotation processor. We'll start by defining a new annotation called `@GenerateBoilerplate`.

```kotlin
@Retention(AnnotationRetention.SOURCE)
@Target(AnnotationTarget.CLASS)
annotation class GenerateBoilerplate
```

This annotation can be used on classes. It will be retained in the source code, but it will not be present in the compiled bytecode.

Next, we'll write a function to generate the boilerplate code for a class annotated with `@GenerateBoilerplate`. This function will take a `Class<*>` as a parameter and will return a `String` containing the generated code.

```kotlin
fun generateBoilerplate(clazz: Class<*>): String {
    val className = clazz.simpleName
    return "class $className {\n}\n"
}
```

This function will simply generate a `class` declaration with the name of the annotated class.

Now that we've written our function to generate the boilerplate code, we'll write our annotation processor. We'll start by defining a new class called `GenerateBoilerplateProcessor`. This class will extend the `AbstractProcessor` class.

```kotlin
class GenerateBoilerplateProcessor : AbstractProcessor() {
}
```

Next, we'll override the `process` function. This function will be called by the kotlinc compiler when it runs our annotation processor.

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
}
```

This function takes two parameters. The first parameter is a set of annotations that the processor should process. The second parameter is the environment in which the processor is being run.

We can use the `roundEnv` parameter to access the annotated elements in our code. We'll use the `getElementsAnnotatedWith` function to get a list of elements annotated with our `@GenerateBoilerplate` annotation.

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
    val annotatedElements = roundEnv.getElementsAnnotatedWith(GenerateBoilerplate::class.java)
}
```

We can then iterate over this list and generate the boilerplate code for each annotated element.

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
    val annotatedElements = roundEnv.getElementsAnnotatedWith(GenerateBoilerplate::class.java)

    for (element in annotatedElements) {
        val clazz = element as TypeElement
        val generatedCode = generateBoilerplate(clazz)
    }
}
```

Finally, we'll write the generated code to a file. We'll use the `Filer` class to create a new file. The `Filer` class is part of the `javax.annotation.processing` package.

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
    val annotatedElements = roundEnv.getElementsAnnotatedWith(GenerateBoilerplate::class.java)

    for (element in annotatedElements) {
        val clazz = element as TypeElement
        val generatedCode = generateBoilerplate(clazz)

        val filer = processingEnv.filer
        val file = filer.createSourceFile(clazz.qualifiedName.toString())
    }
}
```

We'll use the `createSourceFile` function to create a new file. We'll use the fully qualified name of the annotated element as the name of the file.

We can then write the generated code to the file using the `Writer` class.

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
    val annotatedElements = roundEnv.getElementsAnnotatedWith(GenerateBoilerplate::class.java)

    for (element in annotatedElements) {
        val clazz = element as TypeElement
        val generatedCode = generateBoilerplate(clazz)

        val filer = processingEnv.filer
        val file = filer.createSourceFile(clazz.qualifiedName.toString())

        val writer = file.openWriter()
        writer.write(generatedCode)
        writer.close()
    }
}
```

Now that we've written our annotation processor, we can use it in our Kotlin code. We'll create a new Kotlin file in the `src/main/kotlin` directory. We'll name this file "Main.kt".

In this file, we'll annotate a class with our `@GenerateBoilerplate` annotation.

```kotlin
@GenerateBoilerplate
class Foo
```

When we compile this code, the kotlinc compiler will run our annotation processor. Our annotation processor will generate the following code:

```kotlin
class Foo {
}
```

## Using Annotation Processors in our Kotlin Applications

Now that we've seen how to write our own annotation processors, let's take a look at how to use them in our Kotlin applications.

We'll start by adding the `kotlin-annotation-processing` plugin to our `build.gradle` file.

```groovy
plugins {
    id "org.jetbrains.kotlin.plugin.allopen" version "1.3.72"
}
```

We can then configure the `kotlin-annotation-processing` plugin to run our annotation processor. We'll add the following configuration to our `build.gradle` file.

```groovy
kotlinAnnotationProcessing {
    processors = [
            "com.example.GenerateBoilerplateProcessor"
    ]
}
```

We can now use our annotation processor in our Kotlin code. We'll create a new Kotlin file in the `src/main/kotlin` directory. We'll name this file "Main.kt".

In this file, we'll annotate a class with our `@GenerateBoilerplate` annotation.

```kotlin
@GenerateBoilerplate
class Foo
```

When we compile this code, the kotlinc compiler will run our annotation processor. Our annotation processor will generate the following code:

```kotlin
class Foo {
}
```

## Conclusion

In this post, we've seen how to use annotation processors to generate code in Kotlin. We've looked at how to write our own annotation processors and how to use them in our Kotlin applications.