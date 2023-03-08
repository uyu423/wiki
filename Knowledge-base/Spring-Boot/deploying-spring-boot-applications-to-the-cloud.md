---
title: Spring Boot 애플리케이션을 클라우드에 배포
description: 
published: true
date: 2023-02-17T18:03:24.972Z
tags: 
editor: markdown
dateCreated: 2023-01-30T11:02:21.961Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Deploying Spring Boot Applications to the Cloud***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/deploying-spring-boot-applications-to-the-cloud)
{.links-list}


# Spring Boot 애플리케이션을 클라우드에 배포

오늘날 개발자는 애플리케이션을 배포할 플랫폼과 관련하여 선택의 폭이 넓습니다. 클라우드는 강력한 서비스를 제공하는 Amazon Web Services(AWS), Microsoft Azure 및 Google Cloud Platform(GCP)의 세 가지 주요 공급자와 함께 새로운 애플리케이션 배포를 위한 사실상의 표준이 되었습니다.

이 기사에서는 Spring Boot 애플리케이션을 클라우드에 배포하는 데 중점을 둘 것입니다. Spring Boot는 "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 쉽게 만들 수 있는 인기 있는 Java 기반 프레임워크입니다.

Spring Boot 애플리케이션을 클라우드에 배포하는 방법에는 여러 가지가 있습니다. 가장 널리 사용되는 두 가지 접근 방식을 다룰 것입니다.

* PaaS(Platform as a Service)에 배포
* IaaS(Infrastructure as a Service)에 배포

## PaaS(Platform as a Service)에 배포

PaaS(Platform as a Service)는 타사 공급자가 플랫폼 및 인프라 도구를 일반적으로 서비스형 플랫폼 형태로 인터넷을 통해 사용자에게 제공하는 클라우드 컴퓨팅 모델입니다.

PaaS는 클라우드에서 완전한 개발 및 배포 환경을 제공하므로 개발자는 기본 인프라에 대해 걱정하지 않고 코드 작성에 집중할 수 있습니다.

### 헤로쿠

인기 있는 PaaS 공급자 중 하나는 [Heroku](https://www.heroku.com/)로, Spring Boot 애플리케이션 호스팅에 최적화된 플랫폼을 제공합니다.

Heroku의 매력은 단순함에 있습니다. Spring Boot 애플리케이션을 Heroku에 배포하려면 프로젝트의 루트에 다음 줄을 포함하는 ` Procfile `을 생성하기만 하면 됩니다.

    웹: java -jar target/<응용 프로그램 이름>.jar

또한 ` pom.xml ` 파일에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
    <scope>provided</scope>
</dependency>
```

완료하면 `heroku` 명령줄 도구를 사용하여 응용 프로그램을 Heroku에 배포할 수 있습니다. 먼저 새 Heroku 애플리케이션을 만들어야 합니다.

    헤로쿠 생성

그런 다음 애플리케이션을 Heroku에 배포할 수 있습니다.

    git push 헤로쿠 마스터

이제 애플리케이션이 `https://<your-app-name>.herokuapp.com`에서 실행됩니다.

### 클라우드 파운드리

[Cloud Foundry](https://www.cloudfoundry.org/)는 Spring Boot 애플리케이션 배포를 고려할 가치가 있는 또 다른 인기 있는 PaaS 공급자입니다.

Heroku와 마찬가지로 Cloud Foundry를 사용하면 Spring Boot 애플리케이션을 쉽게 배포할 수 있습니다. Spring Boot 애플리케이션을 Cloud Foundry에 배포하려면 먼저 프로젝트의 루트에 ` manifest.yml ` 파일을 생성해야 합니다. 이 파일에는 이름, 메모리 제한 및 호스트 이름과 같은 애플리케이션에 대한 정보가 포함되어 있습니다.

다음은 ` manifest.yml ` 파일의 예입니다.

```yaml
---
applications:
- name: my-app
  memory: 512M
  disk_quota: 1024M
  instances: 1
  path: build/libs/my-app.jar
  env:
    JAVA_OPTS: -Djava.security.egd=file:///dev/urandom
  buildpack: https://github.com/cloudfoundry/java-buildpack
```

그런 다음 `cf` 명령줄 도구를 사용하여 애플리케이션을 Cloud Foundry에 배포할 수 있습니다.

    cf 푸시

이제 애플리케이션이 `https://<your-app-name>.cfapps.io`에서 실행됩니다.

## IaaS(Infrastructure as a Service)에 배포

IaaS(Infrastructure as a Service)는 타사 공급자가 인터넷을 통해 사용자에게 인프라(일반적으로 서버, 스토리지 및 네트워킹)를 제공하는 클라우드 컴퓨팅 모델입니다.

IaaS는 개발자에게 PaaS보다 기본 인프라에 대한 훨씬 더 많은 제어 기능을 제공하지만 설정 및 유지 관리에 더 많은 작업이 필요합니다.

### AWS

AWS(Amazon Web Services)는 가장 인기 있는 IaaS 공급자이며 Spring Boot 애플리케이션을 호스팅하는 데 사용할 수 있는 광범위한 서비스를 제공합니다. 이 섹션에서는 [Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/)를 사용하여 Spring Boot 애플리케이션을 AWS에 배포하는 방법에 중점을 둘 것입니다.

Elastic Beanstalk는 Java, .NET, PHP, Node.js, Python 및 Ruby로 개발된 웹 애플리케이션 및 서비스를 Apache, Nginx, Passenger 및 IIS와 같은 친숙한 서버에 쉽게 배포, 관리 및 확장할 수 있는 서비스입니다. .

Elastic Beanstalk에 Spring Boot 애플리케이션을 배포하려면 먼저 프로젝트의 ` src/main/resources ` 디렉터리에 ` application.properties ` 파일을 생성해야 합니다. 이 파일에는 이름, 버전 및 환경과 같은 애플리케이션에 대한 정보가 포함되어 있습니다.

다음은 ` application.properties ` 파일의 예입니다.

```properties
name=my-app
version=1.0.0
environment=production
```

또한 프로젝트의 루트에 ` AWS Elastic Beanstalk ` 파일을 생성해야 합니다. 이 파일에는 리전, 인스턴스 유형 및 보안 그룹과 같은 애플리케이션 환경에 대한 정보가 포함되어 있습니다.

다음은 ` AWS Elastic Beanstalk ` 파일의 예입니다.

```yaml
---
AWSEBDebuggingMode: true
AWSEBEnvironmentVariables:
  JAVA_OPTS: -Djava.security.egd=file:///dev/urandom
AWSEBServiceRole: null
AWSEBUseAmi64: true
AWSEluaticLoadBalancerScheme: internet-facing
AWSEBSecurityGroups:
- my-security-group
AWSEBSubnets:
- subnet-12345678
AWSEBIAMInstanceProfile: null
AWSEBRDSDatabaseInstance: null
AWSEBRDSDatabasePassword: null
AWSEBRDSDatabaseUsername: null
AWSEBRDSDatabaseEngine: null
AWSEBRDSDatabaseName: null
AWSEBRDSSnapshotIdentifier: null
AWSEBRDSAllocatedStorage: null
AWSEBRDSStorageType: null
AWSEBRDSMultiAZ: null
AWSEBRDSIops: null
AWSEBRDSEncrypted: null
AWSEBRDSKmsKeyId: null
AWSEBRDSDeletionPolicy: null
AWSEBS3Key: my-s3-key
AWSEBS3Bucket: my-s3-bucket
AWSEBS3ObjectKey: my-s3-object-key
AWSEBS3ETag: my-s3-etag
AWSEBS3VersionId: my-s3-version-id
AWSEBS3Region: us-east-1
AWSEBS3StorageClass: STANDARD
AWSEBNotificationEndpoint: null
AWSEBNotificationProtocol: null
AWSEBNotificationTopicARN: null
AWSEBManagedActionHistoryRetentionPeriod: 14
```

이러한 파일을 만들고 나면 `eb` 명령줄 도구를 사용하여 애플리케이션을 Elastic Beanstalk에 배포할 수 있습니다. 먼저 새 Elastic Beanstalk 애플리케이션을 생성해야 합니다.

    EB 생성

그런 다음 애플리케이션을 Elastic Beanstalk에 배포할 수 있습니다.

    EB 배포

이제 애플리케이션이 `http://<your-app-name>.elasticbeanstalk.com`에서 실행됩니다.

### 아주르

Microsoft Azure는 Spring Boot 애플리케이션을 호스팅하는 데 사용할 수 있는 다양한 서비스를 제공하는 인기 있는 또 다른 IaaS 공급자입니다. 이 섹션에서는 [App Service](https://docs.microsoft.com/en-us/azure/app-service/overview)를 사용하여 Azure에 Spring Boot 애플리케이션을 배포하는 방법에 중점을 둘 것입니다.

App Service는 웹 애플리케이션 및 웹 서비스 호스팅에 최적화된 Microsoft Azure PaaS 서비스입니다. App Service에 Spring Boot 애플리케이션을 배포하려면 먼저 프로젝트의 ` src/main/resources ` 디렉터리에 ` application.properties ` 파일을 만들어야 합니다. 이 파일에는 이름, 버전 및 환경과 같은 애플리케이션에 대한 정보가 포함되어 있습니다.

다음은 ` application.properties ` 파일의 예입니다.

```properties
name=my-app
version=1.0.0
environment=production
```

또한 프로젝트의 ` src/main/webapp/WEB-INF ` 디렉토리에 ` web.xml ` 파일을 생성해야 합니다. 이 파일에는 서블릿 클래스 및 매핑과 같은 애플리케이션의 서블릿에 대한 정보가 포함되어 있습니다.

다음은 ` web.xml ` 파일의 예입니다.

```xml
<web-app>
  <servlet>
    <servlet-name>my-app</servlet-name>
    <servlet-class>org.springframework.boot.web.servlet.support.SpringBootServletInitializer</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>my-app</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
</web-app>
```

이러한 파일을 만들고 나면 `az` 명령줄 도구를 사용하여 애플리케이션을 App Service에 배포할 수 있습니다. 먼저 새 App Service 애플리케이션을 만들어야 합니다.

    az appservice plan create --name my-app-service-plan --resource-group my-resource-group --sku S1

그런 다음 애플리케이션을 App Service에 배포할 수 있습니다.

    az webapp create --resource-group my-resource-group --plan my-app-service-plan --name my-app --deployment-container-image="mcr.microsoft.com/java/jdk:8u192- 줄루-알파인"

이제 애플리케이션이 `http://my-app.azurewebsites.net`에서 실행됩니다.

## 결론

이 기사에서는 Spring Boot 애플리케이션을 클라우드에 배포하는 두 가지 방법을 살펴보았습니다.

* PaaS(Platform as a Service)에 배포
* IaaS(Infrastructure as a Service)에 배포

각 접근 방식에는 고유한 장점과 단점이 있으므로 애플리케이션에 적합한 것을 선택하는 것이 중요합니다.

애플리케이션을 클라우드에서 시작하고 실행할 수 있는 빠르고 쉬운 방법을 찾고 있다면 PaaS가 적합합니다. Heroku와 Cloud Foundry는 고려할 가치가 있는 두 가지 인기 있는 PaaS 제공업체입니다.

기본 인프라에 대한 더 많은 제어를 찾고 있다면 IaaS가 갈 길입니다. AWS와 Azure는 Spring Boot 애플리케이션을 호스트하는 데 사용할 수 있는 광범위한 서비스를 제공하는 두 가지 인기 있는 IaaS 공급자입니다.