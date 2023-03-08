---
title: pom.xml
description: 
published: true
date: 2023-02-17T18:00:16.338Z
tags: english, java, maven, springboot
editor: markdown
dateCreated: 2022-12-24T19:31:23.956Z
---

- [pom.xml***Korean** version of this document is available*](/ko/dev/Maven/overview-maven-pom-xml)
{.links-list}

## Detail about the structure of maven pom.xml

- Maven is a build automation tool used primarily for Java projects. It helps manage the build process, dependencies, and documentation of a project.
- The `pom.xml` file is the core of a project's configuration in Maven. It is a XML file that contains information about the project and configuration details used by Maven to build the project.
- Here is a summary of the main elements that can be included in a `pom.xml` file:
  - `project` element: This element is the root element of the `pom.xml` file. It contains information about the project, such as the group id, artifact id, and version.
  - `modelVersion` element: This element specifies the version of the POM model being used.
  - `groupId` element: This element specifies the unique identifier of the group that the project belongs to.
  - `artifactId` element: This element specifies the unique identifier of the project.
  - `version` element: This element specifies the version of the project.
  - `packaging` element: This element specifies the package type of the project, such as `jar`, `war`, or `ear`.
  - `name` element: This element specifies the name of the project.
  - `description` element: This element provides a description of the project.
  - `url` element: This element specifies the URL of the project's homepage.
  - `prerequisites` element: This element specifies any required prerequisites for building the project.
  - `issueManagement` element: This element specifies the URL and system used for managing issues for the project.
  - `ciManagement` element: This element specifies the URL and system used for continuous integration for the project.
  - `inceptionYear` element: This element specifies the year the project was created.
  - `licenses` element: This element specifies the licenses under which the project is distributed.
  - `developers` element: This element specifies the developers who have contributed to the project.
  - `contributors` element: This element specifies the contributors to the project.
  - `mailingLists` element: This element specifies the mailing lists for the project.
  - `scm` element: This element specifies the source control management system and connection information for the project.
  - `organization` element: This element specifies the organization responsible for the project.
  - `build` element: This element specifies the build settings for the project, such as the final name of the built artifact, the directory for compiled source code, and the plugins to use.
  - `profiles` element: This element specifies different build profiles that can be activated to customize the build for different environments.
  - `dependencies` element: This element specifies the dependencies that the project has on external libraries.
  - `repositories` element: This element specifies the locations of the remote repositories that the project depends on.
  - `pluginRepositories` element: This element specifies the locations of the remote plugin repositories that the project depends on.
  
**More**

- [POM Reference*maven.apache.org*](https://maven.apache.org/pom.html)
{.links-list}

---

> ### Appendix: About \<dependencies> and \<dependencyManagement> Elements
> 
> In Maven, the `<dependencies>` element is used to specify the dependencies of a project on external libraries. A dependency is a library that a project needs in order to compile and run. The `<dependencies>` element is typically used in the `pom.xml` file of a project to specify the dependencies that the project has on other libraries.
> 
> Here is an example of how to specify a dependency in the `pom.xml` file:
> 
> ```xml
> <dependencies>
>   <dependency>
>     <groupId>com.example</groupId>
>     <artifactId>example-library</artifactId>
>     <version>1.0</version>
>   </dependency>
> </dependencies>
> ```
> 
> The `<groupId>` element specifies the group or organization that the dependency belongs to, the `<artifactId>` element specifies the name of the dependency, and the `<version>` element specifies the version of the dependency.
> 
> The `<dependencyManagement>` element is used to manage the dependencies of a project and its modules. It is typically used in the parent `pom.xml` file of a multi-module project to specify the versions of the dependencies that are used across all the modules.
> 
> Here is an example of how to specify a dependency in the `<dependencyManagement>` element:
> 
> ```xml
> <dependencyManagement>
>   <dependencies>
>     <dependency>
>       <groupId>com.example</groupId>
>       <artifactId>example-library</artifactId>
>       <version>1.0</version>
>     </dependency>
>   </dependencies>
> </dependencyManagement>
> ```
> 
> By specifying the dependencies in the `<dependencyManagement>` element, you can ensure that all the modules of the project use the same version of the dependency, even if the modules do not explicitly specify the dependency. This can be useful for enforcing consistency across the modules of the project.

> ### Appendix: About \<repositories> Element
> 
> In Maven, the `<repository>` element is used to specify the location of a remote repository that contains the dependencies needed by a project. Maven uses a repository to manage the libraries and artifacts needed by a project, such as dependencies and plugins.
> 
> The `<repository>` element is typically used in the `pom.xml` file of a project to specify the location of a remote repository that contains the dependencies needed by the project. It can be used under the `<repositories>` element to specify a single repository, or under the `<pluginRepositories>` element to specify a repository for plugins.
> 
> Here is an example of how to specify a repository in the `pom.xml` file:
> 
> ```xml
> <repositories>
>   <repository>
>     <id>central</id>
>     <name>Central Repository</name>
>     <url>https://repo.maven.apache.org/maven2</url>
>     <layout>default</layout>
>   </repository>
> </repositories>
> ```
>   
> The `<id>` element specifies a unique identifier for the repository, the `<name>` element specifies a human-readable name for the repository, the `<url>` element specifies the URL of the repository, and the `<layout>` element specifies the layout of the repository.
> 
> By default, Maven uses the Central Repository, which is a public repository maintained by the Apache Maven project, as a source for dependencies. However, you can specify additional repositories in the `pom.xml` file if you need to use dependencies that are not available in the Central Repository.

> ### Appendix: About \<build> Element
> 
> In Maven, the `<build>` element is used to specify the build settings for a project. It is typically used in the `pom.xml` file of a project to specify the configuration for building the project, such as the final name of the built artifact, the directory for compiled source code, and the plugins to use.
> 
> Here is an example of the structure of the `<build>` element in the `pom.xml` file:
> 
> ```xml
> <build>
>   <finalName>${project.artifactId}-${project.version}</finalName>
>   <sourceDirectory>src/main/java</sourceDirectory>
>   <testSourceDirectory>src/test/java</testSourceDirectory>
>   <resources>
>     <resource>
>       <directory>src/main/resources</directory>
>     </resource>
>   </resources>
>   <testResources>
>     <testResource>
>       <directory>src/test/resources</directory>
>     </testResource>
>   </testResources>
>   <plugins>
>     <plugin>
>       <groupId>org.apache.maven.plugins</groupId>
>       <artifactId>maven-compiler-plugin</artifactId>
>       <version>3.8.0</version>
>       <configuration>
>         <source>1.8</source>
>         <target>1.8</target>
>       </configuration>
>     </plugin>
>   </plugins>
> </build>
> ```
> The `<finalName>` element specifies the final name of the built artifact, the `<sourceDirectory>` element specifies the directory where the source code is located, the `<testSourceDirectory>` element specifies the directory where the test source code is located, and the `<resources>` and `<testResources>` elements specify the locations of the resource files for the project and tests, respectively.
> 
> The `<plugins>` element is used to specify the plugins that are used in the build process. A plugin is a piece of code that provides additional functionality to Maven. In the example above, the `maven-compiler-plugin` is used to compile the source code of the project.

> ### Appendix: About the inheritance structure of pom.xml of multi-module project
> 
> In a Maven multi-module project, a parent `pom.xml` file is used to define common configuration and manage the modules of the project. The parent `pom.xml` file is located in the root directory of the project and defines the common properties, dependencies, and build plugins that are shared by all the modules.
> 
> Each module in the project has its own `pom.xml` file that specifies the configuration specific to that module. The child `pom.xml` files inherit the configuration from the parent `pom.xml` file unless they explicitly override it.
> 
> Here is an example of the structure of a Maven multi-module project:
> 
> ```
> root
> |-- pom.xml (parent pom)
> |-- module1
> |   |-- pom.xml (child pom)
> |-- module2
> |   |-- pom.xml (child pom)
> |-- module3
>     |-- pom.xml (child pom)
> ```
> 
> To define a module in the parent `pom.xml` file, you can use the `<module>` element under the `<modules>` element, like this:
>   
> ```
> <modules>
>   <module>module1</module>
>   <module>module2</module>
>   <module>module3</module>
> </modules>
> ```
> 
> Each child `pom.xml` file must have a `<parent>` element that specifies the group id, artifact id, and version of the parent `pom.xml` file, like this:
> 
> ```xml  
> <parent>
>   <groupId>com.example</groupId>
>   <artifactId>root</artifactId>
>   <version>1.0</version>
> </parent>
> ```

![maven.png](/maven.png){.align-center}