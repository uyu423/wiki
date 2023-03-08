---
title: pom.xml
description: 
published: true
date: 2023-02-17T18:00:08.122Z
tags: springboot, maven, java
editor: markdown
dateCreated: 2022-12-23T09:49:18.780Z
---

- [pom.xml***Korean** version of this document is available*](/en/dev/Maven/overview-maven-pom-xml)
{.links-list}

## maven pom.xml 의 구조에 대한 세부 정보

- Maven은 주로 Java 프로젝트에 사용되는 빌드 자동화 도구입니다. 프로젝트의 빌드 프로세스, 종속성 및 문서를 관리하는 데 도움이 됩니다.
- `pom.xml` 파일은 Maven에서 프로젝트 구성의 핵심입니다. Maven에서 프로젝트를 빌드하는 데 사용하는 프로젝트 및 구성 세부 정보에 대한 정보가 포함된 XML 파일입니다.
- 다음은 `pom.xml` 파일에 포함될 수 있는 주요 요소에 대한 요약입니다.
   - `project`: `pom.xml` 파일의 루트 요소입니다. 여기에는 그룹 ID, 아티팩트 ID 및 버전과 같은 프로젝트에 대한 정보가 포함됩니다.
   - `modelVersion`: 사용 중인 POM 모델의 버전을 지정합니다.
   - `groupId`: 프로젝트가 속한 그룹의 고유 식별자를 지정합니다.
   - `artifactId`: 프로젝트의 고유 식별자를 지정합니다.
   - `version`: 프로젝트의 버전을 지정합니다.
   - `packaging`: `jar`, `war` 또는 `ear`와 같은 프로젝트의 패키지 유형을 지정합니다.
   - `name`: 프로젝트의 이름을 지정합니다.
   - `description`: 프로젝트에 대한 설명을 제공합니다.
   - `url`: 프로젝트 홈페이지의 URL을 지정합니다.
   - `prerequisites`: 프로젝트를 빌드하는 데 필요한 전제 조건을 지정합니다.
   - `issueManagement`: 프로젝트의 이슈를 관리하는 데 사용되는 URL 및 시스템을 지정합니다.
   - `ciManagement`: 프로젝트의 지속적인 통합(CI, Continuous Integration)에 사용되는 URL 및 시스템을 지정합니다.
   - `inceptionYear`: 프로젝트가 생성된 연도를 지정합니다.
   - `licenses`: 프로젝트가 배포되는 라이선스를 지정합니다.
   - `developers`: 프로젝트의 개발자를 지정합니다.
   - `contributors`: 프로젝트 기여자를 지정합니다.
   - `mailingLists`:프로젝트의 메일링 리스트를 지정합니다.
   - `scm`: 프로젝트에 대한 소스 제어 관리 시스템 및 연결 정보를 지정합니다.
   - `organization`: 프로젝트를 담당하는 조직을 지정합니다.
   - `build`: 빌드된 아티팩트의 최종 이름, 컴파일된 소스 코드의 디렉토리 및 사용할 플러그인과 같은 프로젝트에 대한 빌드 설정을 지정합니다.
   - `profiles`: 다양한 환경에 대한 빌드를 사용자 지정하기 위해 활성화할 수 있는 다양한 빌드 프로필을 지정합니다.
   - `dependencies`: 프로젝트가 외부 라이브러리에 갖는 종속성을 지정합니다.
   - `repositories`: 프로젝트가 의존하는 원격 저장소의 위치를 지정합니다.
   - `pluginRepositories`: 프로젝트가 의존하는 원격 플러그인 저장소의 위치를 지정합니다.

**More**

- [POM Reference*maven.apache.org*](https://maven.apache.org/pom.html)
{.links-list}

---

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

> ### 부록: \<repositories> 요소 정보
>
> Maven에서 `<repository>` 요소는 프로젝트에 필요한 종속성을 포함하는 원격 저장소의 위치를 지정하는 데 사용됩니다. Maven은 리포지토리를 사용하여 종속성 및 플러그인과 같이 프로젝트에 필요한 라이브러리 및 아티팩트를 관리합니다.
>
> `<repository>` 요소는 일반적으로 프로젝트의 `pom.xml` 파일에서 프로젝트에 필요한 종속성을 포함하는 원격 저장소의 위치를 지정하는 데 사용됩니다. `<repositories>` 요소 아래에서 단일 저장소를 지정하거나 `<pluginRepositories>` 요소 아래에서 플러그인 저장소를 지정할 수 있습니다.
>
> 다음은 `pom.xml` 파일에서 리포지토리를 지정하는 방법의 예입니다.
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
> `<id>` 요소는 저장소의 고유 식별자를 지정하고 `<name>` 요소는 사람이 읽을 수 있는 저장소 이름을 지정하며 `<url>` 요소는 저장소의 URL을 지정하고 ` <layout>` 요소는 저장소의 레이아웃을 지정합니다.
>
> 기본적으로 Maven은 Apache Maven 프로젝트에서 유지 관리하는 공용 저장소인 Central Repository를 종속 항목의 소스로 사용합니다. 그러나 중앙 저장소에서 사용할 수 없는 종속성을 사용해야 하는 경우 `pom.xml` 파일에서 추가 저장소를 지정할 수 있습니다.

> ### 부록: \<build> 요소 정보
>
> Maven에서 `<build>` 요소는 프로젝트의 빌드 설정을 지정하는 데 사용됩니다. 일반적으로 프로젝트의 `pom.xml` 파일에서 빌드된 아티팩트의 최종 이름, 컴파일된 소스 코드의 디렉터리 및 사용할 플러그인과 같은 프로젝트 빌드를 위한 구성을 지정하는 데 사용됩니다.
>
> 다음은 `pom.xml` 파일에 있는 `<build>` 요소 구조의 예입니다.
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
> `<finalName>` 요소는 빌드된 아티팩트의 최종 이름을 지정하고, `<sourceDirectory>` 요소는 소스 코드가 있는 디렉토리를 지정하고, `<testSourceDirectory>` 요소는 테스트 소스 코드가 있는 디렉토리를 지정합니다. `<resources>` 및 `<testResources>` 요소는 각각 프로젝트 및 테스트에 대한 리소스 파일의 위치를 지정합니다.
>
> `<plugins>` 요소는 빌드 프로세스에서 사용되는 플러그인을 지정하는 데 사용됩니다. 플러그인은 Maven에 추가 기능을 제공합니다. 위의 예에서 `maven-compiler-plugin`은 프로젝트의 소스 코드를 컴파일하는 데 사용됩니다.

> ### 부록: 다중 모듈 프로젝트의 pom.xml 상속 구조에 대하여
>
> Maven 다중 모듈 프로젝트에서 상위 `pom.xml` 파일은 공통 구성을 정의하고 프로젝트의 모듈을 관리하는 데 사용됩니다. 상위 `pom.xml` 파일은 프로젝트의 루트 디렉터리에 있으며 모든 모듈에서 공유하는 공통 속성, 종속성 및 빌드 플러그인을 정의합니다.
>
> 프로젝트의 각 모듈에는 해당 모듈에 특정한 구성을 지정하는 자체 `pom.xml` 파일이 있습니다. 하위 `pom.xml` 파일은 명시적으로 재정의하지 않는 한 상위 `pom.xml` 파일에서 구성을 상속합니다.
>
> 다음은 Maven 다중 모듈 프로젝트 구조의 예입니다.
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
> 상위 `pom.xml` 파일에서 모듈을 정의하려면 다음과 같이 `<modules>` 요소 아래에 `<module>` 요소를 사용할 수 있습니다.
>
> ```
> <modules>
>   <module>module1</module>
>   <module>module2</module>
>   <module>module3</module>
> </modules>
> ```
>
> 각 하위 `pom.xml` 파일에는 다음과 같이 상위 `pom.xml` 파일의 그룹 ID, 아티팩트 ID 및 버전을 지정하는 `<parent>` 요소가 있어야 합니다.
>
> ```xml  
> <parent>
>   <groupId>com.example</groupId>
>   <artifactId>root</artifactId>
>   <version>1.0</version>
> </parent>
> ```

![maven.png](/maven.png){.align-center}