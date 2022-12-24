---
title: Maven pom.xml 개요
description: 
published: true
date: 2022-12-24T16:18:11.574Z
tags: java, maven, springboot
editor: markdown
dateCreated: 2022-12-23T09:49:18.780Z
---

# Korean

## maven pom.xml 의 구조에 대한 세부 정보

- Maven은 주로 Java 프로젝트에 사용되는 빌드 자동화 도구입니다. 프로젝트의 빌드 프로세스, 종속성 및 문서를 관리하는 데 도움이 됩니다.
- `pom.xml` 파일은 Maven에서 프로젝트 구성의 핵심입니다. Maven에서 프로젝트를 빌드하는 데 사용하는 프로젝트 및 구성 세부 정보에 대한 정보가 포함된 XML 파일입니다.
- 다음은 `pom.xml` 파일에 포함될 수 있는 주요 요소에 대한 요약입니다.
   - `project`: 이 요소는 `pom.xml` 파일의 루트 요소입니다. 여기에는 그룹 ID, 아티팩트 ID 및 버전과 같은 프로젝트에 대한 정보가 포함됩니다.
   - `modelVersion`: 이 요소는 사용 중인 POM 모델의 버전을 지정합니다.
   - `groupId`: 이 요소는 프로젝트가 속한 그룹의 고유 식별자를 지정합니다.
   - `artifactId`: 이 요소는 프로젝트의 고유 식별자를 지정합니다.
   - `version`: 이 요소는 프로젝트의 버전을 지정합니다.
   - `packaging`: 이 요소는 `jar`, `war` 또는 `ear`와 같은 프로젝트의 패키지 유형을 지정합니다.
   - `name`: 이 요소는 프로젝트의 이름을 지정합니다.
   - `설명`: 이 요소는 프로젝트에 대한 설명을 제공합니다.
   - `url`: 이 요소는 프로젝트 홈페이지의 URL을 지정합니다.
   - `prerequisites`: 이 요소는 프로젝트를 빌드하는 데 필요한 전제 조건을 지정합니다.
   - `issueManagement`: 이 요소는 프로젝트의 이슈를 관리하는 데 사용되는 URL 및 시스템을 지정합니다.
   - `ciManagement`: 이 요소는 프로젝트의 지속적인 통합에 사용되는 URL 및 시스템을 지정합니다.
   - `inceptionYear`: 이 요소는 프로젝트가 생성된 연도를 지정합니다.
   - `licenses`: 이 요소는 프로젝트가 배포되는 라이선스를 지정합니다.
   - `developers`: 이 요소는 프로젝트에 기여한 개발자를 지정합니다.
   - `contributors`: 이 요소는 프로젝트 기여자를 지정합니다.
   - `mailingLists`: 이 요소는 프로젝트의 메일링 리스트를 지정합니다.
   - `scm`: 이 요소는 프로젝트에 대한 소스 제어 관리 시스템 및 연결 정보를 지정합니다.
   - `organization`: 이 요소는 프로젝트를 담당하는 조직을 지정합니다.
   - `build`: 이 요소는 빌드된 아티팩트의 최종 이름, 컴파일된 소스 코드의 디렉토리 및 사용할 플러그인과 같은 프로젝트에 대한 빌드 설정을 지정합니다.
   - `profiles`: 이 요소는 다양한 환경에 대한 빌드를 사용자 지정하기 위해 활성화할 수 있는 다양한 빌드 프로필을 지정합니다.
   - `dependencies`: 이 요소는 프로젝트가 외부 라이브러리에 갖는 종속성을 지정합니다.
   - `repositories`: 이 요소는 프로젝트가 의존하는 원격 저장소의 위치를 지정합니다.
   - `pluginRepositories`: 이 요소는 프로젝트가 의존하는 원격 플러그인 저장소의 위치를 지정합니다.

**More**

- [POM Reference*maven.apache.org*](https://maven.apache.org/pom.html)
{.links-list}

> ### 부록: \<dependencies> 및 \<dependencyManagement> 에 대하여
>
> Maven에서 `<dependencies>` 요소는 외부 라이브러리에 대한 프로젝트의 종속성을 지정하는 데 사용됩니다. 종속성은 프로젝트를 컴파일하고 실행하기 위해 필요한 라이브러리입니다. `<dependencies>` 요소는 일반적으로 프로젝트의 `pom.xml` 파일에서 프로젝트가 다른 라이브러리에 대해 가지는 종속성을 지정하는 데 사용됩니다.
>
> 다음은 `pom.xml` 파일에서 종속성을 지정하는 방법의 예입니다.
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
> `<groupId>` 요소는 종속성이 속한 그룹 또는 조직을 지정하고 `<artifactId>` 요소는 종속성의 이름을 지정하며 `<version>` 요소는 종속성의 버전을 지정합니다.
>
> `<dependencyManagement>` 요소는 프로젝트 및 해당 모듈의 종속성을 관리하는 데 사용됩니다. 일반적으로 모든 모듈에서 사용되는 종속성 버전을 지정하기 위해 다중 모듈 프로젝트의 상위 `pom.xml` 파일에서 사용됩니다.
>
> 다음은 `<dependencyManagement>` 요소에 종속성을 지정하는 방법의 예입니다.
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
> `<dependencyManagement>` 요소에 종속성을 지정하면 모듈이 명시적으로 종속성을 지정하지 않더라도 프로젝트의 모든 모듈이 동일한 버전의 종속성을 사용하도록 할 수 있습니다. 이는 프로젝트의 모듈 간에 일관성을 유지하는 데 유용할 수 있습니다.

---

# English

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
> To define a module in the parent pom.xml file, you can use the `<module>` element under the `<modules>` element, like this:
>   
> ```
> <modules>
>   <module>module1</module>
>   <module>module2</module>
>   <module>module3</module>
> </modules>
> ```
> 
> Each child pom.xml file must have a `<parent>` element that specifies the group id, artifact id, and version of the parent pom.xml file, like this:
> 
> ```xml  
> <parent>
>   <groupId>com.example</groupId>
>   <artifactId>root</artifactId>
>   <version>1.0</version>
> </parent>
> ```

- [POM Reference*maven.apache.org*](https://maven.apache.org/pom.html)
{.links-list}